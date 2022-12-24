---
layout: post
title:  "Jedis Pool"
date:   2022-12-22 00:01:05 +0530
categories: [redis, java]
---


In order to use [Redis](https://redis.io/) in java, we need to use one of client libraries like [Jedis](https://github.com/redis/jedis), [Redisson](https://github.com/mrniko/redisson) or [Lettuce](https://github.com/lettuce-io/lettuce-core).  

So far I have mostly worked with Jedis. For all interactions with Redis, we need to use a `Jedis` object. Common convention is to create a `JedisPool` and then obtain an instance of Jedis from that. Using pool ensures that connection resources are used optimally. 

### Minimum setup of JedisPool

- Minimum configuration required to setup `JedisPool` is to pass `host` in constructor so that it can connect to redis instance hosted on that host. This will use default port `6379` for connecting to redis. 

	```java
	JedisPool pool = new JedisPool(host);
	```

- If we want to use a custom port for connecting to redis, that has to be passed in constructor of `JedisPool`.
	```java
	JedisPool pool = new JedisPool(host, port);
	```

### Configuring JedisPool
Above setup will create a `JedisPool` instance with default configuration for pool.

- If we want to pass a custom pool configuration, then we need to build an instance of `JedisPoolConfig` class and configure it accordingly.
	```java
	JedisPoolConfig poolConfig = new JedisPoolConfig();
	// Max number of Jedis instances in pool, default is 8
    poolConfig.setMaxTotal(8);      

    // Max number of allowed idle Jedis instances in pool, default is 8. Extra idle instances are destroyed.
    poolConfig.setMaxIdle(8);		

	// Min number of idle Jedis instances in pool. Pool will target to keep idle instances to this. default is 0	
    poolConfig.setMinIdle(0);	

    // Whether to validate idle instances in pool.
    // If validation fails, instance will be removed from pool & destroyed.
    // By default is is enabled.
    poolConfig.setTestWhileIdle(true);	

    // Minimum idle duraion after which instance is eligible for eviction. Default is 1 minute.
    poolConfig.setMinEvictableIdleTimeMillis(60000);

    // Sleep time between eviction runs, default is 30 seconds.
    poolConfig.setTimeBetweenEvictionRunsMillis(30000);

    // Number of instances to test for eviction in each run, default is to cehck for each idle instance.
    poolConfig.setNumTestsPerEvictionRun(-1);

    // If enabled, pool returns most recently used instance from pool.
    // If disabled, pool returns least recently used instance from pool.
    // By deafult it is enabled.
    poolConfig.setLifo(true);

    // If enabled, pool serves first thread that requested for instance.
    // By default it is disabled, so any thread could be served first irrespective of order in which it requested.
    poolConfig.setFairness(false)

    // Amount of time any thread will wait before throwing exception in case pool is exhausted.
    // By default threads are blocked indefinitely.
	poolConfig.setMaxWaitMillis(-1)

	// There are many more but these seem most useful ones.
	```

- After that just pass this config into JedisPool constructor.
	```java
	JedisPool pool = new JedisPool(poolConfig, host, port);	
	```

### Using JedisPool
- After setting up JedisPool, next step is to get an instance of `Jedis` and use that for interactions with redis.
	```java
	try (Jedis jedis = pool.getResource()) {
		...
	}
	```
- Always make sure `Jedis` instance is resturned back to pool after use. This can be done in two ways
	- use within `try-with-resources` block as shown in above example, or
	- explicitly call close on `Jedis` instance
	```java
	Jedis jedis = pool.getResource();
	...
	jedis.close();
	```

If we miss to return instance back to pool, it will get exhausted and any threads asking for next instance could get blocked indefinitely. I recently learned this hard way, so I would highly recommend to always return `Jedis` instance back to pool.

How to use Jedis intance to interact with Redis? I will cover that in some other post and add a link here.

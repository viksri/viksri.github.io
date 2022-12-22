---
layout: post
title:  "Jedis Pool"
date:   2022-12-22 00:01:05 +0530
categories: redis
---

This post is to note down understanding of jedis pools. Today I have hit an issue where test got stuck because we missed to return back jedis instances to jedis pool after use.

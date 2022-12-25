---
layout: post
title:  "Zigzag Encoding"
date:   2022-12-25 19:43:05 +0530
categories: serialization
---

I got to know about zigzag encoding while trying to understand [protobuf encoding](https://developers.google.com/protocol-buffers/docs/encoding). It is simple but very efficient way to encode negative integers. Before we go deep into zigzag encoding, lets first start with how integers are usually encoded in binary.

#### Binary encoding of integers

Integers are encoded as 4 bytes.
- MSB(Most Significant Bit) represents sign bit. If MSB is 1, it is negative integer otherwise it is positive integer.
- Rest of bits represent value of integer. 
	- For positive integers, it is simply binary representation of integer. So representation of +24 will be
	```
		sign bit :                              0       	// number is positive
		binary representation of 24 :           00011000	
		binary represntation of 24 in 31 bits : 0000000 00000000 00000000 00011000	
	``` 
	so binary encoding of +24 is `00000000 00000000 00000000 00011000`. We can efficiently store it as `00011000` and save 3 bytes.

	- For negative integers, value is encoded as 2's complement of value. So representation of -24 will be
	```
		sign bit :                              1           // number is negative
		binary representation of 24 :           00011000
		binary represntation of 24 in 31 bits : 0000000 00000000 00000000 00011000	
		1's complement of 24 in 31 bits :       1111111 11111111 11111111 11100111
		2's complement of 24 in 31 bits :       1111111 11111111 11111111 11101000                               
	``` 
	so binary encoding of -24 is `11111111 11111111 11111111 11101000`. It is not possible to efficiently store negative numbers as it will always take 4 bytes.	


#### How zigzag encoding works

To overcome space inefficiency in storing smaller negative integers with 2's complement notation, zigzag encoding converts negative numbers into positive number.
- Each positive number `n` is encoded as `2 * n`, and 
- Each negative number is encoded as `2 * n + 1`.

	- In zigzag encoding +24, will be encoded as 48
	```
		binary representation of 48 :           00110000	
	``` 
	It will again take only 1 byte.
	- In zigzag encoding -24, will be encoded as 49
	```
		binary representation of 48 :           00110001	
	```
	It will take only 1 byte, which saves us 3 bytes compared to 2's complement notation.
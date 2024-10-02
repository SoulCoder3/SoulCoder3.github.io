---
layout:     post
title:      Computer Network Note 09-30
subtitle:   Computer Network
date:       2024-9-30
author:     BY David
header-img: img/TechTool.jpg
catalog: true
tags:
    - Computer Network
    - Note

---

## Byte Stuffing
* Same as bit stuffing, except at byte level
    * Generally have two different flags, STX and ETX
    * Found in PPP, DDCMP. BISYNC, etc
* Need to stuff if either appears in the payload
    * Prefix with another special character, DLE(data link escape)
    * New problem: what if DLE appears in payload?
* Stuff DLE with DLE
    * Could be as bad as 50% efficient to send all DLEs

## Clock-Based Framing
* Any bit errors may throw off our framing
* An alternative is to base framing on external clock
    * This is what SONET does, among others
* Significant engineering tradeoffs
* No extra bits needed in the data stream
* Clock drift may confuse frame boundaries
    * read the end of one frame and beginning of the next
* Error detection- and perhaps correction

## Per-Frame Detection Codes
* want to add an error detection code per frame
    * Frame is unit of transmission; all or nothing.
    * Computed over the entire frame -- including header!
* Receiver checks EDS to make sure frame is valid
    * If frame fails check, throw it away
* We could use error-correcting codes
    * But they are less efficient, and we expect errors to be rare
    * Counter example: satellite communication

## Coding
* The problem is data itself is not self-verifying
    * Every string of bits is potentially legitimate
    * Hence, any errors/changes in a set of bits a re equally legit
* The solution is to reduce the set of potential bitstrings
    * Not every string of bits is allowable
    * Receipt of a disallowed string of bits means the original bits were garbled in transit

## Codewords
* Efficient codes are of uniform Hamming Distance -- Distance between legal codewords
    * All codewords are equidistant from their neighbors

## 2D+1 Hamming Distance
* Can detect up to 2 bit flips
    * Any fewer if guaranteed to land in the middle
* Can correct up to d bit flips

## parity 
* EDS is an extra bit computed to ensure odd(even) number of ones
* Code has a rate of 2/3 (need three bits to encode two)
Note: Even parity is simply XOR

## Voting
* EDC just duplicates data bit n times
* Straightforward duplication is extremely inefficient

## CheckSsums
* EDC is the sume of the data in the frame
* Extremely lightweight
* Also easy to modify if frame is modified in fligth
* IP packets include a 1's complement checksum

## Cyclic remainder check
* Idea is to divide the incoming data, D, rather than add
    * the divisor is called the generator, g

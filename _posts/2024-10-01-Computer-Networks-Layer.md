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

## Layering: A Modular Approach
* **Sub-divide the problem**
  * Each layer relies on services from layer below
  * Eacher layer exports services to layer above
* **Interface between layers defines interaction**
  * Hides implementation details(**encapsulation**)
  * Layers can change without disturbing other layers(**modularity**)
* **Interface among peers in a layer is a protocol**
  * If peers speak same protocol, they can interoperate

## Key Design Decision
* **End-to-end argument**
  * Functionality should be implemented at a lower layer **if and only if** it can be **correctly** and **completely** implemented there
  * Incomplete versions of a function can be used as a performance enhancement, but not for correctness
* Early, and still relevant, example
* ARPAnet provided reliable link transfers between switches
* **Was this enough for reliable communication**
  * No, Packets could still get corrupted on host-switch link, or inside of the switches
  * Hence, still need reliability at higher layers

## Protocol Standardization
* **Communicating hosts speaking the same protocol**
  * Standardization to enable multiple implementations
  * Or, the same folks have to write all the software
* **Internet Engineering Task Force**
  * Based on working groups that focus on specific issues
  * Produces "Request For Comments"(RFCs)
    * Rough consensus and running code
    * After enough timepasses, promoted to Internet Standards
  * **Other standards bodies exist**
    * IOS, ITU, IEEE, etc.
  * ![web packet](/img/2024-10-01-Computer-Network-01/web-packet.png)
  * **Notice that layers add overhead**
    * Space(**header**), effective bandwidth
    * Time(**processing headers， “peeling the onion”**), latency
## Later: Phy/(MAC) Link Layer
* **Signal encoding**
  * Encode binary data from source node into signals that physical links carry
  * Signal is decoded back into binary data at receiving node
  * Work performed by network aadapter at sender and receiver
* Media access
  * Arbitrate which nodes can send frames at any point in time
  * Not always necessary, like point-to-point duplex links

## Framing
* Break down a steam of bits into smaller, digestible chunks called **frames**
  * Identify the beginning and the end of the bistream
* Allows the link to be shared
  * Mulitple senders and/or receivers can **time multiplex** the link
  * Each frame can be separately addressed
* Provides manageable unit for error handing
  * Easy to determine whether something went wrong
  * And perhaps even to fix it if desired

## What is Frame?
* Wraps payload up with some additional information
  * Header usually contains addressing information
  * Maybe includes a trailer
* Basic unit of reception
  * Link either delivers entire frame payload, or none of it
  * Typically, some **maximum transmission unit(MTU)**
* Some link layers require absence of frames as well

## Fixed-Length Frames
* Easy to manage for receiver
  * Well understood buffering requirement
* Introduces inefficiencis for variable length payloads
  * May waste space(padding) for small payloads
  * Larger payloads need to be **fragmented across many frames**
  * Very common inside switches

## Length-Based Framing
* ![Length-based](/img/2024-10-01-Computer-Network-01/Length-based.png)
* To avoid overhead, we'd like variable length frames
## Sentinel-based Framing
* Allow for variable length frames
* Idea: Mark start/end of frame with special "marker"
  * Byte pattern, bit pattern, singal patter
* Must make sure marker doesn't appear in data
* **Two solution**
  * Special non-data physical-layer symbol
    * Impact on efficiency(can't use symbol for data) if code
  * Stuffing
    * Dynamically remove marker bit patterns from data stream
    * Receiver "unstuffs" data stream to reconstruct original data
## Bit-level Stuffing
* Avoid sentinel bit pattern in payload data
  * sentinel is bit pattern **011111110**
* Sender: any time **five** ones appear in outgoing data, insert a zero
* Receiver: any time five ones appear, removes next zero
  * If there is no zero, there will either be six one(sentinel) or
  * It declares an error condition
  * bit pattern that cannot appear is 01111111
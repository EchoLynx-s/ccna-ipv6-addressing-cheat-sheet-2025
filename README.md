# CCNA – IPv6 Addressing (Module 12)

> **Use case:** This repo file is both a study guide for me (**EchoLynx**) and a
> portfolio artifact for recruiters to see my understanding of **IPv6
> addressing, coexistence with IPv4, and IPv6 subnetting**.

Quick-reference notes for NetAcad CCNA – **Module 12: IPv6 Addressing**.  
Focus is on why IPv6 exists, how IPv6 addresses are written, and how to
configure / verify IPv6 GUAs, LLAs, and subnets on hosts and routers.

I use this repo to revise:

- Why IPv4 alone is not enough and how **IPv4 + IPv6 coexist** in real networks.
- How to **read and write IPv6 addresses** (full, compressed, double-colon rules).
- The main **IPv6 address types**: global unicast, link-local, unique local,
  multicast, anycast.
- How to **statically and dynamically configure** IPv6 GUAs and LLAs
  (SLAAC, DHCPv6, EUI-64, random IIDs).
- How IPv6 **multicast** is used (`FF02::1`, `FF02::2`, solicited-node, etc.).
- How to **subnet an IPv6 /64 or larger prefix** using subnet IDs.

---

## Table of Contents

- [Module 12 Overview](#module-12-overview)  
- [Module Map](#module-map)  

- [12.0 Introduction](#120-introduction)  
  - [12.0.1 Why should I take this module?](#1201-why-should-i-take-this-module)  
  - [12.0.2 What will I learn in this module?](#1202-what-will-i-learn-in-this-module)  

- [12.1 IPv4 Issues](#121-ipv4-issues)  
  - [12.1.1 Need for IPv6](#1211-need-for-ipv6)  
  - [12.1.2 IPv4 and IPv6 Coexistence](#1212-ipv4-and-ipv6-coexistence)  
  - [12.1.3 Check Your Understanding – IPv4 Issues](#1213-check-your-understanding--ipv4-issues)  

- [12.2 IPv6 Address Representation](#122-ipv6-address-representation)  
  - [12.2.1 IPv6 Addressing Formats](#1221-ipv6-addressing-formats)  
  - [12.2.2 Rule 1 – Omit Leading Zeros](#1222-rule-1--omit-leading-zeros)  
  - [12.2.3 Rule 2 – Double Colon](#1223-rule-2--double-colon)  
  - [12.2.4 Check Your Understanding – IPv6 Address Representation](#1224-check-your-understanding--ipv6-address-representation)  

- [12.3 IPv6 Address Types](#123-ipv6-address-types)  
  - [12.3.1 Unicast, Multicast, Anycast](#1231-unicast-multicast-anycast)  
  - [12.3.2 IPv6 Prefix Length](#1232-ipv6-prefix-length)  
  - [12.3.3 Types of IPv6 Unicast Addresses](#1233-types-of-ipv6-unicast-addresses)  
  - [12.3.4 A Note About the Unique Local Address](#1234-a-note-about-the-unique-local-address)  
  - [12.3.5 IPv6 GUA](#1235-ipv6-gua)  
  - [12.3.6 IPv6 GUA Structure](#1236-ipv6-gua-structure)  
  - [12.3.7 IPv6 LLA](#1237-ipv6-lla)  
  - [12.3.8 Check Your Understanding – IPv6 Address Types](#1238-check-your-understanding--ipv6-address-types)  

- [12.4 GUA and LLA Static Configuration](#124-gua-and-lla-static-configuration)  
  - [12.4.1 Static GUA Configuration on a Router](#1241-static-gua-configuration-on-a-router)  
  - [12.4.2 Static GUA Configuration on a Windows Host](#1242-static-gua-configuration-on-a-windows-host)  
  - [12.4.3 Static Configuration of a Link-Local Unicast Address](#1243-static-configuration-of-a-link-local-unicast-address)  
  - [12.4.4 Syntax Checker – GUA and LLA Static Configuration](#1244-syntax-checker--gua-and-lla-static-configuration)  
  - [12.4.5 Packet Tracer – Basic Device Configuration](#1245-packet-tracer--basic-device-configuration)  

- [12.5 Dynamic Addressing for IPv6 GUAs](#125-dynamic-addressing-for-ipv6-guas)  
  - [12.5.1 RS and RA Messages](#1251-rs-and-ra-messages)  
  - [12.5.2 Method 1 – SLAAC](#1252-method-1--slaac)  
  - [12.5.3 Method 2 – SLAAC and Stateless DHCPv6](#1253-method-2--slaac-and-stateless-dhcpv6)  
  - [12.5.4 Method 3 – Stateful DHCPv6](#1254-method-3--stateful-dhcpv6)  
  - [12.5.5 EUI-64 Process vs. Randomly Generated](#1255-eui-64-process-vs-randomly-generated)  
  - [12.5.6 EUI-64 Process](#1256-eui-64-process)  
  - [12.5.7 Randomly Generated Interface IDs](#1257-randomly-generated-interface-ids)  
  - [12.5.8 Check Your Understanding – Dynamic Addressing for IPv6 GUAs](#1258-check-your-understanding--dynamic-addressing-for-ipv6-guas)  

- [12.6 Dynamic Addressing for IPv6 LLAs](#126-dynamic-addressing-for-ipv6-llas)  
  - [12.6.1 Dynamic LLAs](#1261-dynamic-llas)  
  - [12.6.2 Dynamic LLAs on Windows](#1262-dynamic-llas-on-windows)  
  - [12.6.3 Dynamic LLAs on Cisco Routers](#1263-dynamic-llas-on-cisco-routers)  
  - [12.6.4 Verify IPv6 Address Configuration](#1264-verify-ipv6-address-configuration)  
  - [12.6.5 Syntax Checker – Verify IPv6 Address Configuration](#1265-syntax-checker--verify-ipv6-address-configuration)  
  - [12.6.6 Packet Tracer – Configure IPv6 Addressing](#1266-packet-tracer--configure-ipv6-addressing)  

- [12.7 IPv6 Multicast Addresses](#127-ipv6-multicast-addresses)  
  - [12.7.1 Assigned IPv6 Multicast Addresses](#1271-assigned-ipv6-multicast-addresses)  
  - [12.7.2 Well-Known IPv6 Multicast Addresses](#1272-well-known-ipv6-multicast-addresses)  
  - [12.7.3 Solicited-Node IPv6 Multicast Addresses](#1273-solicited-node-ipv6-multicast-addresses)  
  - [12.7.4 Lab – Identify IPv6 Addresses](#1274-lab--identify-ipv6-addresses)  

- [12.8 Subnet an IPv6 Network](#128-subnet-an-ipv6-network)  
  - [12.8.1 Subnet Using the Subnet ID](#1281-subnet-using-the-subnet-id)  
  - [12.8.2 IPv6 Subnetting Example](#1282-ipv6-subnetting-example)  
  - [12.8.3 IPv6 Subnet Allocation](#1283-ipv6-subnet-allocation)  
  - [12.8.4 Router Configured with IPv6 Subnets](#1284-router-configured-with-ipv6-subnets)  
  - [12.8.5 Check Your Understanding – Subnet an IPv6 Network](#1285-check-your-understanding--subnet-an-ipv6-network)  

- [12.9 Module Practice and Quiz](#129-module-practice-and-quiz)  
  - [12.9.1 Packet Tracer – Implement a Subnetted IPv6 Addressing Scheme](#1291-packet-tracer--implement-a-subnetted-ipv6-addressing-scheme)  
  - [12.9.2 Lab – Configure IPv6 Addresses on Network Devices](#1292-lab--configure-ipv6-addresses-on-network-devices)  
  - [12.9.3 What did I learn in this module?](#1293-what-did-i-learn-in-this-module)  
  - [12.9.4 Module Quiz – IPv6 Addressing](#1294-module-quiz--ipv6-addressing)  

---

## Module 12 Overview

> **Goal:** Be comfortable working in dual-stack networks, able to read, configure,
> and troubleshoot IPv6 addressing (GUA + LLA), dynamic address assignment,
> IPv6 multicast, and IPv6 subnetting.

---

## Module Map

| Topic                            | Focus                                                                 |
|----------------------------------|-----------------------------------------------------------------------|
| 12.1 IPv4 Issues                 | Why IPv4 is not enough; motivation for IPv6                          |
| 12.2 IPv6 Address Representation | Hex, compression rules, and notation                                 |
| 12.3 IPv6 Address Types          | Unicast, multicast, anycast; GUA, LLA, ULA                           |
| 12.4 GUA and LLA Static Config   | Manual IPv6 addressing on routers and hosts                          |
| 12.5 Dynamic Addressing for GUAs | SLAAC, stateless & stateful DHCPv6, EUI-64 vs random IIDs            |
| 12.6 Dynamic Addressing for LLAs | How hosts and routers auto-create link-local addresses               |
| 12.7 IPv6 Multicast Addresses    | FF02::/16 groups, solicited-node multicast                           |
| 12.8 Subnet an IPv6 Network      | Using subnet IDs to carve up /48, /56, /64 prefixes                  |
| 12.9 Practice and Quiz           | IPv6 implementation labs and final review                            |

---

## 12.0 Introduction

### 12.0.1 Why should I take this module?

- IPv4 is **running out of addresses**. NAT has delayed the problem but also
  breaks end-to-end connectivity and adds complexity.
- New trends like **mobile broadband** and the **Internet of Things (IoT)**
  create *massive* numbers of devices that all need IP connectivity.
- IPv6 is the long-term answer:
  - 128-bit address space → effectively inexhaustible.
  - Built-in features such as **ICMPv6 Neighbor Discovery**, **SLAAC**, and
    **multicast** improve automation and efficiency.
- Many large ISPs, content providers, and enterprises already run **IPv6-only
  or dual-stack networks**. As a network/security engineer, I must be fluent in
  IPv6 to stay relevant.

**Recruiter angle:**  
> Shows I understand *why* modern networks adopt IPv6, not just how to type
> `ipv6 address` on a router.

---

### 12.0.2 What will I learn in this module?

High-level objectives:

- Explain the **limitations of IPv4** and the global IPv4 exhaustion story.
- Represent IPv6 addresses in **binary / hex / compressed notation**, including
  the two big formatting rules (leading zeros and double colon).
- Compare and identify **IPv6 address types**:
  - Global Unicast (GUA)
  - Link-Local (LLA)
  - Unique Local (ULA)
  - Multicast and Anycast
- **Statically configure** IPv6 GUAs and LLAs on routers and end hosts.
- Explain and configure **dynamic IPv6 addressing**:
  - SLAAC
  - Stateless DHCPv6
  - Stateful DHCPv6
  - Interface IDs via **EUI-64** and via random generation.
- Understand how devices auto-generate LLAs and how to **verify IPv6
  configuration** on Windows and Cisco IOS.
- Recognise and use important **IPv6 multicast groups** like:
  - `FF02::1` (all nodes), `FF02::2` (all routers),
  - solicited-node multicast used by Neighbor Discovery.
- Subnet an IPv6 prefix using the **subnet ID** field and design an addressing
  plan using /64s, /56s, etc.

---

## 12.1 IPv4 Issues

### 12.1.1 Need for IPv6

**Key ideas**

- IPv4 uses **32-bit addresses** → theoretical max ≈ **4.3 billion** unique
  addresses. That seemed huge in the 1980s; today it’s not enough.
- The global address pool is managed by **RIRs (Regional Internet Registries)**.
  Over the last decade, each RIR has **fully allocated its IPv4 blocks** to
  ISPs and organisations. New large IPv4 allocations are essentially gone.
- **Private addressing + NAT** slowed exhaustion:
  - Many private devices share one public IPv4 via port translation.
  - But NAT:
    - breaks true end-to-end connectivity,
    - complicates some protocols (VoIP, IPsec, P2P),
    - adds extra processing and sometimes latency.
- The modern internet is not just PCs and servers:
  - **Smartphones**, tablets, game consoles,
  - **Smart home** and **industrial IoT** (sensors, cameras, appliances, cars),
  - All of them want IP connectivity.
- IPv6 was designed as the **successor to IPv4**, fixing limitations:
  - 128-bit addresses → unimaginably large address space.
  - New features such as:
    - **ICMPv6 / Neighbor Discovery** (replacing ARP and some ICMPv4 roles),
    - **SLAAC** for auto-configuration,
    - Required support for **IPsec** in the base protocol.

**One-liner for interviews**

> *“IPv6 exists because IPv4 ran out of globally routable addresses, and hacks
> like NAT don’t scale cleanly for a world of billions of always-connected
> devices.”*

---

### 12.1.2 IPv4 and IPv6 Coexistence

Real networks won’t flip from IPv4 to IPv6 in one day. For a long time we will
see **both protocols coexisting**. The IETF defined three transition
techniques:

1. **Dual Stack**

   - Devices run **both IPv4 and IPv6** protocol stacks at the same time.
   - Interfaces have both an IPv4 address and an IPv6 address.
   - Traffic uses IPv4 or IPv6 **natively**, depending on the destination.
   - This is the **preferred / native** way to provide IPv6 connectivity.

2. **Tunneling**

   - Used when an IPv6 island must cross an **IPv4-only core**.
   - The IPv6 packet is **encapsulated inside an IPv4 packet** (like a VPN
     tunnel).
   - The tunnel endpoints are dual-stack; the middle of the path only “sees”
     IPv4.

3. **Translation**

   - Used when an IPv6-only host must talk to an **IPv4-only host**.
   - A device (e.g. **NAT64** translator) converts:
     - IPv6 → IPv4 in one direction,
     - IPv4 → IPv6 in the other.
   - Conceptually similar to NAT for IPv4, but between *different protocols*.

> **Design note (from NetAcad):** tunneling and translation are primarily
> **transition mechanisms** on the way to **native IPv6**. The long-term goal is
> dual-stack or IPv6-only, not to keep complex transition tricks forever.

---

### 12.1.3 Check Your Understanding – IPv4 Issues

Quick navigation:

- [Q1 – Main driver for moving to IPv6](#q1--main-driver-for-moving-to-ipv6)
- [Q2 – RIR IPv4 exhaustion statement](#q2--rir-ipv4-exhaustion-statement)
- [Q3 – Which technique uses native IPv6?](#q3--which-technique-uses-native-ipv6)

---

#### Q1 – Main driver for moving to IPv6

**Exam question**

> What is the most important motivating factor for moving to IPv6?

Options:

- Better performance with IPv6  
- IPv6 addresses that are easier to work with  
- Better security with IPv6  
- **Depletion of IPv4 addresses ✅**

**Why this is correct**

- IPv6 does bring some side benefits (cleaner header, better support for
  extension headers, etc.), but **the core reason** it was created and
  standardised is **address exhaustion**.
- All five RIRs have effectively **run out of IPv4 space** to allocate to ISPs.
  Without a new protocol, the internet can’t keep growing.
- Performance and security can be improved in both IPv4 and IPv6 through other
  technologies; they were **not** the main drivers for inventing IPv6.

**Skill demonstrated (for recruiters)**

- Understands the **business / global context** for IPv6 deployment, not just
  the commands.

---

#### Q2 – RIR IPv4 exhaustion statement

**Exam question**

> True or False: **4 out of 5 RIRs** no longer have enough IPv4 addresses to
> allocate to customers on a regular basis.

Options:

- False  
- True  

**Correct answer**

- **False ✅**

**Why this is correct**

- The material states that **all five RIRs** have fully allocated their IPv4
  address space – not just 4 out of 5.
- So the statement “4 out of 5” is inaccurate → therefore **False**.

**Skill demonstrated**

- Careful reading of wording like “some”, “most”, “all”, which often appears in
  exam questions and technical documentation.

---

#### Q3 – Which technique uses native IPv6?

**Exam question**

> Which of the following techniques use **native IPv6 connectivity**?

Options:

- Translation  
- All of the above  
- Tunneling  
- **Dual stack ✅**

**Why this is correct**

- **Dual stack** means the network and devices natively support **both IPv4 and
  IPv6**. Packets are sent as real IPv6 packets (no encapsulation or protocol
  conversion) → this is **native IPv6 connectivity**.
- **Tunneling** encapsulates IPv6 inside IPv4; the IPv6 packets are *not* being
  forwarded natively across the whole path.
- **Translation** (e.g. NAT64) actually **changes** packets between IPv4 and
  IPv6, which is the opposite of native end-to-end IPv6.

**Skill demonstrated**

- Correctly distinguishes between **dual-stack, tunneling, and translation**,
  and knows which one preserves **native IPv6**.

---

<!--
Next sections (12.2–12.9) will follow the same style: concise theory notes +
Q&A with explanations for each “Check Your Understanding” / quiz block.
-->

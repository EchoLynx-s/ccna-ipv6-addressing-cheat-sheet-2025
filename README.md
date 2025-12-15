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
- How IPv6 **multicast** is used (`ff02::1`, `ff02::2`, solicited-node, etc.).
- How to **subnet an IPv6 /64 or larger prefix** using subnet IDs.

> **At a glance – what this shows I can do**
> - Design IPv6 addressing plans with /64 LANs and subnet IDs.
> - Configure IPv6 GUAs + LLAs on Cisco routers and Windows hosts.
> - Explain and troubleshoot SLAAC vs stateless vs stateful DHCPv6.
> - Compress and expand IPv6 addresses confidently (rules 1 & 2).
> - Use IPv6 link-local and multicast (`ff02::1`, `ff02::2`) in real topologies.

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
  - [12.1.3 Check Your Understanding – IPv4 Issues](#1213-check-your-understanding-ipv4-issues)  

- [12.2 IPv6 Address Representation](#122-ipv6-address-representation)  
  - [12.2.1 IPv6 Addressing Formats](#1221-ipv6-addressing-formats)  
  - [12.2.2 Rule 1 – Omit Leading Zeros](#1222-rule-1-omit-leading-zeros)  
  - [12.2.3 Rule 2 – Double Colon](#1223-rule-2-double-colon)  
  - [12.2.4 Check Your Understanding – IPv6 Address Representation](#1224-check-your-understanding-ipv6-address-representation)  

- [12.3 IPv6 Address Types](#123-ipv6-address-types)  
  - [12.3.1 Unicast, Multicast, Anycast](#1231-unicast-multicast-anycast)  
  - [12.3.2 IPv6 Prefix Length](#1232-ipv6-prefix-length)  
  - [12.3.3 Types of IPv6 Unicast Addresses](#1233-types-of-ipv6-unicast-addresses)  
  - [12.3.4 A Note About the Unique Local Address](#1234-a-note-about-the-unique-local-address)  
  - [12.3.5 IPv6 GUA](#1235-ipv6-gua)  
  - [12.3.6 IPv6 GUA Structure](#1236-ipv6-gua-structure)  
  - [12.3.7 IPv6 LLA](#1237-ipv6-lla)  
  - [12.3.8 Check Your Understanding – IPv6 Address Types](#1238-check-your-understanding-ipv6-address-types)  

- [12.4 GUA and LLA Static Configuration](#124-gua-and-lla-static-configuration)  
  - [12.4.1 Static GUA Configuration on a Router](#1241-static-gua-configuration-on-a-router)  
  - [12.4.2 Static GUA Configuration on a Windows Host](#1242-static-gua-configuration-on-a-windows-host)  
  - [12.4.3 Static Configuration of a Link-Local Unicast Address](#1243-static-configuration-of-a-link-local-unicast-address)  
  - [12.4.4 Syntax Checker – GUA and LLA Static Configuration](#1244-syntax-checker-gua-and-lla-static-configuration)  
  - [12.4.5 Packet Tracer – Basic Device Configuration](#1245-packet-tracer-basic-device-configuration)  

- [12.5 Dynamic Addressing for IPv6 GUAs](#125-dynamic-addressing-for-ipv6-guas)  
  - [12.5.1 RS and RA Messages](#1251-rs-and-ra-messages)  
  - [12.5.2 Method 1 – SLAAC](#1252-method-1-slaac)  
  - [12.5.3 Method 2 – SLAAC and Stateless DHCPv6](#1253-method-2-slaac-and-stateless-dhcpv6)  
  - [12.5.4 Method 3 – Stateful DHCPv6](#1254-method-3-stateful-dhcpv6)  
  - [12.5.5 EUI-64 Process vs. Randomly Generated Interface IDs](#1255-eui-64-process-vs-randomly-generated-interface-ids)  
  - [12.5.6 EUI-64 Process](#1256-eui-64-process)  
  - [12.5.7 Randomly Generated Interface IDs](#1257-randomly-generated-interface-ids)  
  - [12.5.8 Check Your Understanding – Dynamic Addressing for IPv6 GUAs](#1258-check-your-understanding-dynamic-addressing-for-ipv6-guas)  

- [12.6 Dynamic Addressing for IPv6 LLAs](#126-dynamic-addressing-for-ipv6-llas)  
  - [12.6.1 Dynamic LLAs](#1261-dynamic-llas)  
  - [12.6.2 Dynamic LLAs on Windows](#1262-dynamic-llas-on-windows)  
  - [12.6.3 Dynamic LLAs on Cisco Routers](#1263-dynamic-llas-on-cisco-routers)  
  - [12.6.4 Verify IPv6 Address Configuration](#1264-verify-ipv6-address-configuration)  
  - [12.6.5 Syntax Checker – Verify IPv6 Address Configuration](#1265-syntax-checker-verify-ipv6-address-configuration)  
  - [12.6.6 Packet Tracer – Configure IPv6 Addressing](#1266-packet-tracer-configure-ipv6-addressing)  

- [12.7 IPv6 Multicast Addresses](#127-ipv6-multicast-addresses)  
  - [12.7.1 Assigned IPv6 Multicast Addresses](#1271-assigned-ipv6-multicast-addresses)  
  - [12.7.2 Well-Known IPv6 Multicast Addresses](#1272-well-known-ipv6-multicast-addresses)  
  - [12.7.3 Solicited-Node IPv6 Multicast Addresses](#1273-solicited-node-ipv6-multicast-addresses)  
  - [12.7.4 Lab – Identify IPv6 Addresses](#1274-lab-identify-ipv6-addresses)  

- [12.8 Subnet an IPv6 Network](#128-subnet-an-ipv6-network)  
  - [12.8.1 Subnet Using the Subnet ID](#1281-subnet-using-the-subnet-id)  
  - [12.8.2 IPv6 Subnetting Example](#1282-ipv6-subnetting-example)  
  - [12.8.3 IPv6 Subnet Allocation](#1283-ipv6-subnet-allocation)  
  - [12.8.4 Router Configured with IPv6 Subnets](#1284-router-configured-with-ipv6-subnets)  
  - [12.8.5 Check Your Understanding – Subnet an IPv6 Network](#1285-check-your-understanding-subnet-an-ipv6-network)  

- [12.9 Module Practice and Quiz](#129-module-practice-and-quiz)  
  - [12.9.1 Packet Tracer – Implement a Subnetted IPv6 Addressing Scheme](#1291-packet-tracer-implement-a-subnetted-ipv6-addressing-scheme)  
  - [12.9.2 Lab – Configure IPv6 Addresses on Network Devices](#1292-lab-configure-ipv6-addresses-on-network-devices)  
  - [12.9.3 What did I learn in this module?](#1293-what-did-i-learn-in-this-module)  
  - [12.9.4 Module Quiz – IPv6 Addressing](#1294-module-quiz-ipv6-addressing)  

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
| 12.7 IPv6 Multicast Addresses    | ff00::/8 groups, solicited-node multicast                            |
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
  - `ff02::1` (all nodes), `ff02::2` (all routers),
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

> **Design note:** tunneling and translation are primarily
> **transition mechanisms** on the way to **native IPv6**. The long-term goal is
> dual-stack or IPv6-only, not to keep complex transition tricks forever.

---

### 12.1.3 Check Your Understanding – IPv4 Issues

Quick navigation:

- [Q1 – Main driver for moving to IPv6](#q1-main-driver-for-moving-to-ipv6)
- [Q2 – RIR IPv4 exhaustion statement](#q2-rir-ipv4-exhaustion-statement)
- [Q3 – Which technique uses native IPv6?](#q3-which-technique-uses-native-ipv6)

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

---

## 12.2 IPv6 Address Representation  

> **Big idea:** IPv6 addresses are 128‑bit hex strings. We almost never write the full 32 hex digits because there are rules to shorten them safely.  

### 12.2.1 IPv6 Addressing Formats  

- IPv6 address length: **128 bits**.  
- Written as **8 groups of 16 bits** (hextets), separated by colons (`:`).  
- Each hextet = **4 hexadecimal digits** → 16 bits.  
- Hex digits are **0–9** and **a–f** (not case‑sensitive).  

**Example – preferred (full) format**  

```text
2001:0db8:0000:0000:0000:0000:0000:0200
```

Terminology:  

- **Hextet** – informal term for a 16‑bit chunk of an IPv6 address (4 hex digits).  
- **Preferred format** – full, unshortened 8×4‑hex notation.  
- We shorten it using **Rule 1** and **Rule 2**.  

---

### 12.2.2 Rule 1 – Omit Leading Zeros  

> **Rule 1:** Within any hextet, you may **omit one or more leading `0`s**.  
> You **must not** omit trailing zeros, or mix up the number of hex digits.  

Examples (single hextet):  

- `01ab` → `1ab`  
- `09f0` → `9f0`  
- `0a00` → `a00`  
- `00ab` → `ab`  

This rule applies **independently per hextet**.  

**Whole‑address examples**  

Preferred vs “no leading 0s” (short form):  

| Preferred format                              | Omit leading zeros              |
|----------------------------------------------|---------------------------------|
| `2001:0db8:0000:1111:0000:0000:0000:0200`    | `2001:db8:0:1111:0:0:0:200`     |
| `2001:0db8:0000:00a3:ab00:0ab0:000b:1234`    | `2001:db8:0:a3:ab00:ab0:b:1234` |
| `2001:0db8:000a:0001:0c01:90ff:fe90:0001`    | `2001:db8:a:1:c01:90ff:fe90:1`  |
| `fe80:0000:0000:0000:0123:4567:89ab:cdef`    | `fe80:0:0:0:123:4567:89ab:cdef` |
| `fe80:0000:0000:0000:0000:0000:0000:0001`    | `fe80:0:0:0:0:0:0:1`            |
| `0000:0000:0000:0000:0000:0000:0000:0000`    | `0:0:0:0:0:0:0:0`               |

Key points for Rule 1:  

- You always keep **between 1 and 4 hex digits per hextet**.  
- This rule alone **does not** change the number of hextets (still 8).  

---

### 12.2.3 Rule 2 – Double Colon  

> **Rule 2:** You may replace **one single, contiguous run of all‑zero hextets** with the double colon `::`.  

Guidelines:  

1. `::` can represent **one or more** `0000` hextets, but **only once per address**.  
2. Use it on the **longest** sequence of all‑zero hextets. If there’s a tie, it’s your choice, but RFC practice is to use the **leftmost** longest run.  
3. Combining Rule 1 and Rule 2 gives the **compressed** form.  

**Incorrect example from the course**  

- Wrong: `2001:db8::abcd::1234` (two `::` → ambiguous).  

Possible (different) expansions would be:  

- `2001:db8:0000:0000:abcd:0000:0000:1234`  
- `2001:db8:0000:abcd:0000:0000:0000:1234`  
- etc. → more than one answer ⇒ **not allowed**.  

**Correct compression examples**  

| Type                | Format example                                                  |
|---------------------|-----------------------------------------------------------------|
| Preferred           | `2001:0db8:0000:1111:0000:0000:0000:0200`                       |
| Compressed/spaces   | `2001:db8:0:1111:0:0:0:200`                                     |
| Compressed (final)  | `2001:db8:0:1111::200`                                          |
| Preferred           | `fe80:0000:0000:0000:0123:4567:89ab:cdef`                       |
| Compressed/spaces   | `fe80:0:0:0:123:4567:89ab:cdef`                                 |
| Compressed (final)  | `fe80::123:4567:89ab:cdef`                                      |
| Preferred           | `fe80:0000:0000:0000:0000:0000:0000:0001`                       |
| Compressed/spaces   | `fe80:0:0:0:0:0:0:1`                                            |
| Compressed (final)  | `fe80::1`                                                       |
| Preferred           | `0000:0000:0000:0000:0000:0000:0000:0001`                       |
| Compressed (final)  | `::1` (loopback)                                                |
| Preferred           | `0000:0000:0000:0000:0000:0000:0000:0000`                       |
| Compressed (final)  | `::` (unspecified address)                                      |

**Rule‑of‑thumb summary**  

- Apply **Rule 1** first (drop leading zeros in each hextet).  
- Then apply **Rule 2** (replace the single longest run of `0` hextets with `::`).  
- You may never use more than **one** `::` in any IPv6 address.  

---

### 12.2.4 Check Your Understanding – IPv6 Address Representation  

> These are practice conversions based on the 12.2.4 activity.  
> Answers are written in lowercase, as NetAcad expects.

#### Example 1  

Preferred:  

```text
fe80:0000:0000:0000:0000:0000:0101:1111
```

- **Omit leading zeros:** `fe80:0:0:0:0:0:101:1111`  
- **Compressed format:** `fe80::101:1111`  

#### Example 2  

Preferred:  

```text
2001:0db8:0000:0000:0000:abcd:0000:0001
```

- **Omit leading zeros:** `2001:db8:0:0:0:abcd:0:1`  
- **Compressed format:** `2001:db8::abcd:0:1` (leftmost longest zero‑run)  

#### Example 3  

Preferred:  

```text
0000:0000:0000:0000:0000:0000:0000:0000
```

- **Omit leading zeros:** `0:0:0:0:0:0:0:0`  
- **Compressed format:** `::`  

> **Exam skill:** For any given IPv6 address, be able to:  
> 1. Write the full preferred version (expand).  
> 2. Write the shortest valid compressed version (shrink).  

---

## 12.3 IPv6 Address Types  

> **Big idea:** IPv6 improves addressing by defining multiple unicast types, rich multicast, and anycast. IPv6 has **no broadcast** at all.  

### 12.3.1 Unicast, Multicast, Anycast  

Three broad categories of IPv6 addresses:  

- **Unicast**  
  - Identifies **a single interface**.  
  - Packets are delivered to **one** IPv6-enabled device.  
  - Examples: GUA, LLA, ULA, loopback, etc.  

- **Multicast**  
  - Identifies **a group of devices**.  
  - Packets sent to a multicast address are delivered to **all interfaces** that joined that group.  
  - Replaces IPv4 broadcast functionality.  

- **Anycast**  
  - A unicast address that is **assigned to multiple interfaces** (usually on different routers).  
  - Packets are delivered to the **nearest** device (in routing terms).  
  - Anycast operation is **beyond the scope** of this CCNA module but good to know conceptually.  

**Important:** IPv6 has **no broadcast address**. Instead, it uses **IPv6 all‑nodes multicast** (e.g. `ff02::1`) to reach all nodes on a link.  

---

### 12.3.2 IPv6 Prefix Length  

- IPv6 uses **prefix length notation** (`/n`) instead of dotted‑decimal masks.  
- The prefix indicates the **network portion**; the remaining bits are the **interface ID** (host part).  
- Common LAN prefix: **`/64`**.  

Example:  

```text
2001:db8:a::/64
```

- First 64 bits (`2001:0db8:000a:0000`) → **prefix**.  
- Last 64 bits (`0000:0000:0000:0000`) → **interface ID**.  

Why `/64` is recommended:  

- SLAAC (Stateless Address Autoconfiguration) assumes **64‑bit interface IDs**.  
- `/64` makes subnetting in IPv6 simple and consistent.  

---

### 12.3.3 Types of IPv6 Unicast Addresses  

An IPv6 **unicast address** uniquely identifies an interface. A packet sent to a unicast address is received by that specific interface.  

Main IPv6 unicast types:  

1. **Global Unicast Address (GUA)**  
   - Equivalent to IPv4 **public** addresses.  
   - Globally unique, Internet‑routable.  
   - Assigned statically or dynamically (SLAAC/DHCPv6).  
   - Typical prefix: `2000::/3` (addresses starting with `2` or `3`).  

2. **Link‑local Address (LLA)**  
   - Required on every IPv6‑enabled interface.  
   - Used to communicate **on the local link only** (non‑routable).  
   - Always in `fe80::/10` (e.g. `fe80::1`, `fe80::abcd:1234`).  
   - Routers never forward packets with LLA as source or destination.  

3. **Loopback Address**  
   - Used to test the local TCP/IP stack.  
   - Single address: **`::1/128`**.  

4. **Unspecified Address**  
   - All zeros: **`::/128`**.  
   - Used by a host when it does not yet know its own address (e.g. as a source during DHCPv6).  
   - Never appears as a destination.  

5. **Unique Local Address (ULA)**  
   - Like IPv4 private addresses (for internal use, not globally routed).  
   - Range: **`fc00::/7` to `fdff::/7`**.  
   - Commonly written as `fdxx:xxxx:...`.  

Most IPv6 interfaces will have **at least two unicast addresses**: a **GUA** + a **link‑local**.  

---

### 12.3.4 A Note About the Unique Local Address  

Unique Local Addresses (ULAs):  

- Range: **`fc00::/7` to `fdff::/7`**.  
- Intended for:  
  - Local addressing **within a site** or between a small number of sites.  
  - Devices that **never need global Internet access** (e.g. internal servers, printers).  
- Properties vs IPv4 private addresses (RFC 1918):  
  - Both are for non‑public addressing.  
  - ULAs are **not globally routed** or translated to GUAs.  
  - ULAs are designed to be globally unique if generated properly (using a random Global ID).  

---

### 12.3.5 IPv6 GUA  

Global Unicast Addresses (GUAs):  

- Globally unique, Internet‑routable IPv6 addresses.  
- Allocated by IANA → RIRs → ISPs → organizations.  
- Current GUA allocation range: addresses with the first three bits `001`, i.e. **`2000::/3`**.  

That means:  

- Smallest current GUA block: `2000::`  
- Largest within that /3: `3fff:ffff:ffff:ffff:ffff:ffff:ffff:ffff`  

A typical enterprise allocation example:  

- Organization receives `2001:db8:acad::/48` as its **global routing prefix**.  
- It can then subnet further using the **Subnet ID** field.  

---

### 12.3.6 IPv6 GUA Structure  

Typical structure (for a `/64` prefix):  

```text
|<------ 48 bits ------>|<-16->|<------------ 64 bits ------------>|
+-----------------------+------+-----------------------------------+
| Global Routing Prefix | Subn |          Interface ID             |
+-----------------------+------+-----------------------------------+
```

- **Global Routing Prefix**  
  - Assigned by the ISP or provider.  
  - Identifies the **site/network** on the global Internet.  
  - Example: `2001:db8:acad::/48` – here `2001:db8:acad` is the global routing prefix.  

- **Subnet ID**  
  - Used **inside the organization** to identify internal subnets.  
  - With a `/48` global prefix and `/64` per subnet, there are **16 bits** for the Subnet ID.  
  - That gives `2^16 = 65,536` subnets, each with `2^64` addresses.  

- **Interface ID**  
  - The remaining **64 bits**, equivalent to the host portion in IPv4.  
  - Can be generated via **EUI‑64** or a **random** 64‑bit value.  
  - Recommended to keep `/64` interface IDs for SLAAC compatibility.  

---

### 12.3.7 IPv6 LLA  

Link‑local addresses (LLAs):  

- Address range: **`fe80::/10`** (from `fe80::` to `febf:ffff:ffff:ffff:ffff:ffff:ffff:ffff`).  
- Purpose: communication **only on the local link** (local network segment).  
- Every IPv6-enabled interface **must have an LLA**.  

How LLAs are used:  

- Host ↔ default‑gateway router communication on the same link.  
- Routing protocol neighbor communication between routers (e.g. OSPFv3, EIGRP for IPv6).  

LLAs can be:  

- **Statically configured**, e.g.:  

  ```text
  interface g0/0
   ipv6 address fe80::1:1 link-local
  ```

- **Dynamically created** by the device:  
  - Device takes its MAC or a random value and builds a 64‑bit interface ID in the `fe80::/10` range.  

Important behaviour:  

- Packets with source or destination LLA are **never forwarded** by routers beyond that link.  
- Typically, hosts use the **router’s LLA** (not its GUA) as their default gateway address.  

---

### 12.3.8 Check Your Understanding – IPv6 Address Types  

> These are the key “Check Your Understanding” ideas from 12.3.  

#### Q1 – Recommended Prefix Length for Most IPv6 Subnets  

**Question:**  
What is the recommended prefix length for most IPv6 subnets?  

**Answer:** ✅ **`/64`**  

**Reasoning:** SLAAC and most modern designs expect **64‑bit interface IDs**, which implies a `/64` prefix. This simplifies address autoconfiguration and subnetting.  

---  

#### Q2 – Which Part of a GUA Is Assigned by the ISP?  

**Question:**  
Which part of a Global Unicast Address (GUA) is assigned by the ISP?  

Options (from the activity):  

- Global routing prefix  
- Global routing prefix and subnet ID  
- RIR prefix  
- Prefix  

**Answer:** ✅ **Global routing prefix**  

**Reasoning:**  

- IANA allocates large IPv6 blocks to **RIRs**.  
- RIRs allocate to **ISPs**.  
- ISP then assigns a **global routing prefix** (e.g. `/48` or `/56`) to the customer.  
- The **customer** uses the **Subnet ID** bits under that prefix to create internal subnets.  

---

## 12.4 GUA and LLA Static Configuration

### 12.4.1 Static GUA Configuration on a Router

**Concepts**

- IPv6 **Global Unicast Addresses (GUAs)** are the IPv6 version of public IPv4 addresses:
  - Globally unique and routable on the internet.
  - Typically start with `2` or `3` (e.g. `2001:db8::/32` for documentation).
- In IOS, IPv4 vs IPv6 interface commands differ only slightly:  
  - IPv4: `ip address <ipv4-address> <mask>`  
  - IPv6: `ipv6 address <ipv6-address>/<prefix-length>`

**Key points**

- You can have **multiple IPv6 addresses per interface** (e.g. one GUA + one LLA).
- No space between address and prefix length.
- After configuring IPv6 addresses you must still use `no shutdown` to enable the interface.

**Example topology GUAs**

- `2001:db8:acad:1::/64` – LAN 1 (PC1)  
- `2001:db8:acad:2::/64` – LAN 2 (PC2)  
- `2001:db8:acad:3::/64` – WAN / serial link  

**Example IOS config – GUAs only**

```text
R1(config)# interface g0/0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface g0/0/1
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface s0/1/0
R1(config-if)# ipv6 address 2001:db8:acad:3::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
```

**Interview sound-bite**

> “On Cisco IOS, IPv6 GUAs are configured per interface with  
> `ipv6 address <GUA>/<prefix>`, and each interface can hold several IPv6
> addresses (GUA + LLA) at the same time.”

---

### 12.4.2 Static GUA Configuration on a Windows Host

**Concepts**

- Manually configuring IPv6 on a host is similar to IPv4:
  - IPv6 address + prefix length (instead of dotted mask).
  - Default gateway address (usually the **router’s LLA**).
- Static addressing **does not scale** in large networks, but is useful for:
  - Labs
  - Servers that require fixed addresses
  - Troubleshooting

**Example PC1 config (from the IPv6 properties dialog)**

- **IPv6 address:** `2001:db8:acad:1::10`  
- **Subnet prefix length:** `64`  
- **Default gateway:** `2001:db8:acad:1::1` (or the router’s `fe80::1:1` LLA)  

**Key takeaways**

- Windows lets you choose either:
  - *Obtain an IPv6 address automatically* (SLAAC/DHCPv6), or  
  - *Use the following IPv6 address* (static).
- In real networks, hosts usually obtain GUAs dynamically (**SLAAC** or **DHCPv6**).

---

### 12.4.3 Static Configuration of a Link-Local Unicast Address

**Concepts**

- Every IPv6-enabled interface **must** have a **Link-Local Address (LLA)**:
  - Scope: only the **local link** (LAN segment).  
  - Prefix: `fe80::/10` (e.g. `fe80::1:1`).  
  - Not routable beyond the local link.
- Routers commonly use LLAs as:
  - Default gateway addresses for hosts.
  - Source/destination for routing protocol messages (OSPFv3, EIGRP for IPv6, etc.).

**IOS command pattern**

```text
ipv6 address <link-local-address> link-local
```

> The keyword `link-local` is mandatory when the address starts with `fe80::`.

**Example topology LLAs**

- R1 g0/0/0 – `fe80::1:1`  
- R1 g0/0/1 – `fe80::2:1`  
- R1 s0/1/0 – `fe80::3:1`  

**Example IOS config – LLAs only**

```text
R1(config)# interface g0/0/0
R1(config-if)# ipv6 address fe80::1:1 link-local
R1(config-if)# exit

R1(config)# interface g0/0/1
R1(config-if)# ipv6 address fe80::2:1 link-local
R1(config-if)# exit

R1(config)# interface s0/1/0
R1(config-if)# ipv6 address fe80::3:1 link-local
R1(config-if)# exit
```

**Best practice**

- Use **easy-to-recognise LLAs** on routers (for humans), not random ones:
  - e.g. `fe80::1:1`, `fe80::2:1`, `fe80::3:1` per interface.
- Only needs to be **unique on the link**, not globally unique.

---

### 12.4.4 Syntax Checker – GUA and LLA Static Configuration

This section walks through configuring **both** LLAs and GUAs on all R1 interfaces.

**Task summary**

For each interface:

1. Enter interface config mode.  
2. Configure the LLA with the `link-local` keyword.  
3. Configure the GUA with prefix `/64`.  
4. `no shutdown` to bring the interface up.  
5. `exit` back to global config.

**Final working configuration (from the activity)**

```text
! G0/0/0
R1(config)# interface g0/0/0
R1(config-if)# ipv6 address fe80::1:1 link-local
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
R1(config-if)# exit

! G0/0/1
R1(config)# interface g0/0/1
R1(config-if)# ipv6 address fe80::2:1 link-local
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# no shutdown
R1(config-if)# exit

! Serial 0/1/0
R1(config)# interface s0/1/0
R1(config-if)# ipv6 address fe80::3:1 link-local
R1(config-if)# ipv6 address 2001:db8:acad:3::1/64
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)#  ! end of IPv6 interface config
```

**What this proves (for recruiters)**

- I can configure **dual IPv6 addresses per interface** (LLA + GUA).  
- I understand which commands are needed to actually **activate** the interface
  and make the addresses usable.

---

### 12.4.5 Packet Tracer – Basic Device Configuration

**Activity goal**

- Configure:
  - Router hostname, security (passwords, banner), and **IPv4 + IPv6** addresses.
  - Switch basic settings and management IP (VLAN 1).
  - PC NIC IPv4 and IPv6 addresses and default gateways.
- Verify **end-to-end IPv4 and IPv6 connectivity** between all devices using `ping`.

**What I practise here**

- Filling an addressing table for multiple topologies.
- Applying a consistent **baseline config** on routers/switches (hostnames, passwords, banners).
- Assigning both IPv4 and IPv6 addresses on:
  - Router interfaces (`g0/0`, `g0/1`, `s0/1/0`, etc.).
  - Switch VLAN 1 SVI.
  - PC NICs.
- Testing the network and troubleshooting until **all devices can reach each other** with both protocols.

---

## 12.5 Dynamic Addressing for IPv6 GUAs

### 12.5.1 RS and RA Messages

**ICMPv6 RS (Router Solicitation)**

- Sent **by hosts** to the *all‑routers* multicast address (`ff02::2`).
- Purpose: “Hi routers, I need addressing information.”
- Triggers routers to reply sooner with an RA instead of waiting for the periodic timer.

**ICMPv6 RA (Router Advertisement)**

- Sent **by IPv6 routers** (typically every ~200 seconds) out router interfaces to the *all‑nodes* multicast address (`ff02::1`).
- Can also be sent as a unicast reply to a received RS.
- To make a router send RAs, IPv6 routing must be enabled, e.g.:

  ```text
  R1(config)# ipv6 unicast-routing
  ```

- An RA tells a host **how to get a GUA**. It can include:
  - **Network prefix and prefix length** (e.g. `2001:db8:acad:1::/64`)  
  - **Default gateway address** – usually the router’s IPv6 LLA on that link  
  - **DNS server addresses and domain name** (if configured)  

**Three RA “methods” (how a host should behave):**

1. **Method 1 – SLAAC only**
   - Message meaning: “You have everything you need right here: prefix, prefix‑length, default gateway. Build your own IPv6 GUA.”
2. **Method 2 – SLAAC + Stateless DHCPv6**
   - Message meaning: “Use SLAAC for your GUA and default gateway, but ask a DHCPv6 server for *extra info* (DNS, domain name, etc.).”
3. **Method 3 – Stateful DHCPv6 (no SLAAC)**
   - Message meaning: “Ask a stateful DHCPv6 server for your IPv6 address and other info. I’ll still tell you the default gateway via RA.”

---

### 12.5.2 Method 1 – SLAAC

**SLAAC = Stateless Address Autoconfiguration.**

- Host receives RA with:
  - **Prefix** (e.g. `2001:db8:acad:1::/64`)
  - **Prefix length** (`/64`)
  - **Default gateway** (router’s LLA, e.g. `fe80::1`)
- Host **creates its own Interface ID**:
  - Using **EUI‑64** OR
  - A **random 64‑bit number** (privacy extension).
- Final GUA example:

  ```text
  2001:db8:acad:1:fc99:47ff:fe75:cee0/64
  ```

- No DHCPv6 server needed; there is no central lease database (stateless).

---

### 12.5.3 Method 2 – SLAAC and Stateless DHCPv6

- Router’s RA still provides:
  - **Prefix + prefix length**
  - **Default gateway** (router LLA)
- Host uses **SLAAC** to create its IPv6 GUA.
- RA tells the host: “You still need more information from DHCPv6.”
- Host then contacts a **stateless DHCPv6 server**, which provides:
  - **DNS server address(es)**
  - **Domain name** and similar options
- The **GUA is *not* allocated by DHCPv6** – only additional parameters are.

---

### 12.5.4 Method 3 – Stateful DHCPv6

- Similar idea to **DHCP for IPv4**.
- RA tells the host to use **stateful DHCPv6**:
  - “I’m your default gateway, but get your IPv6 address and other info from the DHCPv6 server.”
- Host sends a **DHCPv6 Solicit** to find a server.
- Stateful DHCPv6 server:
  - Allocates the **GUA** and keeps a **list of which host has which IPv6 address**.
  - Also supplies **DNS servers, domain, etc.**
- The **default gateway** address still comes from the **RA**, not from DHCPv6.

---

### 12.5.5 EUI‑64 Process vs Randomly Generated Interface IDs

When a host uses SLAAC (Method 1 or 2), it must generate the **Interface ID** (last 64 bits). Two options:

#### Option 1 – EUI‑64 (based on MAC address)

- Start with the **48‑bit MAC address** (e.g. `fc:99:47:75:ce:e0`).
- Split into two 24‑bit halves (OUI and device ID).
- Insert the fixed 16‑bit value **`fffe`** in the middle → now 64 bits.
- **Flip the 7th bit** (U/L bit) of the first byte:
  - If it was 0 (universally administered), set to 1 (locally administered).
- Example result: Interface ID `fc99:47ff:fe75:cee0`.
- Combine with prefix from RA → full GUA:

  ```text
  2001:db8:acad:1:fc99:47ff:fe75:cee0/64
  ```

**Pros:**  
- Direct relationship between MAC address and IPv6 Interface ID; easy for admins to map addresses to devices.

**Cons:**  
- Privacy concern: IPv6 address can effectively reveal the device’s **MAC**, making long‑term tracking easier.

#### Option 2 – Random 64‑bit Interface ID (Privacy Extensions)

- Host generates a **random 64‑bit value** instead of using MAC.
- Example Interface ID: `50a5:8a35:a5bb:66e1`

  ```text
  2001:db8:acad:1:50a5:8a35:a5bb:66e1/64
  ```

- Helps prevent tracking of a host based solely on its MAC‑derived Interface ID.
- Modern OSes (Windows Vista and later, many Linux/macOS) **use random IIDs by default**.

**Duplicate Address Detection (DAD)**

- After forming a GUA, host must ensure it is **unique on the link**.
- Sends an ICMPv6 **Neighbor Solicitation** for its own address:
  - If no reply → address is unique and can be used.
  - If reply → conflict detected; host must choose another Interface ID.

---

### 12.5.6 EUI‑64 Process

This subsection is a step-by-step, exam-style view of the EUI‑64 process.

Given MAC: `fc:99:47:75:ce:e0`.

1. Split into two halves:

   ```text
   fc:99:47   75:ce:e0
   ```

2. Insert `ff:fe` in the middle:

   ```text
   fc:99:47:ff:fe:75:ce:e0
   ```

3. Flip the 7th bit of the first byte (`fc` = `11111100` in binary):

   - 7th bit from left is currently `1` → flip to `0`.  
   - New first byte becomes `fe` (`11111110`).

   Resulting Interface ID:

   ```text
   fe:99:47:ff:fe:75:ce:e0  ->  fe99:47ff:fe75:cee0
   ```

4. Combine with prefix, e.g. `2001:db8:acad:1::/64`:

   ```text
   2001:db8:acad:1:fe99:47ff:fe75:cee0/64
   ```

**Exam tip:** you don’t usually have to do all the binary, just remember:

- Split MAC in half, insert `fffe` in the middle,
- Flip the 7th bit of the first byte.

---

### 12.5.7 Randomly Generated Interface IDs

Key points:

- Random IIDs improve **privacy** by making it harder to track a device over time.
- Often combined with **temporary addresses** that rotate periodically.
- In Wireshark / logs, you will see GUAs whose interface IDs look random, not based on MAC.

For security work, knowing this explains why:

- You might not be able to infer MAC vendor from an IPv6 address.
- The same host may appear with different IPv6 addresses over time.

---

### 12.5.8 Check Your Understanding – Dynamic Addressing for IPv6 GUAs

> **Question 1** – True or False?  
> RA messages are sent to all IPv6 routers by hosts requesting addressing information.

- **Correct answer:** `False`  
  - **RS** (Router Solicitation) messages are sent by **hosts** to **routers** to request addressing info.  
  - **RA** (Router Advertisement) messages are sent by **routers** to **hosts** with the addressing details.

(Other quiz questions will be added here as I encounter them.)

---

### Quick Comparison Table – IPv6 GUA Methods

| Method | Who creates the GUA?        | Where does host get prefix + default gateway? | Extra info source (DNS etc.) | Central lease DB? |
|-------|------------------------------|-----------------------------------------------|------------------------------|-------------------|
| 1 – SLAAC | Host (EUI‑64 or random IID) | RA (router)                                   | None                         | No (stateless)    |
| 2 – SLAAC + Stateless DHCPv6 | Host (EUI‑64 or random IID) | RA (router)                                   | Stateless DHCPv6 server      | No (stateless)    |
| 3 – Stateful DHCPv6 | DHCPv6 server                | RA (router) – default gateway only            | Same stateful DHCPv6 server  | Yes (stateful)    |

---

## 12.6 Dynamic Addressing for IPv6 LLAs  

> **Big idea:** Every IPv6 interface *must* have a **link-local address (LLA)**.  
> If you don’t configure one manually, the OS/router will **auto-generate** it.  
> LLAs live in `fe80::/10` and are used for **local-link communication,
> neighbor discovery, and default-gateway reachability**.

---

### 12.6.1 Dynamic LLAs  

All IPv6 devices must have at least one **Link-Local Address** on each
IPv6-enabled interface. Like IPv6 GUAs, LLAs can be created **dynamically**.

**How a dynamic LLA is built**

1. Start with the **`fe80::/10`** prefix.  
2. Pad the rest of the network bits with zeros → effectively `fe80::/64`.  
3. Generate the **64-bit interface ID** using either:
   - the **EUI-64 process** (from the MAC address), or  
   - a **randomly generated 64-bit number**.

Resulting format (conceptually):

```text
fe80:0000:0000:0000:XXXX:XXXX:XXXX:XXXX  →  fe80::XXXX:XXXX:XXXX:XXXX
```

> **Study note:**  
> Memorise: **LLA prefix = `fe80::/10`**. In most real configs you’ll see it
> as `fe80::/64` with a 64-bit interface ID.

> **Recruiter angle:**  
> I understand that even when a network isn’t “fully IPv6”, every modern host
> and router is already generating `fe80::/10` link-local addresses and using
> them for neighbor discovery and default-gateway communication.

---

### 12.6.2 Dynamic LLAs on Windows  

Operating systems such as Windows normally use the **same interface-ID method**
for both:

- a **SLAAC-created GUA**, and  
- a **dynamically created LLA**.

Only the **prefix** is different:

- GUA → something like `2001:db8:acad:1::/64`  
- LLA → always `fe80::/64`

#### Example – EUI-64 generated interface ID

```text
C:\> ipconfig

Ethernet adapter Local Area Connection:

   IPv6 Address . . . . . . . . . . : 2001:db8:acad:1::fc99:47ff:fe75:cee0
   Link-local IPv6 Address . . . . . : fe80::fc99:47ff:fe75:cee0
   Default Gateway . . . . . . . . . : fe80::1
```

Here Windows:

- Received the prefix `2001:db8:acad:1::/64` via RA (SLAAC).  
- Used **EUI-64** to turn the NIC MAC address into the interface ID
  `fc99:47ff:fe75:cee0`.  
- Combined that ID with:
  - the GUA prefix → **GUA** `2001:db8:acad:1::fc99:47ff:fe75:cee0`  
  - the LLA prefix → **LLA** `fe80::fc99:47ff:fe75:cee0`  

#### Example – Random 64-bit generated interface ID

```text
C:\> ipconfig

Ethernet adapter Local Area Connection:

   IPv6 Address . . . . . . . . . . : 2001:db8:acad:1::50a5:8a35:a5bb:66e1
   Link-local IPv6 Address . . . . . : fe80::50a5:8a35:a5bb:66e1
   Default Gateway . . . . . . . . . : fe80::1
```

Here the interface ID was chosen **randomly** for privacy, but the logic is the
same: one ID → used once with GUA prefix, once with `fe80::/64`.

> **Exam trap:**  
> Windows will show **both** a GUA and an LLA in `ipconfig`. The **default
> gateway** for IPv6 will often be written as the router’s **LLA**, not its GUA.

---

### 12.6.3 Dynamic LLAs on Cisco Routers  

Cisco routers **automatically create an IPv6 LLA** whenever you assign a GUA to
an interface.

- On **Ethernet** interfaces, IOS uses **EUI-64** based on the interface’s MAC
  address to build the LLA.
- On **serial** interfaces (no MAC), IOS uses the MAC address of the **first
  available Ethernet interface** to generate the interface ID.

This auto-generated LLA:

- Must be **unique only on that link**, not globally.  
- Can be a bit long and ugly, so in production many engineers choose to
  **overwrite it with a static, human-friendly LLA**.

#### Example – LLA using EUI-64 on Router R1  

```text
R1# show interface gigabitEthernet 0/0/0
GigabitEthernet0/0/0 is up, line protocol is up
  Hardware is ISR4221-2x1GE, address is 7079.b392.3640
  (output omitted)

R1# show ipv6 interface brief
GigabitEthernet0/0/0 [up/up]
    FE80::7279:B3FF:FE92:3640
    2001:DB8:ACAD:1::1
GigabitEthernet0/0/1 [up/up]
    FE80::7279:B3FF:FE92:3641
    2001:DB8:ACAD:2::1
Serial0/1/0 [up/up]
    FE80::7279:B3FF:FE92:3640
    2001:DB8:ACAD:3::1
Serial0/1/1 [down/down]
    unassigned
```

Notes:

- Each interface has **two IPv6 addresses**:
  - The **LLA** (starts with `fe80::`), auto-generated by IOS.  
  - The **GUA** that we configured (e.g. `2001:db8:acad:1::1/64`).
- Notice that the Serial0/1/0 LLA is the **same** as G0/0/0’s LLA.  
  That’s ok because **they are on different links**.

> **Study note:**  
> `show ipv6 interface brief` is the go-to command to see the **status, LLAs,
> and GUAs** of all interfaces in one shot.

> **Recruiter angle:**  
> I’m comfortable reading router output and explaining why an interface has
> multiple IPv6 addresses and how IOS derived the link-locals automatically.

---

### 12.6.4 Verify IPv6 Address Configuration  

This topic glues everything together: **LLAs, GUAs, routes, and pings**.

Example topology:

- **PC1** – `2001:db8:acad:1::10/64`, default gateway R1 G0/0/0  
- **PC2** – `2001:db8:acad:2::10/64`, default gateway R1 G0/0/1  
- **R1 G0/0/0** – `2001:db8:acad:1::1/64`, `fe80::1:1`  
- **R1 G0/0/1** – `2001:db8:acad:2::1/64`, `fe80::2:1`  
- **R1 S0/1/0** – `2001:db8:acad:3::1/64`, `fe80::3:1`  

#### 1. Check interface status and addresses

```text
R1# show ipv6 interface brief
GigabitEthernet0/0/0   [up/up]
    FE80::1:1
    2001:DB8:ACAD:1::1
GigabitEthernet0/0/1   [up/up]
    FE80::2:1
    2001:DB8:ACAD:2::1
Serial0/1/0            [up/up]
    FE80::3:1
    2001:DB8:ACAD:3::1
Serial0/1/1            [down/down]
    unassigned
GigabitEthernet0       [administratively down/down]
    unassigned
```

Quick checks:

- Interfaces that should carry traffic are **`[up/up]`**.  
- Each has both an **LLA** and a **GUA**.  
- Extra interfaces can be down/unassigned.

#### 2. Check the IPv6 routing table

```text
R1# show ipv6 route
IPv6 Routing Table - default - 7 entries
Codes: C - Connected, L - Local, S - Static, ...

C   2001:DB8:ACAD:1::/64   [0/0]
     via GigabitEthernet0/0/0, directly connected
L   2001:DB8:ACAD:1::1/128 [0/0]
     via GigabitEthernet0/0/0, receive
C   2001:DB8:ACAD:2::/64   [0/0]
     via GigabitEthernet0/0/1, directly connected
L   2001:DB8:ACAD:2::1/128 [0/0]
     via GigabitEthernet0/0/1, receive
C   2001:DB8:ACAD:3::/64   [0/0]
     via Serial0/1/0, directly connected
L   2001:DB8:ACAD:3::1/128 [0/0]
     via Serial0/1/0, receive
L   FF00::/8               [0/0]
     via Null0, receive
```

Interpretation:

- **`C` (Connected)** routes show the **/64 LAN prefixes** on each interface.  
- **`L` (Local)** routes show the **/128 addresses** of the router’s own
  interfaces.  
- `FF00::/8` is the IPv6 multicast range (special, always present).

#### 3. Verify end-to-end connectivity with ping

```text
R1# ping 2001:db8:acad:1::10
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2001:DB8:ACAD:1::10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
```

If `show ipv6 interface brief` and `show ipv6 route` look good but `ping`
fails, you can start checking:

- Host configs (wrong prefix length? wrong default gateway?)  
- Duplicate addresses (DAD failure)  
- Access lists / firewall rules.

> **Study note:**  
> This trio – `show ipv6 interface brief`, `show ipv6 route`, `ping` – is your
> basic IPv6 troubleshooting toolkit.

---

### 12.6.5 Syntax Checker – Verify IPv6 Address Configuration  

This activity asks you to **enter the correct `show` command** and interpret the
output for R1.

**Question 1 – brief interface status**

> *“Enter the show command that will display a brief summary of the IPv6
> interface status.”*

Correct command:

```text
R1# show ipv6 interface brief
```

This confirms:

- which interfaces are up/down, and  
- which LLAs/GUAs are assigned.

**Question 2 – verify connectivity to PC**

You then:

1. Use `show ipv6 route` to confirm there is a **connected route** to the
   PC’s subnet.  
2. Use `ping` to test connectivity to PC1/PC2.

The NetAcad answer verifies a ping from R1 to PC1:

```text
R1# ping 2001:db8:acad:1::10
!!!!!
```

> **Exam trap:**  
> If a question asks for “a brief summary of the IPv6 interface status” the
> expected command is **`show ipv6 interface brief`**, not `show interface` or
> `show ipv6 interface` (those are more verbose).

> **Recruiter angle:**  
> I can quickly verify IPv6 addressing and connectivity on a Cisco router using
> the right `show` commands and interpret what I see.

---

### 12.6.6 Packet Tracer – Configure IPv6 Addressing  

**Goal of the PT activity**

- Practise configuring **IPv6 addresses** on:
  - routers  
  - servers  
  - clients
- Then verify the implementation using:
  - `show ipv6 interface brief`  
  - `show ipv6 route`  
  - `ping` (end-to-end tests)

**What I train here**

- Filling an **IPv6 addressing table** from a lab diagram.  
- Assigning **both LLAs and GUAs** to router interfaces.  
- Configuring IPv6 on Windows / server NICs and setting the **default gateway**
  to the router’s LLA.  
- Troubleshooting until every device can reach the others over IPv6.

> **Summary statement for portfolio:**  
> *“In the IPv6 Addressing Packet Tracer lab I configured GUAs and LLAs on
> routers, switches, and PCs, and verified connectivity using Cisco IOS `show`
> commands and ICMPv6. This exercise reinforced my understanding of dynamic
> link-local addressing and basic IPv6 troubleshooting.”*


---

## 12.7 Overview

### Big picture

- IPv6 has **no broadcast**. What IPv4 would broadcast, IPv6 normally does with **multicast**.
- Multicast lets one sender efficiently reach **multiple receivers** that have joined the same group.
- IPv6 multicast addresses always start with the prefix:

  ```text
  ff00::/8
  ```

- An IPv6 multicast address is **only ever used as a destination**, never as a source.

There are two main multicast types in this module:

1. **Well-known multicast** – pre-assigned group addresses (e.g. all-nodes, all-routers).  
2. **Solicited-node multicast** – automatically derived per unicast address and used by Neighbor Discovery.

---

## 12.7.1 Assigned IPv6 Multicast Addresses

> Earlier we saw three IPv6 address categories: **unicast, anycast, multicast**.  
> Here we zoom in on the multicast side.

Key points:

- An IPv6 multicast address identifies a **multicast group** (one-to-many).  
- Hosts/apps **join** specific groups; routers forward copies only to links with interested receivers.
- Prefix: **`ff00::/8`**  
  - `ff` in the first 8 bits signals “this is multicast”.

**Assigned (well-known) multicast addresses**

- These are reserved addresses for specific protocols or functions.
- Examples beyond the CCNA scope exist (e.g. OSPFv3, RIPng groups), but in this module we focus on **all-nodes** and **all-routers**.

Why multicast instead of broadcast?

- Avoids waking up devices that **did not subscribe**.  
- Scales better for large IPv6 segments.  
- Keeps the protocol cleaner (no special broadcast type to treat differently).

---

## 12.7.2 Well-Known IPv6 Multicast Addresses

Well-known IPv6 multicast groups you must know cold:

### 1. All-nodes multicast – `ff02::1`

- Group name: **all-nodes**.  
- Scope: **link-local** (the `02` in `ff02` indicates link-local scope).  
- Joined by: **every IPv6-enabled interface** on the link.
- Effect: Sending a packet to `ff02::1` reaches **all IPv6 nodes** on that local network.

Common usage:

- Routers send **ICMPv6 Router Advertisements (RAs)** to `ff02::1` to tell all nodes:  
  - “Here is the IPv6 prefix and default gateway; here’s how to get an address.”
- Some diagnostic tools and protocols can also use `ff02::1` when they really want to reach all nodes.

### 2. All-routers multicast – `ff02::2`

- Group name: **all-routers**.  
- Scope: **link-local**.  
- Joined by: all IPv6 routers on the link **after** you enable IPv6 routing with:

  ```text
  ipv6 unicast-routing
  ```

Common usage:

- Hosts send **ICMPv6 Router Solicitations (RS)** to `ff02::2` when they first join a link and want an RA quickly.
- Routing protocols may also use all-routers or their own multicast groups to find neighbors.

### Conceptual comparison

- `ff02::1` is the **IPv6 “broadcast-like” address** – but still multicast.  
- `ff02::2` reaches only the routers, not end hosts.

Remember: **IPv6 never broadcasts; it multicasts.**

---

## 12.7.3 Solicited-Node IPv6 Multicast Addresses

> Goal: deliver Neighbor Discovery traffic only to **potential matches**, not every node.

### What is a solicited-node multicast address?

- Think of it as a **smart, per-unicast multicast group**.
- Every **unicast** IPv6 address (GUA, LLA, ULA) automatically has an associated **solicited-node** group.
- Prefix:

  ```text
  ff02::1:ff00:0/104
  ```

- The **last 24 bits** (6 hex digits) of the unicast address are copied into the solicited-node address.

Example:

```text
Unicast address:        2001:db8:acad:1::1234:5678
Take last 24 bits:                           34:5678
Solicited-node group:  ff02::1:ff34:5678
```

Each host joins the solicited-node group(s) for all of its unicast addresses.

### Why do we use solicited-node multicast?

- Used by **ICMPv6 Neighbor Discovery (ND)** to perform the equivalent of ARP in IPv4.
- Instead of sending “Who has this IPv6?” to **everyone** (`ff02::1`), the router/host sends it only to the **relevant solicited-node group**.
- This dramatically reduces unnecessary processing compared to a broadcast model.

### Interaction with Ethernet MAC addresses

- Each solicited-node IPv6 multicast group is mapped to a special **Ethernet multicast MAC** address.  
- The NIC can check the **destination MAC** itself and drop frames that are clearly for a different solicited-node group **before** they reach the IPv6 stack.

In practice:

- PC receives an Ethernet frame with a multicast destination MAC; the NIC checks the MAC.  
- If it does not match any joined solicited-node group, the NIC drops the frame and we never waste CPU time in the IP layer.

**Key mental image:**

> *“Solicited-node multicast is a per-address filter that lets Neighbor Discovery ask ‘Who owns this IPv6?’ without shouting at the entire link.”*

---

## 12.7.4 Lab – Identify IPv6 Addresses (Summary)

Lab name: **12.7.4 – Lab: Identify IPv6 Addresses** fileciteturn8file0

### Part 1 – Practice with IPv6 Address Types

Activities:

- Given a list of compressed IPv6 addresses, you have to classify each as:  
  - Loopback (`::1`)  
  - Global unicast (starts with `2xxx` or `3xxx`)  
  - Link-local (`fe80::/10`)  
  - Unique local (`fc00::/7` – `fdxx::`)  
  - Multicast (`ffxx::`)
- Practise **compressing and decompressing** IPv6 addresses using:
  - Removing leading zeros per hextet.
  - Using `::` once for contiguous zero hextets.

What this teaches:

- Recognising address **type just by its prefix**.  
- Being fluent at IPv6 **notation rules** (super important for exams and troubleshooting).

### Part 2 – Examine a Host IPv6 Interface

Activities:

- Confirm IPv6 is installed and active on a Windows PC.
- Use `ipconfig /all` to inspect:
  - Link-local IPv6 address (`fe80::...`).  
  - Whether there are any **global** or **unique-local** addresses configured.  
  - Default gateway (often an IPv4 address in older/home setups).

Typical findings:

- On a small home network, the PC may have **only a link-local IPv6 address** and **no GUA/ULA**, which hints that the router is not providing IPv6 internet access yet.
- The interface ID portion of the link-local address is often **randomly generated**, showing that privacy-aware addressing is used.

### Reflection questions from the lab

- *How will I need to support IPv6 in future networks?*  
  → Plan for **dual-stack**, **IPv6-only segments**, and tools that understand both IPv4 and IPv6.

- *Will IPv4 continue forever?*  
  → Realistically we will see **dual-stack** and **translation** for many years, but the long-term direction is clearly **more IPv6**, especially for new services and IoT-style deployments.

---

## Cheat Sheet – Addresses to Memorise

| Function                      | IPv6 Address / Prefix        | Notes                                       |
|------------------------------|------------------------------|---------------------------------------------|
| All IPv6 multicast           | `ff00::/8`                   | All multicast groups start with `ff`.       |
| All-nodes (link-local)       | `ff02::1`                    | Joined by every IPv6 node.                  |
| All-routers (link-local)     | `ff02::2`                    | Joined by all IPv6 routers.                 |
| Solicited-node multicast     | `ff02::1:ff00:0/104`         | Last 24 bits copied from unicast address.   |
| Link-local unicast           | `fe80::/10`                  | Non-routable; one per interface minimum.    |
| Unique local unicast (ULA)   | `fc00::/7`                   | Similar to IPv4 private ranges.             |
| Global unicast (current)     | `2000::/3`                   | Internet-routable IPv6 public space.        |

> **If I only remember three multicast addresses for the exam:**  
> `ff02::1` (all-nodes), `ff02::2` (all-routers), and the **solicited-node pattern** `ff02::1:ff00:0/104`.

---

## Talking Points for Recruiters

When I show this section in my portfolio, these are points I can explain in an interview:

- **Why IPv6 removed broadcast** and relies on multicast instead, and how that impacts security and performance.
- How **all-nodes** and **all-routers** multicast groups are used by **ICMPv6 Router Discovery (RS/RA)**.
- How **solicited-node multicast** plus **Ethernet multicast MAC mapping** makes Neighbor Discovery more efficient than IPv4 ARP.
- How to recognise and categorise IPv6 addresses (GUA, LLA, ULA, multicast, loopback) just from their **prefixes**.
- How I can use tools like `ping`, `ipconfig`, and `show ipv6 interface brief` to verify IPv6 addressing and multicast group membership on real equipment.

> Short CV line I can use:
> *"Comfortable working with IPv6 multicast (all-nodes, all-routers, solicited-node groups) and Neighbor
> Discovery, including how multicast replaces IPv4 broadcast on modern networks."*


---

# CCNA – Module 12.8 IPv6 Subnetting (Study + Recruiter Notes)

> **Use case:** This file is both a study guide for me (**EchoLynx**) and a
> portfolio artifact for recruiters to see that I understand **IPv6 subnetting**
> and how it differs from IPv4.

---

## 12.8 Overview

> **Big idea:** IPv6 was designed with subnetting in mind. Instead of “stealing”
> host bits like in IPv4, IPv6 GUAs have a dedicated **Subnet ID** field that
> makes subnetting simple and highly scalable.

In this section I practise:

- Reading the **GUA structure**: Global Routing Prefix, Subnet ID, Interface ID.
- Subnetting a block like `2001:db8:acad::/48` into /64 subnets using the
  16‑bit Subnet ID field.
- Planning subnet allocation for a small topology (LANs + WAN links).
- Writing basic Cisco IOS configs to assign those IPv6 subnets to router
  interfaces.
- Answering exam‑style questions about **Subnet ID size** and **which hextet is
  the subnet**.

---

## 12.8.1 Subnet Using the Subnet ID

In IPv4, subnetting was an **afterthought**. We “borrow” bits from the host
portion, calculate weird masks, and keep track of “network” vs “broadcast”
addresses.

IPv6 fixed this by building subnetting into the address structure.

### Typical GUA structure (using /64 subnets)

```text
|<------ 48 bits ------>|<--16-->|<------------ 64 bits ------------>|
+-----------------------+--------+-----------------------------------+
| Global Routing Prefix | Subnet |          Interface ID             |
+-----------------------+--------+-----------------------------------+
```

- **Global Routing Prefix** – assigned by the ISP (e.g. `/32`, `/40`, `/48`).
- **Subnet ID** – used **inside the organisation** to create subnets.
- **Interface ID** – last 64 bits, the “host” portion (SLAAC / EUI‑64 / random).

With a `/48` prefix and `/64` subnets:

- Subnet ID has **16 bits** (from bit 49 to 64).
- That gives **2¹⁶ = 65,536 subnets**.
- Each `/64` subnet has **2⁶⁴ ≈ 1.8×10¹⁹ interface addresses**.

> IPv6 address conservation is **not** a concern. The design goal is simplicity
> and hierarchical addressing, not squeezing every single host address.

**Note:** It *is* technically possible to subnet further into the 64‑bit
Interface ID (host portion), but that breaks SLAAC expectations and is rarely
done in modern designs.

**Recruiter‑angle sentence**

> “Unlike IPv4, IPv6 GUAs have a dedicated Subnet ID field. With a /48 prefix I
> can carve out 65k /64s just by incrementing one hextet in hex – no binary
> gymnastics.”

---

## 12.8.2 IPv6 Subnetting Example

**Given:**

- Organisation receives **`2001:db8:acad::/48`** as its Global Routing Prefix.
- We want standard **`/64` subnets**.

That means:

- First **3 hextets** (`2001:db8:acad`) = **Global Routing Prefix**.
- Next **1 hextet** (16 bits) = **Subnet ID**.
- Last **4 hextets** = Interface ID.

We keep the first 3 hextets constant and **increment the 4th hextet** in
hexadecimal to create subnets:

```text
2001:db8:acad:0000::/64
2001:db8:acad:0001::/64
2001:db8:acad:0002::/64
2001:db8:acad:0003::/64
2001:db8:acad:0004::/64
2001:db8:acad:0005::/64
2001:db8:acad:0006::/64
2001:db8:acad:0007::/64
2001:db8:acad:0008::/64
2001:db8:acad:0009::/64
2001:db8:acad:000a::/64
...
2001:db8:acad:fffe::/64
2001:db8:acad:ffff::/64
```

Here:

- `0000` → first subnet,
- `0001` → second subnet,
- `0002` → third subnet,
- …
- `ffff` → 65,536‑th subnet.

> **Study rule:** When subnetting a `/48` GUA into `/64`s, the **fourth hextet
> is always the Subnet ID**. You just count up in hex.

---

## 12.8.3 IPv6 Subnet Allocation

Now we allocate subnets from `2001:db8:acad::/48` to a simple topology.

### Example topology

The network needs five `/64` subnets:

1. LAN1 (PC1 + switch) on **R1 G0/0/0**
2. LAN2 (PC2 + switch) on **R1 G0/0/1**
3. The WAN link between **R1 S0/1/0** and **R2 S0/1/0**
4. LAN3 (PC3 + switch) on **R2 G0/0/0**
5. LAN4 (PC4 + switch) on **R2 G0/0/1**

We simply take the **first five Subnet IDs**:

```text
Base block: 2001:db8:acad::/48

Subnets used:
- 2001:db8:acad:0001::/64   (LAN1)
- 2001:db8:acad:0002::/64   (LAN2)
- 2001:db8:acad:0003::/64   (R1–R2 link)
- 2001:db8:acad:0004::/64   (LAN3)
- 2001:db8:acad:0005::/64   (LAN4)
```

In the course graphics, these are shown in compressed form:

```text
2001:db8:acad:1::/64
2001:db8:acad:2::/64
2001:db8:acad:3::/64
2001:db8:acad:4::/64
2001:db8:acad:5::/64
```

Host examples:

- PC1 → `2001:db8:acad:1::10/64`
- PC2 → `2001:db8:acad:2::10/64`
- PC3 → `2001:db8:acad:4::10/64`
- PC4 → `2001:db8:acad:5::10/64`

Design notes:

- All **LANs and the serial link** use the same `/64` prefix length – we do *not*
  shrink WAN subnets the way we sometimes do in IPv4.
- This “wastes” addresses but **simplicity > conservation** in IPv6.

---

## 12.8.4 Router Configured with IPv6 Subnets

On Cisco IOS, configuring IPv6 subnets looks very similar to other IPv6
examples from this module.

### Router R1 – IPv6 GUA configuration

```text
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface serial 0/1/0
R1(config-if)# ipv6 address 2001:db8:acad:3::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
```

(An equivalent config would be created on R2 using subnets `:3::/64` on the
WAN side and `:4::/64` & `:5::/64` on its LAN interfaces.)

Key takeaways:

- Each interface gets a unique `/64` from the `/48` block.
- Prefix length must match the addressing plan (`/64` here).
- As always in IOS, `no shutdown` is required to bring interfaces up.

> **Interview phrase:** “Given `2001:db8:acad::/48`, I’d use `:1::/64`,
> `:2::/64`, `:3::/64`… for each R1 interface and the R1–R2 link, and then
> mirror that pattern on R2. The config is just `ipv6 address <subnet>::1/64`
> plus `no shutdown`.”

---

## 12.8.5 Check Your Understanding – Subnet an IPv6 Network

These are the mini‑quiz questions from the end of 12.8, with answers and short
explanations.

### Q1 – Was IPv6 designed with subnetting in mind?

> **Question:**  
> True or False? IPv6 was designed with subnetting in mind.

**Correct answer:** ✅ `True`

**Why**

- IPv6 includes a dedicated **Subnet ID** field between the Global Routing
  Prefix and the Interface ID.
- This makes subnetting a **first‑class feature**, not an afterthought like in
  IPv4 where we “borrow” host bits.

---

### Q2 – Which GUA field is used for subnetting?

> **Question:**  
> Which field in an IPv6 GUA is used for subnetting?

Options (from the quiz):

- Interface ID  
- Network  
- Global Routing Prefix  
- **Subnet ID** ✅  
- Prefix  

**Correct answer:** ✅ **Subnet ID**

**Why**

- The **Global Routing Prefix** identifies the organisation/site on the
  internet.
- The **Subnet ID** is what we vary inside the organisation to create multiple
  `/64` subnets under that prefix.

---

### Q3 – Identify the Subnet ID hextet

> **Question:**  
> Given a `/48` Global Routing Prefix and a `/64` prefix, what is the subnet
> portion of the following address?  
> `2001:db8:cafe:1111:2222:3333:4444:5555`

Options:

- 3333  
- **1111** ✅  
- 2222  
- Café  
- 4444  

**Correct answer:** ✅ `1111`

**Reasoning**

- `/48` = first **three hextets** (16 bits × 3): `2001:db8:cafe` → Global
  Routing Prefix.
- `/64` means next **one hextet** (16 bits) is the **Subnet ID**.
- That 4th hextet is `1111`.

> **Pattern:**  
> For a `/48` → `/64` scheme:  
> - Hextets 1–3 = Global Routing Prefix  
> - Hextet 4 = Subnet ID  
> - Hextets 5–8 = Interface ID  

---

### Q4 – How many Subnet ID bits?

> **Question:**  
> Given a `/32` Global Routing Prefix and a `/64` prefix, how many bits are
> allocated for the Subnet ID?

Options:

- **32** ✅  
- 8  
- 16  
- 64  
- 48  

**Correct answer:** ✅ `32`

**Reasoning**

- Prefix length `/64` minus Global Routing Prefix `/32` =  
  `64 − 32 = 32` bits left for the **Subnet ID**.
- That means `2³²` possible `/64` subnets (over 4 billion).

> **Formula:**  
> `SubnetID_bits = Subnet_prefix_length − GlobalRoutingPrefix_length`

---

## Cheat‑Sheet Summary for Interviews

Bullet points I can reuse in CVs / interviews:

- **IPv6 GUA structure:**  
  `Global Routing Prefix (provider) + Subnet ID (customer) + Interface ID (host)`.
- With a `/48` allocation, using `/64` subnets gives:
  - **16‑bit Subnet ID → 65,536 /64s**,  
  - each `/64` with **2⁶⁴ interface addresses**.
- Subnetting is **trivial**: keep the first three hextets fixed and increment
  the 4th hextet in hexadecimal.
- WAN links **also use `/64`** in IPv6 – we don’t try to shrink them like in
  IPv4 because address space is effectively unlimited.
- On Cisco IOS, assigning subnets is as simple as:

  ```text
  interface g0/0/0
    ipv6 address 2001:db8:acad:1::1/64
    no shutdown
  ```

- I understand which part of an IPv6 address is:
  - the **Global Routing Prefix** (ISP / organisation),
  - the **Subnet ID** (internal design),
  - the **Interface ID** (host).

> **One‑liner:**  
> *“For IPv6 subnetting I think in hextets, not dotted masks – e.g. from a
> `2001:db8:acad::/48` block I just count `:1::/64`, `:2::/64`, `:3::/64`… for
> each link. The Subnet ID field makes planning 65k+ subnets almost trivial.”*


---

# CCNA – IPv6 Addressing (Module 12)  
## Section 12.9 – Practice, Labs & Module Quiz

> **Use case:** This file is both my personal study guide (**EchoLynx**) and a
> portfolio artifact for recruiters. It summarises how I *apply* IPv6
> addressing in labs and how I think about exam‑style questions.

---

## 12.9 Overview

**Goal of 12.9:** Take everything from Module 12 (IPv6 addressing, LLAs, GUAs,
multicast, subnetting) and **apply it in Packet Tracer and labs**, then finish
with a quiz that checks understanding.

Core skills I practise here:

- Designing IPv6 subnets from a larger prefix (/48 → multiple /64s).
- Assigning IPv6 GUAs and LLAs on routers, switches, and PCs.
- Enabling IPv6 routing and SLAAC so hosts auto‑configure addresses.
- Verifying connectivity with `show` commands, `ping`, and `traceroute`.
- Reading quiz questions carefully and mapping them back to the theory.

> **Recruiter angle:**  
> Shows that I can design and implement an IPv6 addressing plan end‑to‑end,
> not just memorise theory. I’m comfortable jumping between design, config, and
> verification.

---

## 12.9.1 Packet Tracer – Implement a Subnetted IPv6 Addressing Scheme

**Scenario**

- I’m given an **IPv6 /48 global routing prefix** for the organisation,
  e.g. `2001:db8:acad::/48`.
- The topology needs **five /64 LANs** (PC segments + serial link).
- My job:
  1. Design the /64 subnets using the 16‑bit **Subnet ID field**.
  2. Assign addresses to router interfaces.
  3. Configure PCs to obtain IPv6 addressing automatically.
  4. Verify IPv6 connectivity between all IPv6 hosts.

### Designing the Subnet IDs

With `/48` global prefix + `/64` per subnet:

- First **48 bits** (first 3 hextets) = **Global Routing Prefix**  
  `2001:db8:acad`
- Next **16 bits** (fourth hextet) = **Subnet ID**  
- Last **64 bits** = **Interface ID**

I can create 65,536 subnets (`0000` to `ffff`).  
For 5 subnets I can simply use:

```text
2001:db8:acad:0000::/64   (Subnet ID 0000)
2001:db8:acad:0001::/64   (Subnet ID 0001)
2001:db8:acad:0002::/64   (Subnet ID 0002)
2001:db8:acad:0003::/64   (Subnet ID 0003)
2001:db8:acad:0004::/64   (Subnet ID 0004)
```

In compressed form:

```text
2001:db8:acad:0::/64
2001:db8:acad:1::/64
2001:db8:acad:2::/64
2001:db8:acad:3::/64
2001:db8:acad:4::/64
```

### Example Addressing Plan

- LAN 1 (PC1 + switch + R1 G0/0/0): `2001:db8:acad:1::/64`
  - R1 G0/0/0 – `2001:db8:acad:1::1/64`
  - PC1 – `2001:db8:acad:1::10/64` (via SLAAC or static)
- LAN 2 (PC2 + switch + R1 G0/0/1): `2001:db8:acad:2::/64`
  - R1 G0/0/1 – `2001:db8:acad:2::1/64`
  - PC2 – `2001:db8:acad:2::10/64`
- WAN link R1–R2:
  - `2001:db8:acad:3::/64` (R1 G0/0/2 & R2 G0/0/0)
- Additional LANs for PC3, PC4:
  - `2001:db8:acad:4::/64`
  - `2001:db8:acad:5::/64`

All subnets share the same **/48 global prefix** but have unique **Subnet IDs**.

### Key CLI Steps

On router interfaces:

```text
interface g0/0/0
 ipv6 address 2001:db8:acad:1::1/64
 ipv6 address fe80::1:1 link-local
 no shutdown

interface g0/0/1
 ipv6 address 2001:db8:acad:2::1/64
 ipv6 address fe80::2:1 link-local
 no shutdown

interface s0/1/0
 ipv6 address 2001:db8:acad:3::1/64
 ipv6 address fe80::3:1 link-local
 no shutdown
```

Globally enable IPv6 routing so RAs/SLAAC work:

```text
ipv6 unicast-routing
```

On PCs:

- Usually set NICs to **auto** (SLAAC) so they learn:
  - GUA (`2001:db8:acad:x::xxxx/64`)
  - Default gateway (router **LLA** like `fe80::1:1`)

### Commands to Verify

- `show ipv6 interface brief` – quick summary of GUAs + LLAs and status.
- `show ipv6 route` – ensure all directly connected /64s appear.
- `ping <remote-GUA>` – test host‑to‑host.
- `traceroute <remote-GUA>` – confirm path across routers.

> **Recruiter angle:**  
> This lab shows I can convert a high‑level prefix allocation (`/48`) into a
> concrete addressing plan (multiple `/64`s), implement it in IOS, and validate
> it with the right show and test commands.

---

## 12.9.2 Lab – Configure IPv6 Addresses on Network Devices

There are two flavours here:

- Standard Packet Tracer lab.
- Packet Tracer **Physical Mode (PTPM)** version (same logic, more realistic
  cabling).

The typical addressing table (from the PTPM lab) looks like:

| Device | Interface | IPv6 Address           | /Prefix | Default GW |
|--------|-----------|------------------------|---------|-----------|
| R1     | G0/0/0    | `2001:db8:acad:a::1`   | /64     | N/A       |
| R1     | G0/0/1    | `2001:db8:acad:1::1`   | /64     | N/A       |
| S1     | VLAN 1    | `2001:db8:acad:1::b`   | /64     | `fe80::1` |
| PC‑A   | NIC       | `2001:db8:acad:1::3`   | /64     | `fe80::1` |
| PC‑B   | NIC       | `2001:db8:acad:a::3`   | /64     | `fe80::1` |

### Part 1 – Basic Setup

- Cable the PCs, switch S1, and router R1 according to the topology.
- Configure:
  - Hostnames
  - Console / VTY passwords
  - Banner MOTD
  - Disable DNS lookup, etc.

### Part 2 – Manually Configure IPv6 Addresses

**Step 1 – GUAs on R1**

- Assign the IPv6 GUAs from the addressing table to `G0/0/0` and `G0/0/1`.
- IOS auto‑creates LLAs (EUI‑64) based on MAC addresses.
- Optionally overwrite LLAs with easy‑to‑remember ones:

  ```text
  interface g0/0/0
   ipv6 address fe80::1 link-local
  interface g0/0/1
   ipv6 address fe80::1 link-local
  ```

  Using the same LLA on both interfaces is allowed because **LLAs only need
  to be unique per link**.

**Step 2 – Enable IPv6 Routing and RAs**

- Turn on IPv6 routing:

  ```text
  ipv6 unicast-routing
  ```

- Now R1:
  - Joins the **all‑routers multicast group** `ff02::2`.
  - Starts sending **RA** messages out its interfaces.

- PCs configured for **automatic IPv6** will receive:
  - The prefix + prefix‑length
  - Default gateway (R1’s LLA)
  - Possibly DNS info (depending on lab)

**Step 3 – IPv6 on S1**

- Configure S1’s management SVI:

  ```text
  interface vlan 1
   ipv6 address 2001:db8:acad:1::b/64
   ipv6 address fe80::1 link-local
   no shutdown
  ```

- The switch uses R1’s LLA as its default gateway (from the RA).

**Step 4 – Static GUAs on PCs**

- PCs already have a SLAAC address. Add an extra static one:

  ```text
  2001:db8:acad:1::3/64   (PC‑A)
  2001:db8:acad:a::3/64   (PC‑B)
  ```

- Default gateway: `fe80::1` (R1’s LLA on that link).

### Part 3 – Verify End‑to‑End Connectivity

Useful commands:

- On R1:

  ```text
  show ipv6 interface brief
  show ipv6 route
  ```

- On PCs:

  ```text
  ipconfig
  ping <remote-IPv6>
  tracert <remote-IPv6>
  ```

Connectivity tests:

1. From PC‑A: `ping fe80::1` (R1 LLA).
2. From PC‑A: `tracert` to PC‑B’s GUA.
3. From PC‑B: `ping` PC‑A.
4. From PC‑B: `ping` R1’s LLA on the opposite interface.

### Reflection questions (with answers)

1. **Why can I use the same link‑local address `fe80::1` on both R1 interfaces?**  
   Because LLAs only need to be **unique on each link**. G0/0/0 and G0/0/1 are
   different networks, so using `fe80::1` on both does not create ambiguity.

2. **Subnet ID of `2001:db8:acad::aaaa:1234/64` with a `/48` global prefix?**  
   - `/48` global prefix → first 3 hextets: `2001:db8:acad`.  
   - `/64` prefix → first 4 hextets: `2001:db8:acad:0000`.  
   - Therefore the **Subnet ID** is the 4th hextet = `0000` (or just `0`).

> **Recruiter angle:**  
> These labs show that I not only know IPv6 theory, but can also:
> - Configure dual GUAs/LLAs per interface.
> - Use RA/SLAAC + static addressing together.
> - Confirm behaviour via routing table and interface status.

---

## 12.9.3 What did I learn in this module?

This section of NetAcad summarises all of Module 12. Here is my distilled
version.

### IPv4 Issues

- IPv4 has ~4.3 billion addresses – not enough for today’s internet.
- Private IPv4 + NAT delayed address exhaustion but:
  - Breaks end‑to‑end connectivity,
  - Complicates some protocols (VoIP, IPsec, P2P),
  - Adds operational complexity.
- With more users and IoT devices, IPv4 alone is no longer sustainable.
- Transition mechanisms to IPv6:
  - **Dual stack** (preferred),
  - **Tunneling**,
  - **Translation** (e.g. NAT64).

### IPv6 Address Representation

- IPv6 uses **128‑bit addresses** written as 8 hex hextets.
- Two big formatting rules:
  1. **Omit leading zeros** in any hextet.
  2. Use **`::` once** to replace a single, longest run of all‑zero hextets.
- Prefix length is shown as `/n` (e.g. `/64`), not with dotted‑decimal masks.

### IPv6 Address Types

- Three categories: **unicast**, **multicast**, **anycast**.
- IPv6 unicast addresses usually in **CIDR slash notation** (e.g. `/64`).
- Two key unicast types:
  - **GUA** – globally unique, routable on the internet.
  - **LLA** – `fe80::/10`, for communication only on the local link.
- ULAs (`fc00::/7`) exist for internal‑only addressing.
- IPv6 has **no broadcast**; uses multicast instead.

### GUA and LLA Static Configuration

- IPv4 command:

  ```text
  ip address <ipv4-address> <mask>
  ```

- IPv6 GUA command:

  ```text
  ipv6 address <ipv6-address>/<prefix-length>
  ```

- LLAs on IOS:

  ```text
  ipv6 address <link-local-address> link-local
  ```

- Static configuration doesn’t scale to very large networks, but is perfect for:
  - Labs,
  - Infrastructure devices,
  - Servers requiring stable addresses.

### Dynamic Addressing for IPv6 GUAs

- Hosts can obtain GUAs via **RA messages** + optional **DHCPv6**.
- Three RA configurations hosts can receive:
  1. **SLAAC only** – host self‑generates GUA, uses router LLA as gateway.
  2. **SLAAC + stateless DHCPv6** – SLAAC for GUA, DHCPv6 for DNS/extra info.
  3. **Stateful DHCPv6** – DHCPv6 provides GUA and options; router still
     provides default gateway via RA.
- Interface ID can be built via:
  - **EUI‑64** (MAC‑based), or
  - **Random 64‑bit** value (privacy extensions).

### Dynamic Addressing for IPv6 LLAs

- Every IPv6 interface *must* have an LLA.
- LLAs can be:
  - Manually configured, or
  - Auto‑generated based on MAC or random values.
- On Cisco routers, assigning a GUA to an interface will automatically create
  an LLA.
- Verification commands:
  - `show ipv6 interface brief`
  - `show ipv6 route`
  - `ping <IPv6>`

### IPv6 Multicast Addresses

- Two types:
  - **Well‑known (assigned)** – e.g. `ff02::1` (all‑nodes), `ff02::2` (all‑routers).
  - **Solicited‑node** – used for Neighbor Discovery, mapped to special
    Ethernet multicast MAC addresses.
- Solicited‑node multicast lets NICs filter traffic in hardware, instead of
  punting all multicast up to the IPv6 stack.

### Subnet an IPv6 Network

- IPv6 was designed with **subnetting in mind**:
  - There is a specific **Subnet ID** field between the global routing prefix
    and the interface ID.
- Typical example: `/48` global prefix + `/64` on links
  - **16‑bit Subnet ID** → 65,536 subnets.
  - **64‑bit interface ID** → ~18 quintillion host addresses per subnet.
- Address conservation is not an issue; focus is on **logical design** and
  clear subnetting schemes.

> **Recruiter angle:**  
> I can explain not just how to configure IPv6, but also *why* IPv6 exists and
> how its design (128‑bit space, Subnet ID field, multicast, SLAAC) solves
> real scalability and automation problems.

---

# 12.9.4 Module Quiz – IPv6 Addressing (Explained Answers)

> **Use case:** Quick-reference answer key for the NetAcad quiz  
> **“12.9.4 Module Quiz – IPv6 Addressing”** with explanations that show
> my (EchoLynx) understanding for both **revision** and **recruiters**.

Each question below includes:

- The **correct option** (matching the on-screen quiz wording).
- A short **exam-style justification**.
- A brief **“concept check”** that ties it back to the core ideas of Module 12.

---

## Q1 – Most Compressed IPv6 Address (Rules 1 and 2)

**Question**

> What is the valid most compressed format possible of the IPv6 address  
> `2001:0DB8:0000:AB00:0000:0000:0000:1234`?

**Correct answer**

> ✅ `2001:DB8:0:AB00::1234`

**Why this is correct**

1. **Apply Rule 1 (omit leading zeros)** per hextet:

   ```text
   2001:0DB8:0000:AB00:0000:0000:0000:1234
   → 2001:DB8:0:AB00:0:0:0:1234
   ```

2. **Apply Rule 2 (double colon)** to the **single longest sequence** of all-zero
   hextets. Here, the run is `0:0:0`:

   ```text
   2001:DB8:0:AB00:0:0:0:1234
   → 2001:DB8:0:AB00::1234
   ```

3. You **must not** use `::` twice, so options like `2001:DB8::AB00::1234` are invalid.

**Concept check**

- Shows I can **compress IPv6 addresses correctly**, respecting:
  - Rule 1 – remove leading zeros inside a hextet.
  - Rule 2 – use `::` only once for the longest zero-run.

---

## Q2 – Finding the /64 Prefix

**Question**

> What is the prefix associated with the IPv6 address  
> `2001:DB8:D15:EA:CC44::1/64`?

**Correct answer**

> ✅ `2001:DB8:D15:EA::/64`

**Why this is correct**

- A `/64` prefix means the **first 64 bits** (first **four hextets**) are the
  network prefix.
- The address is:

  ```text
  2001:DB8:D15:EA:CC44::1
  ^^^^ ^^^^ ^^^^ ^^^^
   1    2    3    4   → prefix
  ```

- So the prefix is `2001:DB8:D15:EA::/64`.

**Concept check**

- IPv6 uses **prefix notation** only (no dotted masks).  
- For `/64`, always take the **first four hextets** as the network part.

---

## Q3 – Address Automatically Assigned When IPv6 Is Enabled

**Question**

> What type of address is automatically assigned to an interface when IPv6
> is enabled on that interface?

**Correct answer**

> ✅ **Link-local**

**Why this is correct**

- Every IPv6-enabled interface **must** have a **Link-Local Address (LLA)**.
- OSes and routers **auto-generate** an LLA in the `FE80::/10` range when IPv6
  is enabled.
- Global unicast, unique local, or loopback addresses are **not** automatically
  assigned in the same way.

**Concept check**

- LLAs (`FE80::/10`) are:
  - Used for **local-link** communication (e.g. host ↔ default gateway).
  - **Not routable** off the local segment.
  - Always present on IPv6 interfaces.

---

## Q4 – Non-Routable, Local-Link Only Prefix

**Question**

> Which IPv6 network prefix is only intended for local links and cannot be routed?

**Correct answer**

> ✅ `FE80::/10`

**Why this is correct**

- `FE80::/10` is the **link-local unicast** range. Packets with a link-local
  source or destination must **never be forwarded** by routers.
- The other options mean:
  - `FF00::/12` – IPv6 **multicast**.
  - `2001::/3` – Global Unicast (Internet-routable).
  - `FC00::/7` – Unique Local (RFC 4193 “private” style, but can be routed
    internally).

**Concept check**

- If you see `fe80:` at the start, think **link-local, single link only**.

---

## Q5 – Purpose of `ping ::1`

**Question**

> What is the purpose of the command `ping ::1`?

**Correct answer**

> ✅ It tests the **internal configuration of an IPv6 host**.

**Why this is correct**

- `::1` is the **IPv6 loopback** address (equivalent to IPv4 `127.0.0.1`).
- A successful `ping ::1` proves:
  - The IPv6 stack is **installed and working** on that host.
  - The network interface card or cabling are **not** involved in this test.
- It does *not* check:
  - Default gateway reachability,
  - Multicast to all hosts,
  - External connectivity.

**Concept check**

- Loopback tests the **local TCP/IP stack**, not the network.

---

## Q6 – Extracting the Interface ID

**Question**

> What is the interface ID of the IPv6 address  
> `2001:DB8::1000:A9CD:47FF:FE57:FE94/64`?

**Correct answer**

> ✅ `A9CD:47FF:FE57:FE94`

**Why this is correct**

1. Expand the address:

   - Before `::`: `2001:DB8`
   - After `::`: `1000:A9CD:47FF:FE57:FE94`

   We need a total of **8 hextets**, so `::` represents **one** all-zero hextet:

   ```text
   2001:DB8:0000:1000:A9CD:47FF:FE57:FE94
   ```

2. `/64` prefix → first four hextets are the **network part**:

   ```text
   Network:      2001:DB8:0000:1000
   Interface ID: A9CD:47FF:FE57:FE94
   ```

**Concept check**

- For `/64`:
  - **Network** = hextets 1–4
  - **Interface ID** = hextets 5–8

---

## Q7 – Network Address for a /64

**Question**

> What is the network address for the IPv6 address `2001:DB8:AA04:B5::1/64`?

**Correct answer**

> ✅ `2001:DB8:AA04:B5::/64`

**Why this is correct**

- A `/64` network covers all addresses where the **first four hextets** are the
  same.
- The host address is:

  ```text
  2001:DB8:AA04:B5::1
  ```

- Zero out the interface ID to get the **network address**:

  ```text
  2001:DB8:AA04:B5::/64
  ```

**Concept check**

- IPv6 network address = **prefix with host bits all zero**, same principle as IPv4.

---

## Q8 – Address Type Not Supported in IPv6

**Question**

> Which address type is **not** supported in IPv6?

**Correct answer**

> ✅ **Broadcast**

**Why this is correct**

- IPv6 uses **multicast** instead of broadcast.
  - Example: `FF02::1` (all-nodes), `FF02::2` (all-routers).
- IPv6 supports:
  - **Unicast** (global, link-local, unique local, loopback, etc.)
  - **Multicast**
  - **Anycast** (covered earlier in the module)
- There is **no broadcast address** in IPv6.

**Concept check**

- If an exam question says “broadcast in IPv6,” the correct mental response is:
  > *“IPv6 doesn’t do broadcast; it uses multicast groups instead.”*

---

## Q9 – Meaning of a Successful `ping ::1`

**Question**

> What is indicated by a successful ping to the `::1` IPv6 address?

**Correct answer**

> ✅ **IP is properly installed on the host.**

**Why this is correct**

- `::1` is the **loopback** address. A successful ping shows:
  - The IPv6 protocol stack is **up and functioning**.
  - The OS can send and receive IPv6 traffic internally.
- It does **not** guarantee that:
  - The cable is plugged in,
  - The link-local address is configured,
  - The default gateway or other hosts are reachable.

**Concept check**

- Loopback ping = **sanity check for local IPv6** on that machine.

---

## Q10 – Another Compressed IPv6 Address

**Question**

> What is the most compressed representation of the IPv6 address  
> `2001:0db8:0000:abcd:0000:0000:0000:0001`?

**Correct answer**

> ✅ `2001:db8:0:abcd::1`

**Why this is correct**

1. **Rule 1 – omit leading zeros** per hextet:

   ```text
   2001:0db8:0000:abcd:0000:0000:0000:0001
   → 2001:db8:0:abcd:0:0:0:1
   ```

2. **Rule 2 – double colon** for the longest run of zero hextets (`0:0:0`):

   ```text
   2001:db8:0:abcd:0:0:0:1
   → 2001:db8:0:abcd::1
   ```

3. Other options either:
   - Leave unnecessary zeros (`0000`), or
   - Misplace the `::` so they don’t reflect the correct zero run.

**Concept check**

- Confirms mastery of **IPv6 compression rules**:
  - Apply Rule 1 first (leading zeros),
  - Then Rule 2 (single `::` for longest zero sequence).

---


## Q11 – Minimum IPv6 Configuration on a Router Interface

**Question**

> What is the minimum configuration for a router interface that is enabled for IPv6?

**Correct answer**

> **To have a link-local IPv6 address**

**Why this is correct**

- As soon as you enable IPv6 on an interface, it **must** have a **link-local address (LLA)** so it can participate in IPv6 on that local link.
- On Cisco IOS, the LLA can be:
  - **Automatically generated** (EUI-64 or randomly), or
  - **Manually configured** with `ipv6 address fe80::... link-local`.
- A **global unicast address (GUA)** is *not* strictly required for the interface to be considered IPv6-enabled. LLAs are enough for:
  - Neighbor Discovery (ND)
  - Routing protocol adjacencies
  - Local link communication (e.g., between routers on the same link)

**Why the other options are wrong**

- *“To have both a link-local and a global unicast IPv6 address”*  
  - Common in real networks, but **not the minimum requirement**.
- *“To have a self-generated loopback address”*  
  - Loopback is a **separate interface**, not a requirement for enabling IPv6 on a physical interface.
- *“To have both an IPv4 and an IPv6 address”*  
  - Dual-stack (IPv4 + IPv6) is optional. An interface can be **IPv6-only**.

**Concept check**

If a router interface only has `FE80::1` configured as a link-local and no GUA, is it IPv6-enabled?  
✅ **Yes.** It can still use IPv6 on that link (for routing protocols, neighbor discovery, etc.).

---

## Q12 – Minimum IPv6 Address Required on an Interface

**Question**

> At a minimum, which address is required on IPv6-enabled interfaces?

**Correct answer**

> **Link-local**

**Why this is correct**

- This is the same core idea as Q11 but asked more directly.
- Every IPv6-enabled interface **must** have a **link-local address**:
  - Used as the **source** for a lot of control-plane traffic (ND, RA/RS, routing protocols).
  - Always in the **FE80::/10** range.
- GUAs, ULAs, or other addresses are built **on top** of that requirement.

**Why the other options are wrong**

- **Unique local** – `FC00::/7` scope is within a site, but not strictly required.
- **Global unicast** – Needed for Internet/global reachability, but not required just to enable IPv6.
- **Site local** – Deprecated; replaced by **unique local addresses (ULAs)**.

**Concept check**

If you see only `FE80::...` on an interface and no GUA/ULA, that interface is still **validly IPv6-enabled**.

---

## Q13 – Structure of an IPv6 Global Unicast Address (Choose Three)

**Question**

> What are three parts of an IPv6 global unicast address? (Choose three.)

**Correct answers**

- ✅ **An interface ID that is used to identify the local host on the network**
- ✅ **A global routing prefix that is used to identify the network portion of the address that has been provided by an ISP**
- ✅ **A subnet ID that is used to identify networks inside of the local enterprise site**

**IPv6 GUA structure reminder**

An IPv6 global unicast address is typically structured as:

- **Global Routing Prefix** – Assigned by the ISP; identifies your organization by the rest of the Internet.
- **Subnet ID** – Used by the organization to create internal subnets.
- **Interface ID** – Identifies the specific host/interface on that subnet.

So it’s:

> `global routing prefix` + `subnet ID` + `interface ID`

**Why the other options are wrong**

- *“An interface ID that is used to identify the local network for a particular host”*  
  - Interface ID identifies the **host**, *not* the network.
- *“A global routing prefix that is used to identify the portion of the network address provided by a local administrator”*  
  - The global routing prefix is **provided by the ISP**, not normally by the local admin.  
  - The local admin controls the **subnet ID** portion inside that prefix.

**Concept check**

If you see `2001:DB8:130F:0001::1/64`:

- `2001:DB8:130F` → global routing prefix (ISP-assigned).
- `0001` → subnet ID (your internal subnet).
- `::1` → interface ID (the host on that subnet).

---

## Q14 – Bits Available for /64 Subnets from a /48 Prefix

**Question**

> Your organization is issued the IPv6 prefix of `2001:db8:130f::/48` by your service provider.  
> With this prefix, how many bits are available for your organization to create `/64` subnetworks if interface ID bits are not borrowed?

**Correct answer**

> **16 bits**

**How to think about it**

- A standard IPv6 LAN uses a **/64**:
  - 64 bits for **network (prefix)**  
  - 64 bits for **interface ID**
- The ISP gave you a **/48**:
  - First 48 bits are fixed as your **global routing prefix**.
- To get to `/64`, you need:

> `64 (desired prefix length) – 48 (given prefix length) = 16 bits`

Those extra **16 bits** between /48 and /64 are used as the **Subnet ID** field.

**What this means in practice**

- You can create:

> `2^16 = 65,536` different `/64` subnets

- Address block example:

> `2001:DB8:130F:0000::/64` up to `2001:DB8:130F:FFFF::/64`

**Concept check**

Whenever you see a question like *“Given a /X and you want /64, how many bits for subnetting?”* → just compute `64 - X`.

---

## Q15 – IPv6 Address Used Only on a Single Subnet

**Question**

> Which type of IPv6 address is not routable and used only for communication on a single subnet?

**Correct answer**

> **Link-local address**

**Why this is correct**

- **Link-local addresses**:
  - Are always in the `FE80::/10` range.
  - Are **never forwarded by routers** – they exist only on the local link.
  - Are used for:
    - Neighbor Discovery (ND)
    - Router discovery (RS/RA)
    - Forming routing protocol adjacencies
- They are specifically designed for **single-link communication** and are **not routable** beyond that link.

**Why the other options are wrong**

- **Unspecified address (`::`)**  
  - Used internally by a host during initialization (e.g., before it gets an address). Not assigned to interfaces for data communication.
- **Loopback address (`::1`)**  
  - Used for local host testing (“ping yourself”), not for link communication with other nodes.
- **Unique local address**  
  - `FC00::/7` range. Not globally routable on the Internet, but **can be routed between internal subnets**.
- **Global unicast address**  
  - Globally routable on the IPv6 Internet.

**Concept check**

If you see traffic sourced from `FE80::...`, it will **never be routed off that local link**. If you see `2001:DB8::...` or `FDxx::...`, it **can** be routed (globally or inside the site).


## How This Section Helps Recruiters

- Demonstrates not just memorized answers but:
  - Correct usage of **IPv6 compression rules**.
  - Understanding of **prefix lengths**, **interface IDs**, and **network addresses**.
  - Clear grasp of **link-local vs global**, **loopback**, and **address types**.
- Shows I can:
  - Read an exam-style question,
  - Extract the relevant concept,
  - And explain *why* a given choice is correct or incorrect.



## Final Summary (for my CV / LinkedIn)

> **IPv6 Addressing (CCNA Module 12)**  
> I’ve designed and implemented IPv6 addressing schemes in Packet Tracer and
> lab environments: carving /64 LANs out of a /48 prefix, assigning GUAs and
> LLAs on routers, switches, and hosts, and enabling dual‑stack routing with
> SLAAC and DHCPv6. I regularly validate configurations with `show ipv6
> interface brief`, `show ipv6 route`, `ping`, and `traceroute` and I’m
> comfortable explaining IPv6 address formats, multicast groups, and subnet
> calculations in interviews.


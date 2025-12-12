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

## 12.2 IPv6 Address Representation  

> **Big idea:** IPv6 addresses are 128‑bit hex strings. We almost never write the full 32 hex digits because there are rules to shorten them safely.  

### 12.2.1 IPv6 Addressing Formats  

- IPv6 address length: **128 bits**.  
- Written as **8 groups of 16 bits** (hextets), separated by colons (`:`).  
- Each hextet = **4 hexadecimal digits** → 16 bits.  
- Hex digits are **0–9** and **a–f** (not case‑sensitive).  

**Example – preferred (full) format**  

- Binary (concept): 128 bits total.  
- Hex (preferred):  

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
| `0000:0000:0000:0000:0000:0000:0000:0001`    | `0:0:0:0:0:0:0:1`               |
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
| Preferred           | `2001:0db8:0000:0000:ab00:0000:0000:0000`                       |
| Compressed/spaces   | `2001:db8:0:0:ab00::`                                           |
| Compressed (final)  | `2001:db8::ab00:0:0:0`  **or** `2001:db8:0:0:ab00::` (leftmost) |
| Preferred           | `fe80:0000:0000:0000:0123:4567:89ab:cdef`                       |
| Compressed/spaces   | `fe80:0:0:0:123:4567:89ab:cdef`                                 |
| Compressed (final)  | `fe80::123:4567:89ab:cdef`                                      |
| Preferred           | `fe80:0000:0000:0000:0000:0000:0000:0001`                       |
| Compressed/spaces   | `fe80:0:0:0:0:0:0:1`                                            |
| Compressed (final)  | `fe80::1`                                                       |
| Preferred           | `0000:0000:0000:0000:0000:0000:0000:0001`                       |
| Compressed/spaces   | `::1`                                                           |
| Compressed (final)  | `::1` (loopback)                                                |
| Preferred           | `0000:0000:0000:0000:0000:0000:0000:0000`                       |
| Compressed/spaces   | `::`                                                            |
| Compressed (final)  | `::` (unspecified address)                                      |

**Rule‑of‑thumb summary**  

- Apply **Rule 1** first (drop leading zeros in each hextet).  
- Then apply **Rule 2** (replace the single longest run of `0` hextets with `::`).  
- You may never use more than **one** `::` in any IPv6 address.  

---

### 12.2.4 Check Your Understanding – IPv6 Address Representation  

> These are practice conversions based on the 12.2.4 activity.  
> Answers are written in lowercase, as NetAcad requires in that activity.

#### Example 1  

Preferred:  

```text
fe80:0000:0000:0000:0000:0000:0101:1111
```

- **Omit leading zeroes:** `fe80:0:0:0:0:0:101:1111`  
- **Compressed format:** `fe80::101:1111`  

#### Example 2  

Preferred:  

```text
2001:0db8:0000:0000:0000:abcd:0000:0001
```

- **Omit leading zeroes:** `2001:db8:0:0:0:abcd:0:1`  
- **Compressed format:** `2001:db8::abcd:0:1` or `2001:db8:0:0:0:abcd::1`  
  - Using the **leftmost longest zero‑run**, we normally write: **`2001:db8::abcd:0:1`**.  

#### Example 3  

Preferred:  

```text
0000:0000:0000:0000:0000:0000:0000:0000
```

- **Omit leading zeroes:** `0:0:0:0:0:0:0:0`  
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

- IPv6 also uses **prefix length notation** (`/n`) instead of dotted‑decimal masks.  
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
   - Range: **`fc00::/7`** to **`fdff::/7`**.  
   - Commonly written as `fdxx:xxxx:...`.  

6. **Embedded IPv4 addresses**  
   - Special formats used in transition mechanisms (outside main CCNA focus).  

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
  - ULAs are designed to be globally unique if generated properly (using random 40‑bit Global ID).  

Note from the course: many networks still rely mostly on GUAs + LLAs today; ULAs are less commonly implemented but may become more common over time.  

---

### 12.3.5 IPv6 GUA  

Global Unicast Addresses (GUAs):  

- Globally unique, Internet‑routable IPv6 addresses.  
- Allocated by IANA → RIRs → ISPs → organizations.  
- Current GUA allocation range: addresses with the first three bits `001`, i.e. **`2000::/3`**.  

That means:  

- Smallest current GUA block: `2000::`  
- Largest within that /3: `3fff:ffff:...`  

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
  - With `/48` global prefix and `/64` per subnet, there are **16 bits** for the Subnet ID.  
  - That gives `2^16 = 65,536` subnets, each with `2^64` addresses.  

- **Interface ID**  
  - The remaining **64 bits**, equivalent to the host portion in IPv4.  
  - Can be generated via **EUI‑64** or **random** 64‑bit value.  
  - Recommended to keep `/64` interface IDs for SLAAC compatibility.  

Design notes:  

- Some organizations get `/32` prefixes, leaving **32 bits** for Subnet ID (massive scaling).  
- In IPv6, unlike IPv4, the “all‑zeros” and “all‑ones” interface IDs are valid, not reserved for network/broadcast.  

---

### 12.3.7 IPv6 LLA  

Link‑local addresses (LLAs):  

- Address range: **`fe80::/10`** (from `fe80::` to `febf:ffff:...`).  
- Purpose: communication **only on the local link** (local network segment).  
- Every IPv6-enabled interface **must have an LLA**.  

How LLAs are used:  

- Host ↔ default‑gateway router communication on the same link.  
- Routing protocol neighbor communication between routers (e.g. OSPFv3, EIGRP for IPv6).  

LLAs can be:  

- **Statically configured**, e.g.:  

  ```text
  interface g0/0
   ipv6 address fe80::1 link-local
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
## 12.4.1 Static GUA Configuration on a Router

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

## 12.4.2 Static GUA Configuration on a Windows Host

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

## 12.4.3 Static Configuration of a Link-Local Unicast Address

**Concepts**

- Every IPv6-enabled interface **must** have a **Link-Local Address (LLA)**:
  - Scope: only the **local link** (LAN segment).  
  - Prefix: `FE80::/10` (e.g. `fe80::1:1`).  
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

- R1 G0/0/0 – `fe80::1:1`  
- R1 G0/0/1 – `fe80::2:1`  
- R1 S0/1/0 – `fe80::3:1`  

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

## 12.4.4 Syntax Checker – GUA and LLA Static Configuration

This section walks through configuring **both** LLAs and GUAs on all R1 interfaces.

### Task summary

For each interface:

1. Enter interface config mode.  
2. Configure the LLA with the `link-local` keyword.  
3. Configure the GUA with prefix `/64`.  
4. `no shutdown` to bring the interface up.  
5. `exit` back to global config.

### Final working configuration (from the activity)

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

When this is done, the activity reports:  
> *“You successfully configured IPv6 GUAs on the interfaces of router R1.”*

**What this proves (for recruiters)**

- I can configure **dual IPv6 addresses per interface** (LLA + GUA).  
- I understand which commands are needed to actually **activate** the interface
  and make the addresses usable.

---

## 12.4.5 Packet Tracer – Basic Device Configuration

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

## 12.5.1 RS and RA Messages

**ICMPv6 RS (Router Solicitation)**

- Sent **by hosts** to the *all‑routers* multicast address.
- Purpose: “Hi routers, I need addressing information.”
- Triggers routers to reply sooner with an RA instead of waiting for the periodic timer.

**ICMPv6 RA (Router Advertisement)**

- Sent **by IPv6 routers** (typically every ~200 seconds) out router interfaces to the *all‑nodes* multicast address.
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

## 12.5.2 Method 1 – SLAAC

**SLAAC = Stateless Address Autoconfiguration.**

- Host receives RA with:
  - **Prefix** (e.g. `2001:db8:acad:1::/64`)
  - **Prefix length** (`/64`)
  - **Default gateway** (router’s LLA, e.g. `fe80::1`)
- Host **creates its own Interface ID**:
  - Using **EUI‑64** OR
  - A **random 64‑bit number** (privacy extension)
- Final GUA example:

  ```text
  2001:db8:acad:1:fc99:47ff:fe75:cee0/64
  ```

- No DHCPv6 server needed; there is no central lease database (stateless).

---

## 12.5.3 Method 2 – SLAAC and Stateless DHCPv6

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

## 12.5.4 Method 3 – Stateful DHCPv6

- Similar idea to **DHCP for IPv4**.
- RA tells the host to use **stateful DHCPv6**:
  - “I’m your default gateway, but get your IPv6 address and other info from the DHCPv6 server.”
- Host sends a **DHCPv6 Solicit** to find a server.
- Stateful DHCPv6 server:
  - Allocates the **GUA** and keeps a **list of which host has which IPv6 address**.
  - Also supplies **DNS servers, domain, etc.**
- The **default gateway** address still comes from the **RA**, not from DHCPv6.

---

## 12.5.5 EUI‑64 Process vs Randomly Generated Interface IDs

When a host uses SLAAC (Method 1 or 2), it must generate the **Interface ID** (last 64 bits). Two options:

### Option 1 – EUI‑64 (based on MAC address)

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

### Option 2 – Random 64‑bit Interface ID (Privacy Extensions)

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

## 12.5.8 Check Your Understanding – Dynamic Addressing for IPv6 GUAs

> **Question 1** – True or False?  
> RA messages are sent to all IPv6 routers by hosts requesting addressing information.

- **Correct answer:** `False`  
  - **RS** (Router Solicitation) messages are sent by **hosts** to **routers** to request addressing info.  
  - **RA** (Router Advertisement) messages are sent by **routers** to **hosts** with the addressing details.

(Other quiz questions will be added here as I encounter them.)

---

## Quick Comparison Table

| Method | Who creates the GUA?        | Where does host get prefix + default gateway? | Extra info source (DNS etc.) | Central lease DB? |
|-------|------------------------------|-----------------------------------------------|------------------------------|-------------------|
| 1 – SLAAC | Host (EUI‑64 or random IID) | RA (router)                                   | None                         | No (stateless)    |
| 2 – SLAAC + Stateless DHCPv6 | Host (EUI‑64 or random IID) | RA (router)                                   | Stateless DHCPv6 server      | No (stateless)    |
| 3 – Stateful DHCPv6 | DHCPv6 server                | RA (router) – default gateway only            | Same stateful DHCPv6 server  | Yes (stateful)    |

---



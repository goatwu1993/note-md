---
title: "TCP/IP cheatsheet"
date: 2018-05-11T11:29:21+08:00
draft: false
tags: [networking]
slug: OSI-7-Layres
---

## OSI 7 Layres

- Application Layer (Layer 7)
  - HTTP, HTTPS
  - L7 firewall
- Presentation Layer (Layer 6)
- Session Layer (Layer 5)
  - Sessions
- Transport Layer (Layer 4)
  - TCP, UDP, SCTP, TLS
- Network Layer (Layer 3)
  - IP Address
  - Router, Layer 3 Switch
- Data Link Layer (Layer 2)
  - Ethernet, 802.11(Wi-Fi), MAC Address
  - Layer 2 Switch
- Physical Layer (Layer 1)
  - Hub, Wire, Fiber, Radio

## TCP/IP protocols

- HTTP
  - Hyper Text Transport Protocol
  - TCP Port 80
- HTTPS
  - Hyper Text Transport Protocol Secure
  - TCP Port 443
- FTP
  - File Transfer Protocol
  - TCP Port 21
- Telnet
  - Telecommunication Protocol
  - TCP Port 23
- SMTP
  - Simple Mail Transfer Protocol
  - TCP port 25
  - For email
- DNS
  - Domain Name System
  - UDP Port 53
  - [Some famous public DNS servers](https://www.lifewire.com/free-and-public-dns-servers-2626062)
- TFTP
  - Trivial File Transfer Protocol
  - UDP port 69
  - Not secure. Should only be used in private net.
- RADIUS
  - Remote Authentication Dial-In User Service
  - UDP Port : 1812 (authentication) & 1813(accounting)
  - Code
    - Access-Request
    - Access-Accept
    - Access-Reject
    - Access-Challenge

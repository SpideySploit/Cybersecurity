# Networking Fundamentals Cheatsheet (Week 1)

## 1. OSI Reference Model
| Layer | Name | PDU | Core Function / Scope | Key Protocols |
|-------|------|-----|-----------------------|---------------|
| 7 | Application | Data | User interface & service access | HTTP, HTTPS, DNS, SSH, FTP |
| 6 | Presentation | Data | Encoding, encryption, compression | TLS/SSL, ASCII, JPEG |
| 5 | Session | Data | Session establishment & teardown | NetBIOS, RPC, Sockets |
| 4 | Transport | Segment | End-to-end reliability, port multiplexing | TCP, UDP |
| 3 | Network | Packet | Logical addressing & route selection | IPv4, IPv6, ICMP, ARP |
| 2 | Data Link | Frame | Local delivery via MAC, switching | Ethernet, 802.11 Wi-Fi |
| 1 | Physical | Bits / Signal | Media transmission (cables, RF) | RJ-45, Fiber, Radio Waves |

---

## 2. Transport Protocol Mechanics
- TCP (Connection-Oriented): Reliable transport protocol using a 3-way handshake (SYN -> SYN-ACK -> ACK), sequence tracking, and retransmissions. Returns RST on closed ports.
- UDP (Connectionless): Lightweight, fire-and-forget protocol with no handshake or retransmission logic. Used where lower latency is preferred over packet guarantees (DNS queries, VoIP, live streaming).

---

## 3. Core Ports
- SSH: TCP 22 (Encrypted remote CLI access)
- DNS: UDP/TCP 53 (Domain name resolution)
- HTTP: TCP 80 (Cleartext web traffic)
- HTTPS: TCP 443 (TLS-encrypted web traffic)
- SMB: TCP 445 (File sharing and Windows IPC)

---

## 4. IPv4 Subnetting
- Usable Host Formula: 2^(32 - prefix) - 2
- /24 Subnet: 8 host bits -> 256 total addresses, 254 usable hosts.
- /28 Subnet: 4 host bits -> 16 total addresses, 14 usable hosts.
- Reserved IPs: Network ID (all host bits 0) and Directed Broadcast (all host bits 1).

---

## 5. DNS Hierarchy & Resolution
- Record Types:
  - A: Maps hostname to IPv4 address.
  - AAAA: Maps hostname to IPv6 address.
  - PTR: Maps IPv4/IPv6 address to hostname (reverse lookup).
  - CNAME: Maps an alias to a canonical domain name.
- Resolution Order: Local DNS Cache -> Local hosts file -> Configured Resolver -> Root/TLD Hierarchy.
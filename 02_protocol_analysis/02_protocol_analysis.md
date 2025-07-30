# 02 — Protocol Analysis

---

## Scenario

In this module, I examined captured network traffic to analyze individual protocols in depth. The goal was to better understand how legitimate protocols behave at a packet level and how attackers can abuse them. I focused on DNS, HTTP, and TCP — three commonly used protocols that often appear in both normal and malicious traffic.

---

## What I Did

- Applied protocol-specific filters in Wireshark to isolate and inspect:
  - DNS queries and responses (including NXDOMAINs)
  - HTTP GET requests using curl
  - TCP handshakes between source and destination IPs
- Used "Follow UDP/TCP Stream" and expert packet views to explore structure and intent
- Took screenshots of key packet interactions for documentation and analysis

---

## What I Learned

- DNS responses containing `NXDOMAIN` are flagged by Wireshark and can indicate suspicious beaconing or typosquatting attempts.
- HTTP requests made via `curl` are clearly identifiable by the `User-Agent` and provide full visibility into requested URIs and headers.
- TCP handshakes can be tracked using SYN, SYN/ACK, and ACK flags — helping differentiate between completed, half-open, or failed sessions.
- Even basic Wireshark filters (e.g., `dns`, `http`, `tcp.flags.syn == 1`) can quickly surface anomalous or attacker-controlled behavior.

---

## Why It Matters

Understanding how protocols look "on the wire" is essential for any SOC analyst or blue teamer. This module helped reinforce how attackers use normal-looking packets for malicious purposes — and how to detect that misuse. By practicing protocol-level inspection, I gained deeper insight into detecting abnormal behavior, tuning IDS signatures, and writing better detection rules.

---

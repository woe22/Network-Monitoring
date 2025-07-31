# 06 — Defensive Takeaways

---

## Scenario

This module serves as a final reflection on the Network Monitoring & Traffic Analysis lab. The goal is to extract practical defensive insights from the tools and techniques used throughout the lab and to summarize how these skills apply to real-world SOC environments.

---

## What I Did

Over the course of this lab, I completed the following:

- Captured live network traffic using `tcpdump`
- Analyzed `.pcap` files with Wireshark
- Processed captured traffic using Zeek for log generation
- Deployed Suricata to perform real-time intrusion detection
- Mapped Zeek-observed behaviors to MITRE ATT&CK techniques

Throughout the process, I performed hands-on analysis with raw packet data, high-level protocol views, and detection rules.

---

## What I Learned

The most useful tools in this lab were:

- `tcpdump`: Provided precise, CLI-based traffic capture
- `Wireshark`: Offered deep packet inspection and filtering
- `Suricata`: Enabled detection of known threats and rule-based alerts

These tools formed the foundation of my network visibility stack. Although there were no singular “aha” moments, I gained consistent exposure to how data flows across the wire and how security tools interpret and report on that activity.

---

## Why It Matters

The ability to monitor, capture, and analyze network traffic is foundational for any SOC analyst. This lab helped me practice skills that directly translate to the daily work of a defender:

- Identifying suspicious domains and ports
- Recognizing patterns in connection attempts
- Mapping observed activity to adversary techniques
- Using tools like Zeek and Suricata to surface and enrich alerts

Everything I practiced in this lab can be applied in a professional SOC setting, contributing to faster detection, better threat hunting, and stronger incident response.

---

# 01 — Network Traffic Capture

---

## Scenario

In this module, I acted as both attacker and analyst on a Kali Linux VM to simulate and capture suspicious network traffic. The goal was to produce realistic data that could be analyzed for signs of malicious behavior. Traffic included DNS beacons to nonexistent domains, attempted HTTP file downloads, and TCP handshake analysis — all typical of early-stage attacker behavior or malware communication attempts.

---

## What I Did

```bash
# Started packet capture with tcpdump
sudo tcpdump -i eth0 -w suspicious_traffic.pcap

# Simulated suspicious DNS behavior
for i in {1..10}; do nslookup fake$i.evil-domain.com; sleep 1; done

# Simulated HTTP request to mimic payload download
curl http://example.com/fake.exe

# (Optional) Ran a port scan or SSH brute force simulation (if response is available)
nmap -sS 10.0.2.1-254
```

- Captured all of the above traffic in a `.pcap` file
- Reviewed the capture using Wireshark with filters such as:
  - `dns`
  - `http`
  - `tcp.flags.syn == 1`

---

## What I Learned

- DNS queries to non-existent domains trigger `NXDOMAIN` responses or no response at all, often highlighted as warnings in Wireshark.
- TCP SYN and SYN-ACK packets reveal handshake attempts that can suggest scanning or outbound command-and-control activity.
- Basic `curl` requests to external servers are clearly visible in HTTP streams, and can simulate malware download attempts.
- Wireshark's filtering and "Follow Stream" features are powerful for isolating and inspecting specific interactions.

---

## Why It Matters

Being able to identify and interpret suspicious traffic in packet captures is a foundational blue team skill. Many initial 

---

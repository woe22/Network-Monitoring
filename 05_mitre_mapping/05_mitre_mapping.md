# 05 — MITRE Mapping

---

## Scenario

After capturing and analyzing network traffic using `tcpdump` and Zeek, I needed to classify the observed behaviors using the MITRE ATT&CK framework. The goal was to simulate how a SOC analyst or detection engineer would interpret network activity and align it with known adversary tactics, techniques, and procedures (TTPs).

---

## What I Did

I began by capturing network traffic with `tcpdump`:

```bash
sudo tcpdump -i eth0 -w new_traffic.pcap
```

I then processed the `.pcap` file using Zeek in a Docker container with checksum verification disabled:

```bash
sudo docker run \
  -v ~/zeek_logs:/logs \
  -v ~/new_traffic.pcap:/logs/input.pcap \
  -w /logs \
  zeek/zeek \
  zeek -C -r input.pcap
```

After processing, I reviewed the logs written to the `~/zeek_logs` directory:

```bash
ls ~/zeek_logs/*.log
```

From the logs, I identified the following activity:

- DNS lookups for domains like `example.com`, `fake.example.com`, and `fake1.evil.com`
- TCP SYN connections to port 80 (HTTP)
- HTTP requests initiated by the system (simulated via curl or browser)

I used these observations to map relevant MITRE ATT&CK techniques.

---

## What I Learned

By interpreting the data in the Zeek logs, I was able to map the following behaviors to MITRE techniques:

| Observed Behavior                    | MITRE Technique                              | ID          |
|-------------------------------------|-----------------------------------------------|--------------|
| DNS queries for external domains    | Application Layer Protocol: DNS               | T1071.004    |
| TCP connections to HTTP (port 80)   | Application Layer Protocol: Web Protocols     | T1071.001    |
| Simulated file download or staging  | Ingress Tool Transfer                         | T1105        |

This reinforced my ability to translate low-level traffic data into a structured threat intelligence framework. Even in a small-scale capture, adversary-like behaviors can be identified and documented using industry standards like MITRE.

---

## Why It Matters

Understanding how to map observed behaviors to MITRE techniques is a core skill for SOC analysts, threat hunters, and detection engineers. It allows teams to:

- Communicate threats in a standardized format
- Build detections that align with adversary TTPs
- Develop a threat-informed defense strategy

This module helped me practice analyzing benign but realistic traffic and connect it to potential attacker behavior. The ability to recognize and document these patterns is essential in any blue team role.

---

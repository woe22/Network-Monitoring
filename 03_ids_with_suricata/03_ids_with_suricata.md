# 03 — IDS with Suricata

---

## Scenario

In this module, I used Suricata to process previously captured suspicious network traffic. The goal was to simulate how a SOC analyst might use an IDS to detect abnormal or potentially malicious behavior in packet captures. Suricata was run in offline mode against the PCAP and logged structured alerts that could later be reviewed manually or ingested into a SIEM.

---

## What I Did

```bash
# Installed Suricata
sudo apt update
sudo apt install suricata -y

# Created an output directory for logs
mkdir output

# Ran Suricata in offline mode against suspicious_traffic.pcap
sudo suricata -r suspicious_traffic.pcap -l output/

# Viewed human-readable alerts
cat output/fast.log

# Parsed JSON logs with jq
sudo apt install jq -y
cat output/eve.json | jq '.alert'
```

- Installed and configured Suricata
- Processed a packet capture from previous modules
- Analyzed alerts in both `fast.log` and `eve.json`
- Collected screenshots of structured detection output

---

## What I Learned

- Suricata can detect protocol anomalies like UDP checksum mismatches even without custom rule tuning
- `fast.log` gives a quick analyst-friendly view, while `eve.json` is ideal for pipelines and structured alerting
- Basic IDS alerts provide critical entry points for deeper investigation and correlation
- `jq` is a useful utility for filtering and extracting Suricata alert fields in JSON

---

## Why It Matters

Suricata is a powerful open-source IDS/IPS engine used in real-world SOC environments. Knowing how to run it against raw packet captures and interpret alerts helps reinforce threat detection workflows. This module provided a practical look at how analysts transition from network activity to actionable detection — a fundamental blue team skill.

---

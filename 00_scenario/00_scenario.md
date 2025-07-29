# 00 — Scenario and Lab Setup

---

🧠 Scenario  
This lab focuses on simulating the responsibilities of a SOC analyst by capturing and analyzing suspicious network traffic in a controlled virtual environment. The goal is to emulate real-world network threats such as lateral movement, data exfiltration, unauthorized access, and malware communication. The lab is structured to observe this behavior in live packet captures and translate findings into defensive insights.

---

🎯 Objective  
To build foundational blue team capabilities by:

- Capturing and inspecting suspicious network traffic
- Identifying anomalies and extracting indicators of compromise (IOCs)
- Correlating observed behavior to MITRE ATT&CK techniques
- Developing comfort with SOC-relevant packet capture and analysis tools

---

💻 Lab Environment  

| Component       | Details                                         |
|----------------|--------------------------------------------------|
| Analyst VM     | Kali Linux (Wireshark, tcpdump, Suricata, Zeek) |
| Target Machine | Simulated attacker/suspicious host (if needed)  |
| Capture Tools  | tcpdump, Wireshark                              |
| Detection Tools| Suricata, Zeek                                  |

---

🔐 Threat Simulation Summary  
The lab will simulate suspicious activities such as:

- Unauthorized remote access attempts (e.g., SSH or RDP probes)
- Malicious DNS requests or HTTP connections to suspicious hosts
- Simulated data exfiltration (e.g., large outbound transfers)
- Unusual port scanning or service discovery traffic

Traffic will be intentionally crafted or generated to trigger attention in monitoring tools, offering real-world defensive training opportunities.

---

🛡 Blue Team Focus  
This lab strengthens the following skills:

- Packet-level inspection and analysis
- Intrusion detection using Suricata
- Protocol behavior awareness (HTTP, DNS, TCP/UDP patterns)
- Threat detection and MITRE technique identification
- Documentation of network anomalies and IOCs

---

⚠️ Disclaimer  
This lab is intended solely for ethical, educational purposes in a contained virtual environment. All simulated threat behaviors are conducted without external connectivity. The goal is to reinforce blue team defensive skills through hands-on exposure to real-world tactics in a safe setting.

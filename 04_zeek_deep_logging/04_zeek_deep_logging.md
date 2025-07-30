# 04 — Zeek Deep Logging

---

## Scenario

The purpose of this module was to enrich our network‑forensics workflow by processing the **suspicious / new traffic PCAP** with **Zeek**. Unlike Suricata, Zeek produces extensive metadata logs (`conn.log`, `dns.log`, `http.log`, etc.) that are ideal for threat‑hunting, timeline reconstruction, and ATT&CK mapping.

---

## What I Did

```bash
# 1. Captured traffic that included DNS and HTTP activity
sudo tcpdump -i eth0 -w new_traffic.pcap

# 2. Pulled the official Zeek Docker image and ran it in checksum‑ignore mode
sudo docker run -v $HOME:/pcap zeek/zeek zeek -C -r /pcap/new_traffic.pcap

# 3. Verified log output — nothing appeared at first ➜ began troubleshooting
#    a) Confirmed PCAP contents with tcpdump (DNS & SYN packets present)
#    b) Observed checksum‑offloading warnings
# 4. Forced Zeek to write logs to a dedicated directory
mkdir -p ~/zeek_logs
sudo docker run   -v ~/zeek_logs:/logs -w /logs   -v ~/new_traffic.pcap:/logs/input.pcap   zeek/zeek zeek -C -r input.pcap
```

### ✔️ Resulting Logs

| Log File  | Entries | Purpose                                     |
|-----------|---------|---------------------------------------------|
| `conn.log`|   38    | Summaries of each TCP/UDP flow              |
| `dns.log` |    5    | Queries for `example.com` and `fake.example.com` |
| `http.log`|    1    | `GET /fake.exe` request (curl simulation)   |

Screenshots of key log lines have been saved to:

```
/04_zeek_deep_logging/visuals/
├── zeek_conn_log.png
├── zeek_dns_log.png
└── zeek_http_log.png
```

---

## Troubleshooting Highlights

1. **NIC Checksum Off‑loading**  
   *Initial runs produced no logs because packets failed checksum validation.*  
   **Fix:** Added `-C` to ignore invalid checksums.

2. **Log Path Confusion**  
   Logs were written inside the container’s working directory, not the host.  
   **Fix:** Used `-v ~/zeek_logs:/logs` and `-w /logs` to bind and set the CWD.

3. **Minimal Traffic**  
   Early PCAPs contained only ARP packets, which Zeek ignores.  
   **Fix:** Re‑captured traffic with confirmed DNS lookups and an HTTP request.

---

## What I Learned

* Zeek requires **complete protocol events** to generate logs; SYN floods or ARP chatter alone won’t suffice.  
* Virtual NICs often enable **checksum off‑loading** by default, which can silently drop packets from analysis tools.  
* Containerising NSM tools demands careful volume mounts (`-v`) and working‑directory control (`-w`) to retrieve artifacts.

---

## Why It Matters

Zeek’s metadata logs offer unparalleled visibility for blue‑team operations. By successfully generating and reviewing `conn.log`, `dns.log`, and `http.log`, I now have:

* Session‑level context for every connection in the capture  
* Extracted domains, URIs, and user‑agents for IOC mapping  
* A repeatable, containerised workflow that dovetails with Suricata alerts

This completes the deep‑logging objective and sets the stage for **`05 — MITRE Mapping`**, where Zeek and Suricata outputs will be correlated to ATT&CK techniques.

---

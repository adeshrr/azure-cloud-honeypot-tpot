# Cloud Honeypot on Azure using T-Pot

This project documents the deployment of a **cloud-based honeypot environment** using **T-Pot** on an **Azure Virtual Machine**. The goal was to monitor and analyze real-world cyberattacks by collecting logs and traffic data from a variety of honeypot services.

---

## Tools & Technologies Used

- **Azure VM (Ubuntu)** – Hosted the T-Pot honeypot environment.
- **T-Pot** – A comprehensive honeypot platform that includes several honeypot services.
- **Kibana** – Used to visualize logs and network activity.
- **Elasticsearch & Logstash** – Managed and processed log data for analysis.

---

## Project Objective

To set up a publicly accessible honeypot in a cloud environment to attract, capture, and study malicious traffic, understand attacker behavior, and identify commonly targeted services and ports.

---

## Setup Summary

1. Provisioned an Azure Virtual Machine (Standard\_B1s – free tier eligible).
2. Downloaded and mounted the official T-Pot ISO image.
3. Completed the T-Pot installation using guided setup.
4. Opened required ports through Azure Network Security Groups.
5. Enabled data visualization through Kibana’s web interface.

---

## Honeypot Services Capturing Data

| Service       | Protocols Emulated   | Observation       |
| ------------- | -------------------- | ----------------- |
| Cowrie        | SSH, Telnet          | High interaction  |
| Honeytrap     | Generic TCP/UDP      | High volume       |
| Sentrypeer    | SIP (VoIP)           | Region-specific   |
| Dionaea       | SMB, FTP, HTTP       | Malware samples   |
| RedisHoneypot | Redis                | Moderate hits     |
| Mailoney      | SMTP                 | Low interaction   |
| ADBHoney      | Android Debug Bridge | Targeted attempts |
| Conpot        | ICS/SCADA            | Rare attempts     |

> Cowrie and Honeytrap logged the majority of incoming traffic, showing common attacker interest in Telnet and SSH.

---

## Geographic Attack Distribution

- Majority of malicious traffic came from Europe, the U.S., and Southeast Asia.
- Frequent sources included cloud-hosted environments, likely part of automated botnets.
- SIP-based attacks were especially common from Europe.

> Notably, IPs from Poland generated a large number of VoIP attacks.

---

## Dashboard Highlights (via Kibana)

- **Total Attacks Captured**: \~27,000
- **Common Ports Targeted**:
  - 5060 (SIP)
  - 22 (SSH)
  - 23 (Telnet)
  - 80 (HTTP)
- **Top Attack Services**: Cowrie, Honeytrap, Sentrypeer
- **Attack Timeline**: Spikes during early morning hours, indicating automation

---

## Screenshots

Screenshots related to dashboard and attack data:

- `kibana_dashboard.png`
- `cowrie_activity.png`
- `port_activity.png`
- `source_ips_map.png`
- `log_volume_stats.png`

All screenshots are available in the `/screenshots/` folder.

---

## Repository Structure

```
azure-cloud-honeypot-tpot/
├── README.md
├── architecture-diagram.png
├── INSTALLATION.md
└── screenshots/
    ├── kibana_dashboard.png
    ├── cowrie_activity.png
    ├── port_activity.png
    ├── source_ips_map.png
    └── log_volume_stats.png
```

---

## Conclusion

This cloud honeypot project helped simulate a real-world environment where attackers interacted with various fake services. The collected data offers insights into active threat sources, commonly targeted ports, and global attacker trends. This type of monitoring can support early detection efforts and strengthen defensive cybersecurity strategies.


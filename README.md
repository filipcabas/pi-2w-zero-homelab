# pi-2w-zero-homelab
Optimized homelab infrastructure on Raspberry Pi Zero 2 W featuring network-wide ad-blocking (Pi-hole), recursive DNS (Unbound), secure password vault (Vaultwarden), and automated Fail2ban defense with real-time Telegram alerts.

# Self-Hosted Secure DNS & Password Management Infrastructure

A lightweight, production-ready, and highly optimized self-hosted infrastructure built on top of a **Raspberry Pi Zero 2 W**. This architecture provides network-wide ad-blocking, private recursive DNS resolution, automated threat-intelligence-backed host defense, and a secure local password management vault with real-time Telegram alerting.

---

## Architecture Overview

The system architecture seamlessly integrates networking, containerization, local storage preservation, and active system auditing to operate reliably under strict hardware limitations (512MB RAM).
+---------------------------------------+
                  |               Tailscale               |
                  |        (Secure Remote Access)         |
                  +-------------------+-------------------+
                                      |
                                      v

+------------------+         +------------+------------+         +------------------+
|  Client Devices  +-------->|         Pi-hole         +-------->|     Unbound      |
|  (Local/Remote)  |   DNS   |  (Network Ad-blocker)   |   DNS   | (Recursive DNS)  |
+------------------+         +------------+------------+         +--------+---------+
|                               |
v                               v
+------------+------------+         +--------+---------+
|       Vaultwarden       |         |   Root DNS Servers|
| (Docker Bitwarden API)  |         +------------------+
+------------+------------+
|
Logs  | (systemd-journald)
v
+------------+------------+
|        Fail2ban         |
|   (Intrusion Defense)   |
+------------+------------+
|
Trigger Action| (iptables + curl)
v
+------------+------------+
|   Telegram Alert Bot    |
|  (Instant Notification) |
+-------------------------+

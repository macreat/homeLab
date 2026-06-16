# How to Use: GCPDS Research Hub & Accelerant Agent

This document provides quick access links and operational details for the services running on the GCPDS Home Server.

##  The Innovation: Why Self-Hosted?

The **Research Accelerant Hub** represents a shift from local processing to a centralized "Research Engine":
- **Computational Offloading:** Moves heavy AI tasks (Ollama/Llama 3.1) and PDF indexing to dedicated server hardware.
- **24/7 Autonomous Pipeline:** Research sessions (Search → Extraction → Synthesis) run in the background without needing your laptop open.
- **Secure Global Access:** Leveraging **Tailscale** to bypass complex University network restrictions, providing a seamless "local" experience from anywhere.
- **Dockerized Architecture:** Ensures consistent environments across development and production, simplifying updates and maintenance.

---

##  Quick Access Dashboards

Access these links when connected to the **University Network** or **Tailscale**:

| Service | Local/IP Link | Remote (Tailscale) | Status |
| :--- | :--- | :--- | :--- |
| **CasaOS Dashboard** | [http://192.168.0.104](http://192.168.0.104) | [http://100.70.18.50](http://100.70.18.50) | ![Online](https://img.shields.io/badge/Port-80-blue) |
| **Research Agent UI** | [http://192.168.0.104:3000](http://192.168.0.104:3000) | [http://100.70.18.50:3000](http://100.70.18.50:3000) | ![Online](https://img.shields.io/badge/Port-3000-brightgreen) |

> **Pro Tip:** If Avahi is active on your machine, you can use `http://local.local` for local access.

---

##  User Credentials

Access is currently restricted to two primary user profiles:

| User Profile | Username | Access Level |
| :--- | :--- | :--- |
| **Admin** | `serveradmin` | Full `sudo` and system management. |
| **Guest/Coworker**| `coworker` | Standard access (cannot update system). |

---

##  Operational Commands

If you have SSH access, use these aliases to manage the agent:

```bash
gcpds agent start      # Start the Research Agent services
gcpds agent stop       # Stop all services
gcpds agent status     # Check health of Docker containers
```



### 2. Gemini CLI (Interactive Agent API) ( future ) 
This repository is managed and updated via the **Gemini CLI**, an AI-powered interactive agent. It allows for:
- **Autonomous Editing:** Surgical updates to the codebase and documentation.
- **Context-Aware Research:** Deep analysis of project logs and architectural patterns.
- **Verification:** Automated testing and validation of system changes.

---

*Maintained by the GCPDS Team. v0.2-1.0 Prototype Stable.*

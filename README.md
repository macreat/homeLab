# GCPDS - SELF HOSTED  Research Hub & Accelerant Agent 

![homeLab](content/imgs/server1.jpeg)

Welcome to the **GCPDS Research Hub**, a high-performance development environment and AI-powered research assistant designed for autonomous literature review and automated deployment.

---

##  Project Genesis & Design Phases

This server was built following a rigorous 6-phase infrastructure plan. We transitioned from a standard Desktop PC to a professional-grade research server by offloading heavy computational tasks to a dedicated self-hosted environment.

> **Design History:** For a detailed breakdown of the hardware setup, OS configuration, and AI stack implementation, see the [**INFRASTRUCTURE PLAN FOLLOWED**](INFRASTRUCTURE_PLAN.md).

---

##  The Innovation: Why Self-Hosted?

The **Research Accelerant Hub** represents a shift from local processing to a centralized "Research Engine":
- **Computational Offloading:** Moves heavy AI tasks (Ollama/Llama 3.1) and PDF indexing to dedicated server hardware.
- **24/7 Autonomous Pipeline:** Research sessions run in the background without needing your laptop open.
- **Secure Global Access:** Leveraging **Tailscale** to bypass complex network restrictions, providing a seamless "local" experience from anywhere.
- **Persistent API Deployment:** The core research API (Hono + tRPC) is containerized via **Docker** and bound to port **3000** of the server's IPv4 address. This transforms the tool from a local `npm run dev` script into a resilient, always-on academic utility.
- **Dockerized Architecture:** Ensures consistent environments across development and production, eliminating "it works on my machine" issues.

---

##  Innovation & Management Tool

The core engine of this hub is the _Research Accelerant Agent_. To get started, follow this **[detailed guide](howToUse.md)**, which walks you through setup, usage, and best practices.

This tool serves as the primary innovation layer, providing:
- **Autonomous Orchestration:** Automates the end-to-end research pipeline directly from the server.
- **Centralized Management:** A single, Dockerized interface for all academic and data operations.
- **Enhanced Understanding:** Deeply integrates with the server's infrastructure to provide AI-driven insights.

For the full technical breakdown and development updates, visit the official repository:
👉 [**GitHub: Macreat/ResearchAccelerantAgent**](https://github.com/macreat/ResearchAccelerantAgent)

---

##  Quick Access Dashboards

Access these links when connected to the **University Network** or **Tailscale**:

| Service | Local/IP Link | Remote (Tailscale) | Purpose |
| :--- | :--- | :--- | :--- |
| **CasaOS Dashboard** | [http://192.168.0.104](http://192.168.0.104) | [http://100.70.18.50](http://100.70.18.50) | **Storage & Management:** Set up files, manage the Data Lake, and monitor server hardware. |
| **Research Agent UI** | [http://192.168.0.104:3000](http://192.168.0.104:3000) | [http://100.70.18.50:3000](http://100.70.18.50:3000) | **API Research Tool:** Execute academic pipelines, AI synthesis, and document generation. |

###  Which link should I use?
- **Local/IP Link:** Use this when you are on the same WiFi/Ethernet as the server. It is faster and has zero latency.
- **Remote (Tailscale):** Use this when you are working from home or when the University network restricts local discovery. It provides a secure, encrypted tunnel to your hub from anywhere in the world.
- **Pro Tip:** If Avahi is active on your machine, use `http://local.local` to find the server automatically even if the IP changes.

---



##  User Credentials

Access is currently restricted to two primary user profiles:

| User Profile | Username | Access Level |
| :--- | :--- | :--- |
| **Admin** | `serveradmin` | Full `sudo` and system management. |
| **Guest/Coworker**| `coworker` | Standard access (cannot update system). |

---
*Maintained by the GCPDS Team. v0.2-1.0 Prototype Stable.*

# GCPDS & Personal Lab Home Server Setup

This manual outlines the workflow for transforming a Desktop PC into a high-performance research hub and personal deployment server. It combines the simplicity of **CasaOS** with professional tools for **Signal Processing (GCPDS)**, **AI Automation**, and **CI/CD**.


The repo is designed as a flexible infrastructure and experimentation platform for future integrations, including custom CI/CD workflows, GitHub Actions extensions, YAML-based automation pipelines, infrastructure orchestration, and scalable research or development environments.

---

## Phase 1: Hardware Preparation
*Desktop specific tweaks to ensure 24/7 reliability.*

*   **BIOS Settings:**
    *   **Virtualization:** Enable `Intel VT-x` or `AMD-V` (Critical for Docker/LLMs).
    *   **AC Power Recovery:** Set to `Always On` or `Last State` (Server restarts after power loss).
    *   **GPU Priority:** Ensure the NVIDIA GPU is in the `PCIe x16` slot.
*   **Storage Strategy:**
    *   **NVMe/SSD:** For OS and active Python/C environments.
    *   **HDD/SATA:** For the **Local Data Lake** (Datasets, DBs, and Media).

---

##  Phase 2: Base OS & Management
*Setting up the foundation.*

1.  **Install OS:** Ubuntu Server 24.04 LTS.
    *   *Tip:* During storage config, **Deselect** "Set up this disk as an LVM group" for simpler disk management.
    *   **SSH:** Select "Install OpenSSH server".
2.  **Dashboard (CasaOS):**
    ```bash
    curl -fsSL https://get.casaos.io | sudo bash
    ```
    *   Access via browser: `http://<your-server-ip>`
3.  **Update System:**
    ```bash
    sudo apt update && sudo apt upgrade -y && sudo reboot
    ```

---

##  Phase 3: Local Data Lake (The Cowork Solution)
*Stop tracking huge files in Git. Use the server as a central source of truth.*

*   **The Problem:** Cloning a repo shouldn't take hours due to large datasets or DBs.
*   **The Solution:** Host them in a shared directory (`/data/shared`) on the server.
*   **Access:**
    *   **Local:** Use Samba (available in CasaOS App Store) to map the drive to your PC/Laptop.
    *   **Remote:** Access the shared files via **Tailscale** from anywhere.
*   **Documentation:** If a file is missing in the repo, check the `SERVER_DATA.md` in your project for the server-side path.

---

##  Phase 4: Research & AI Stack

### 1. Python & C Environment
*   **Python:** Install [Miniforge](https://github.com/conda-forge/miniforge) for `conda` environments optimized for `python-gcpds`.
*   **C/C++:** `sudo apt install build-essential cmake ninja-build`.

### 2. NVIDIA Container Toolkit (GPU Power)
*Enable your GPU for Docker/ML.*
```bash
# 1. Install Drivers
sudo ubuntu-drivers autoinstall && sudo reboot

# 2. Install Toolkit
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt update && sudo apt install -y nvidia-container-toolkit

# 3. Configure Docker
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```

### 3. AI Automation (LLM)
*   **Ollama:** Run local LLMs for coding assistance and server automation.
    ```bash
    curl -fsSL https://ollama.com/install.sh | sh
    ollama run llama3 # Uses your GPU!
    ```

---

##  Phase 5: CI/CD & Personal Deployment
*Host your own "GitHub Actions" and test your personal projects.*

### 1. GitHub Actions Self-Hosted Runner
Turn your server into a worker for your personal repositories:
1.  Go to your GitHub Repo -> **Settings** -> **Actions** -> **Runners**.
2.  Click **New self-hosted runner** and follow the commands on your server.
3.  Now, every time you push code, your server will build and test it!

### 2. Personal Sandbox
*   Use CasaOS to create "Custom Docker" containers for your personal projects.
*   Deploy web apps, bots, or scripts without messing up the main research environment.

---

##  Phase 6: Connectivity (Local & Remote)
*   **Tailscale:** Access your server, files, and LLM from home or the lab salon without port forwarding.
    ```bash
    curl -fsSL https://tailscale.com/install.sh | sh
    sudo tailscale up
    ```
*   **Netdata:** (App Store) Real-time monitoring of CPU/GPU/RAM usage.

---
*Created for the GCPDS Team Cowork & Personal Lab Development.*

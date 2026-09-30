# 🏰 Bare-Metal Homelab & Hardware Fleet Architecture

> **Engineering Philosophy:** *"3xR: Reuse, Refix, Recycle — Squeeze Every Cycle."*  
> Modern software engineering often hides behind infinite cloud credits and over-provisioned Kubernetes clusters. This repository documents a resilient, production-grade 5-node bare-metal fleet built exclusively on repurposed, rescued, and thermally optimized hardware.

---

## 📊 Fleet Quick-Reference Matrix

| Node ID | Machine | Hardware Specs | Primary OS | Primary Role |
| :--- | :--- | :--- | :--- | :--- |
| **`milhy-pc`** | MILHY-PC | Intel i5-4690K (4C/4T @ 3.90GHz), 32GB DDR3, GTX 1060 6GB | MX Linux (SysVinit / XFCE) | Primary Workstation, heavy compilation, daily development & virtualization |
| **`has`** | HAS Server | Compaq Presario CQ57 (AMD E-300 APU 2C, 4GB RAM, 240GB SSD, Built-in UPS) | Debian 13 (trixie) | Central Home Automation, 25 Docker containers, Mega-Orchestrator MCP Cluster |
| **`optiplex`** | Dell OptiPlex | Intel Core 2 Quad Q9550, 16GB DDR2, 256GB SSD + 3TB HDD | Debian GNU/Linux (Headless) | Private Storage Cloud, Nextcloud, and containerized Coder development server |
| **`acer-aio`** | Acer Aspire Z5610 | Core 2 Quad Q9550, 8GB DDR3, 23" Touch AIO | Linux (Custom PowerManagement) | Bedside ambient status terminal, bedroom media streamer, and telemetry display |
| **`rpi-tv`** | RPi Dumb TV Hub | Raspberry Pi 3 Model B (4C Cortex-A53, 1GB LPDDR2, MicroSD) | Debian 13 (trixie) | Living room dumb-TV dashboard, Textual TUI / FastAPI, and go2rtc RTSP camera stream |

---

## 🖥️ Deep-Dive Node Profiles & Engineering Feats

### 1. `milhy-pc` — Primary Workstation & Daily Driver
- **The Mission:** High-throughput developer workstation, multi-monitor productivity center, and virtualization host.
- **Hardware Profile:**
  - **CPU:** Intel Core i5-4690K (Haswell 4-core, 3.50GHz base / 3.90GHz boost).
  - **RAM:** 32 GB Dual-Channel DDR3.
  - **GPU:** NVIDIA GeForce GTX 1060 6GB (Dual Fan).
  - **Storage:** NVMe/SATA SSDs for low-latency builds + bulk local storage.
  - **Monitors:** Dual-screen configuration (AOC 24B1W + Philips 223V5).
- **OS & Environment Architecture:**
  - Running **MX Linux** with **SysVinit** (deliberately chosen to eliminate systemd background bloat and preserve deterministic process scheduling).
  - Minimalist, highly responsive **XFCE** desktop tuned with custom keyboard shortcuts, custom terminal dotfiles, and dark-theme ergonomics.
  - Hosts dedicated development containers and specialized QEMU/KVM virtual machines for sandbox validation.

### 2. `has` — Home Automation Server (Compaq Presario CQ57 with Built-in UPS)
- **The Mission:** 24/7 central automation brain, network hygiene, and Model Context Protocol (MCP) gateway.
- **Hardware Profile:**
  - **Model:** Compaq Presario CQ57 Notebook PC (Hewlett-Packard).
  - **CPU:** AMD E-300 APU with Radeon HD Graphics (2 cores @ 1.30 GHz).
  - **RAM:** 4 GB DDR3.
  - **Storage:** 240 GB SSD (root system & Docker persistent volumes).
  - **OS:** Debian GNU/Linux 13 (trixie, Linux kernel 6.12).
- **The Hardware Trick (Built-in Zero-Latency UPS):** Instead of purchasing an expensive enterprise rackmount server and high-drain UPS battery unit, HAS runs on a repurposed headless laptop. The functioning internal laptop battery acts as a native, zero-cost uninterruptible power supply (UPS), completely insulating the system against grid micro-outages, brownouts, and voltage fluctuations with zero latency.
- **Production Services (25 Docker Microservices):**
  - **Home Assistant:** Central smart home automation and Zigbee/Z-Wave coordination (`ghcr.io/home-assistant/home-assistant:stable`, port 10002 -> 8123).
  - **Mega-Orchestrator MCP Gateway (port 7000) & Security Gateway (port 7080):** Multi-agent orchestrator connecting specialized MCP servers.
  - **MCP Core Microservices:** Filesystem (7001), Git (7002), Terminal (7003), Database (7004), Memory (7005), Security (7008), Config (7009), Log (7010), Advanced Memory (7012), FORAI (7016), MQTT (7019), Code Graph (7020), Marketplace (7034), Vault (7070).
  - **Data Layer:** PostgreSQL 15 (7021), Redis 7 (7022), Qdrant vector database wrapper (7026).
  - **Observability & Ingress:** Grafana (7031), Promtail log collector, Mosquitto MQTT, and Tailscale Funnel.

### 3. `optiplex` — Dell OptiPlex (Storage Cloud & Coder Backend)
- **The Mission:** High-capacity local network storage, continuous backup destination, and remote web development environment.
- **Hardware Profile:**
  - **Chassis:** Dell OptiPlex Small Form Factor / Desktop.
  - **CPU:** Intel Core 2 Quad Q9550 (4 cores, 12MB L2 cache, 2.83GHz).
  - **RAM:** 16 GB RAM.
  - **Storage:** 256 GB SSD (OS & containers) + 3 TB high-capacity HDD (partition `Backup` shared via Samba and SSH).
  - **Network:** Static local IP (`192.168.0.41`) + Tailscale static mesh node.
- **The "No AVX" Post-Mortem & Architectural Pivot:**
  - *The Historical Mistake:* This node was originally nicknamed "LLMS" with the intention of hosting quantized language models on CPU.
  - *The Hardware Bottleneck:* The Intel Core 2 Quad architecture (Penryn / Yorkfield) **completely lacks AVX and AVX2 vector instruction extensions**. Modern LLM inference engines (such as `llama.cpp` or `ollama`) and vector math libraries rely on AVX/AVX2 for matrix operations; without them, CPU inference falls back to slow scalar execution or throws invalid instruction faults.
  - *The Senior Pivot:* Rather than discarding the machine, it was re-architected into its optimal role: an exceptionally stable, cool-running Storage Cloud running **Nextcloud** and a containerized **Coder** server. A strict operational policy bans AVX-dependent workloads from this machine, saving power and CPU cycles.

### 4. `acer-aio` — Acer Aspire Z5610 (2010 Relic)
- **The Mission:** Bedside ambient status monitor, streaming media player, and bedroom TV terminal.
- **Hardware Profile:** 23-inch All-in-One PC from 2009/2010, Core 2 Quad Q9550 / E8400, 8 GB DDR3 RAM.
- **Thermal Engineering & MSR Throttling:**
  - *The Problem:* Upgrading the compact AIO chassis with a higher TDP quad-core processor created severe thermal saturation under heavy I/O, hitting the BIOS safety cutoff at 82°C and shutting down.
  - *The Solution:* Engineered [`PowerManagement`](https://github.com/milhy545/PowerManagement)—a custom Linux daemon communicating directly with CPU Model-Specific Registers (MSR) to dynamically throttle multiplier states, smooth fan PWM curves, and multiplex core utilization before thermal thresholds are breached.

### 5. `rpi-tv` — Raspberry Pi Dumb TV Dashboard
- **The Mission:** Low-power living room entertainment hub, home camera monitor, and lightweight system control.
- **Hardware Profile:** Raspberry Pi 3 Model B Rev 1.2 (Broadcom BCM2837 4-core Cortex-A53 @ 1.2GHz, 1 GB LPDDR2, Debian 13 trixie).
- **Core Affinity Pinning Architecture:**
  - Hardware video decode is pinned exclusively to **Core 0 & Core 1**.
  - Background telemetry, network polling, and WebSocket streams are pinned to **Core 2**.
  - Keeps user interaction responsive (under 15% CPU load) offloading spikes to Core 3 during high-bitrate scenes.
- **Software Stack:** Python Textual TUI, FastAPI WebUI with WebSocket terminal (port 8099), and `go2rtc` for sub-second RTSP/WebRTC IP camera streaming.

---

## 🌐 Network Mesh & Zero-Trust Infrastructure

The entire fleet communicates across a hybrid network topology:
1. **Local High-Throughput Layer:** Fast Gigabit Ethernet and private subnets (`192.168.0.x`) for high-volume storage transfers (Samba, Nextcloud, Docker image pulls).
2. **Tailscale Zero-Trust WireGuard Mesh:** Every node maintains an encrypted peer-to-peer Tailscale connection, allowing seamless SSH management, unified dotfile synchronization, and inter-node API communication regardless of whether a machine is behind CGNAT or roaming.
3. **Public Ingress Control:** Strict zero-open-ports policy on home routers. External webhook or dashboard access is gated exclusively through Tailscale Funnel.

---

## 💡 Why This Hardware Mastery Matters for Logistics & Enterprise IT

1. **Root-Cause Triage Over Blind Replacement:** Having repaired electronics at the PCB level and tuned registers on 15-year-old CPUs, I do not assume a system failure requires an expensive hardware replacement. I trace kernel logs, verify thermal envelopes, inspect cabling, and resolve the root bottleneck.
2. **Warehouse-Grade Reliability:** In an Avonmouth distribution warehouse, an RF scanner dropping off Wi-Fi or a thermal printer dropping its driver halts pickers and delays departures. Building resilient systems on resource-constrained hardware instills the exact same discipline: systems must not crash under pressure.
3. **Extreme Resource Efficiency:** Knowing how to squeeze full performance out of low-spec hardware translates directly into writing cleaner, more efficient code and designing cost-effective cloud architectures where RAM and CPU are paid for by the minute.

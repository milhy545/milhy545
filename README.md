# 🔧 Stanislav "Milhy" Muller

### SysAdmin | Vibe Coder | Former Warehouse Operative | Hardware Pragmatist
📍 *Newport, South Wales, UK* | 🇬🇧 *UK Standards & Open to Logistics IT, Systems Support & DevOps roles*  

[![Live Showcase](https://img.shields.io/badge/PORTFOLIO-LIVE_SHOWCASE-2ea44f?style=for-the-badge&logo=githubpages&logoColor=white)](https://milhy545.github.io/milhy545-showcase/)
[![LinkedIn](https://img.shields.io/badge/LINKEDIN-CONNECT-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/stanislav-muller)
[![Docs CZ](https://img.shields.io/badge/DOKUMENTACE-ČEŠTINA-blue?style=for-the-badge)](./README.cz.md)

> *"If it runs reliably on a Core 2 Quad, it will fly on the Cloud. And if it survives a -25°C commercial freezer warehouse, it will survive enterprise production."*

---

## 👨‍💻 Bridging Physical Logistics & IT Infrastructure

Before transitioning into full-time Linux systems administration, automation, and AI orchestration ("Vibe Coding"), I spent **7 years on the frontlines of UK distribution hubs (Avonmouth)** operating Reach Trucks, voice-picking headsets, and RF handheld scanners, backed by **12 years of electrical component diagnostics**.

In high-throughput warehousing, **downtime is measured in lost pallets and missed departures**:
- When a warehouse Wi-Fi roaming glitch drops an RF scanner mid-pick, pickers stop.
- When an industrial Zebra thermal printer jams or loses its driver spool, shipping docks stall.
- When a Warehouse Management System (WMS) drops a transaction socket, the whole conveyor line backs up.

I don't just write scripts; I build robust, fault-tolerant systems designed to withstand real-world operational chaos.

---

## 🚀 Daily-Driver Utilities & Production Systems
*Active, battle-tested software designed to solve concrete operational and resource bottlenecks.*

### 🎮 [Steam-VRAM-Manager](https://github.com/milhy545/Steam-VRAM-Manager)
**Desktop-Agnostic GPU VRAM & Local LLM Orchestrator**
- **The Problem:** Running local LLMs (`llama.cpp` / `llama-server` on full GPU offload) consumes ~5.38 GB VRAM. Launching modern Steam games on a 6GB card (GTX 1060) triggers immediate Out-Of-Memory (OOM) crashes.
- **The Solution:** A universal systemd-aware wrapper that hooks into the Steam game lifecycle. It cleanly stops `llama.service`, flushes CUDA context (freeing 5.4 GB), enables NVIDIA PRIME offload, and launches the game with full VRAM. On exit, a GUI dialog (kdialog/zenity/yad) with a 60-second timeout automatically restores the AI service.
- **Docs & Deep-Dive:** [English README](https://github.com/milhy545/Steam-VRAM-Manager/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/Steam-VRAM-Manager/blob/main/README.cz.md)

### 🛡️ [MyVoiceTranslator](https://github.com/milhy545/MyVoiceTranslator) *(Milhy's Interview Shield)*
**Low-Hardware Real-Time STT & EN ➔ CS Translation Shield**
- **The Problem:** Bridging real-time technical language barriers during live UK technical interviews and training without cloud latency or heavy dependencies.
- **The Solution:** A lightweight Python Textual TUI with a strict **CPU-first fallback strategy** and PipeWire/PulseAudio loopback routing. Features automated session logging in Markdown and single-command local deployment (`~/.local/bin/myvoice`).
- **Docs & Deep-Dive:** [English README](https://github.com/milhy545/MyVoiceTranslator/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/MyVoiceTranslator/blob/main/README.cz.md)

### 🧠 [Orchestration Platform](https://github.com/milhy545/orchestration)
**14-Container Docker MCP Gateway & Memory Backbone**
- **Architecture:** Complete multi-agent MCP platform running 14 modular Docker microservices (Filesystem, Git, Terminal, Database, Memory, FORAI Code Tracking, Qdrant vector database, and Marketplace).
- **The Hardware Irony:** This core orchestration brain runs on the **oldest, lowest-spec hardware in my entire lab**. MCP tools and API gateways demand reliable RAM and network persistence, not raw compute cycles. Running the nervous system on legacy silicon proves zero-waste efficiency.
- **Docs & Deep-Dive:** [English README](https://github.com/milhy545/orchestration/blob/master/README.md) | [Česká dokumentace](https://github.com/milhy545/orchestration/blob/master/README.cz.md)

### ⚡ [PowerManagement](https://github.com/milhy545/PowerManagement)
**Linux MSR CPU Frequency Control & Thermal Throttling**
- **The Problem:** Upgraded a 2010 All-in-One PC with a significantly more powerful CPU, leading to severe thermal saturation and automatic shutdowns at 82°C.
- **The Solution:** Custom Linux power management suite interacting directly with CPU MSR (Model-Specific Registers) to dynamically step frequencies, control PWM fan curves, and multiplex core utilization to prevent thermal cutoff.
- **Docs & Deep-Dive:** [English README](https://github.com/milhy545/PowerManagement/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/PowerManagement/blob/main/README.cz.md)

---

## 🧪 Knowledge Labs & Engineering Post-Mortems
*Deep technical sandboxes where unfinished code yielded profound low-level systems knowledge.*

### 📺 [RPi-TV Dashboard](https://github.com/milhy545/RPi) *(Embedded Kernel Tuning & Core Affinity)*
- **Deep-Dive Lesson:** Pushing a resource-constrained 4-core ARM Raspberry Pi to deliver 1080p media playback and Steam Link game streaming.
- **Kernel Orchestration:**
  - **Core 0:** Isolated exclusively for network stack, Wi-Fi, and Bluetooth IRQ noise.
  - **Core 3:** Locked for ALSA audio stack to eliminate audio dropouts and buffer underruns.
  - **Cores 1 & 2:** Dedicated to the MPV player engine with dynamic 160% threshold burst scheduling to Core 3 during peak rendering.
- **Docs & Deep-Dive:** [English README](https://github.com/milhy545/RPi/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/RPi/blob/main/README.cz.md)

### 📚 [kindle_butler](https://github.com/milhy545/kindle_butler) *(Hardware udev Peripheral Automation)*
- **Deep-Dive Lesson:** Linux peripheral event automation via `udev` rules.
- **Implementation:** Triggers background library synchronization upon USB plug-in, leverages Gemini AI for metadata normalization, and reformats complex technical tables for readable E-Ink typography.
- **Docs & Deep-Dive:** [English README](https://github.com/milhy545/kindle_butler/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/kindle_butler/blob/main/README.cz.md)

### 🔑 [Unification](https://github.com/milhy545/Unification) *(The SSH Hell Chronicle)*
- **Deep-Dive Lesson:** Documented post-mortem of 150+ configuration failures while managing multi-server SSH keys, port forwarding mismatches, and nested tmux sessions. Led to unified key management and automated environment provisioning.
- **Docs & Deep-Dive:** [English README](https://github.com/milhy545/Unification/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/Unification/blob/main/README.cz.md) | [The SSH Chronicle](https://github.com/milhy545/Unification/blob/main/docs/stories/ssh-hell-chronicle-en.md)

### 💡 The Engineering Pivot: MyCoder ➔ `pi`
- **Architectural Lesson:** Originally designed a custom autonomous coding agent (`MyCoder`). When open-source `pi` (`p-coding-agent`) was released with modular provider support and zero bloat, I immediately deprecated MyCoder.
- **Senior Takeaway:** A pragmatic engineer never reinvents the wheel when an excellent open-source tool solves the problem.

---

## 🛠️ Tech Stack & Homelab Fleet

| Category | Technologies & Tools |
| :--- | :--- |
| **Operating Systems & Shell:** | Debian / MX Linux, Raspberry Pi OS, Bash, Zsh, Oh My Zsh, tmux |
| **Containers & Virtualization:** | Docker, Docker Compose, systemd user services, QEMU/KVM |
| **Networking & Mesh:** | Tailscale (WireGuard mesh), SSH automation, PipeWire / PulseAudio |
| **Languages & Tooling:** | Python (uv, Textual, FastAPI), Node.js, Shell, Git, GitHub Actions |
| **AI & Inference:** | `llama.cpp` (NVIDIA CUDA offload), Model Context Protocol (MCP), Pi, Codex, AGY |
| **Hardware Nodes:** | Workstation (i5-4690K, GTX 1060 6GB), HAS MCP Node, Bedside Media Node, RPi TV |

---
*Generated with automated GitOps discipline — Contact: [GitHub Profile](https://github.com/milhy545)*

# 🔧 Stanislav "Milhy" Muller

### SysAdmin | Vibe Coder | Former Warehouse Operative | Hardware Pragmatist
📍 *Newport, South Wales, UK* | 🚀 *Open to IT Infrastructure, Service Desk & Logistics Tech roles*

> **"If it runs on a Core 2 Quad, it will fly on the Cloud. And if it survives a -25°C freezer chamber, it will survive production."**

---

## 👨‍💻 About Me
Former Electrician and 7-year Warehouse Operative transitioning into **Linux Systems Administration, Infrastructure Support, and AI-assisted Development ("Vibe Coding")**. 

I bridge the gap between physical operations and IT infrastructure. Having spent years operating Reach Trucks, voice-picking headsets, and handheld RF scanners across Avonmouth distribution hubs, **I know firsthand what happens when an RF scanner drops offline, a zebra label printer jams, or a WMS connection drops in the middle of a shift: production grinds to a dead stop.**

My technical foundation combines 12 years of electrical component-level diagnostics with practical system administration: running containerized workloads, MCP servers, and local LLM pipelines across optimized modern and legacy hardware.

---

## 🖥️ The Lab & Infrastructure Topology

* **MILHY-PC (Primary Workstation & Local AI Node):**
  * *Specs:* Intel Core i5-4690K | 32 GB RAM | NVIDIA GeForce GTX 1060 6GB | MX Linux (Debian)
  * *Workload:* Vibe Coding daily driver, Docker environments, local LLM inference via `llama.cpp` (Qwen 7B / Mistral).
  * *Custom Tooling:* Built custom dynamic VRAM management (`steam-gpu-wrap`) to orchestrate GPU memory between local AI services and system tasks.
* **HAS (Home Automation Server):**
  * *Specs:* Repurposed headless laptop (internal battery acts as built-in UPS) running Alpine Linux.
  * *Workload:* 24 Docker containers, Home Assistant, AdGuard Home, MQTT, and the Mega-Orchestrator MCP cluster exposed securely via Tailscale Funnel.
* **Optiplex (3xR Storage & Backend Node):**
  * *Specs:* Intel Core 2 Quad Q9550 | 16 GB RAM | 256GB SSD + 3TB HDD | Headless Docker Host
  * *Workload:* Local storage cloud (Nextcloud) and Coder backend. Practical proof of the **Reuse, Refix, Recycle** principle.

---

## 🛠️ Technical Arsenal

| Category | Stack & Tools |
| :--- | :--- |
| **Operating Systems** | Linux (Debian, Arch, Alpine, MX Linux), Systemd daemons, SSH Key/Tunnel Mesh |
| **Logistics & IT Ops** | WMS hardware triage, RF barcode scanners, Zebra/thermal printers, First-line Desktop support (Win 11) |
| **Containers & Net** | Docker, Docker Compose, Portainer, TCP/IP, VLAN basics, WireGuard, Tailscale, Sing-box |
| **Scripting & Automation**| Bash/Zsh (Oh-My-Zsh), Python (system daemons, APIs, FastMCP servers), Node.js |
| **AI Orchestration** | Model Context Protocol (MCP), Pi CLI, AGY (Antigravity), Jules, Claude Code, llama.cpp |
| **Physical Hardware** | Component-level diagnostics, Cat6 structured cabling, distribution boards, thermal & power management |

---

## 🏗️ Key Active Projects

* **[RPi-TV](https://github.com/milhy545/RPi):** Low-RAM Raspberry Pi TV dashboard with Textual TUI, WebUI, go2rtc (WebRTC/RTSP) streaming, and Playwright verification.
* **[orchestration](https://github.com/milhy545/orchestration):** Modular Mega-Orchestrator aggregating Model Context Protocol (MCP) services across local hardware with Qdrant vector backend.
* **[PowerManagement](https://github.com/milhy545/PowerManagement):** Linux Power Suite with MSR-based CPU frequency and thermal control for legacy multi-core silicon.
* **[reed-openapi-spec](https://github.com/milhy545/reed-openapi-spec):** Clean OpenAPI specification for UK job market aggregation.

---

## ⚡ Why My Background Matters for IT Support

1. **Warehouse Reality:** I don't treat IT support as an isolated ticket queue. I know the physical pressure of pick targets, shift handovers, and loading dock deadlines.
2. **Hardware Diagnostics:** 12 years of electromechanics means I don't just restart a frozen box; I check cabling, verify continuity, isolate port faults, and fix root causes.
3. **Pragmatic Automation:** I write shell scripts and deploy containers to eliminate operational friction and repetitive manual steps.

---

## 📬 Contact & Links
* **GitHub:** [github.com/milhy545](https://github.com/milhy545)
* **LinkedIn:** [linkedin.com/in/stanislav-muller](https://www.linkedin.com/in/stanislav-muller)
* **Location:** Newport, South Wales (NP19 7LY)

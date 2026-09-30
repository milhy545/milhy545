# ğŸ› ï¸ The Homelab Fleet: Pre-AI Silicon in Modern Production

> *"If it runs reliably on a Core 2 Quad, it will fly on the Cloud. And if it survives a -25Â°C commercial freezer warehouse, it will survive enterprise production."*

[![Live Showcase](https://img.shields.io/badge/PORTFOLIO-LIVE_SHOWCASE-2ea44f?style=for-the-badge&logo=githubpages&logoColor=white)](https://milhy545.github.io/milhy545-showcase/)
[![LinkedIn](https://img.shields.io/badge/LINKEDIN-CONNECT-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/stanislav-muller)
[![Docs CZ](https://img.shields.io/badge/DOCUMENTACE-ÄŒDETTANA-blue?style=for-the-badge)](./hardware-fleet.cz.md)

---

## ğŸ— Architectural Philosophy: The 3xR Principle

In an industry obsessed with throwing multi-thousand-dollar cloud instances and brand-new silicon at every problem, my home lab is built on a diametrically opposed principle: **Reuse, Refix, Recycle (3xR)**, governed by **The Goat Principle** (*Functionality > Aesthetics*).

Every piece of computing equipment in this labâ€”from an Intel Core 2 Quad to a headless laptopâ€”has been systematically diagnosed at the component level, optimized through low-level Linux kernel tuning, and assigned a strictly defined architectural role. If hardware fails to run modern workloads out-of-the-box, we do not discard it; we profile the bottleneck, write kernel wrappers or MSR frequency controllers, containerize the services, and make it rock-solid.

Machine-readable topology catalog: [`data/hardware-fleet.json`](../data/hardware-fleet.json)

---

## ğŸ¿ Fleet Overview & Node Topology

| Node ID | Machine | Hardware Specs | Primary OS | Primary Role |
| :--- | :--- | :--- | :--- | :--- |
| **`milhy-pc`** | MILHY-PC | Intel i5-4690K, 32GB RAM, GTX 1060 6GB Dual | MX[^H
XšX[ˆLÊHXZ[ˆšX™HÛÙ[™È	ˆØØ[SHÔH›ÙHŸ
Š˜\Ø
ŠˆTÈÙ\™\ˆ™\\œÜÙYXY\ÜÈ\Ü
Z[Z[ˆTÊH[[™H[^ØÚÙ\ˆÛÛZ[™\œËÛYH\ÜÚ\İ[YYØKSÜ˜Ú\İ˜]ÜˆPÔŸ
Š»Ü\^
Šˆ[ÜT^[[ÛÜ™Hˆ]XYNMMLM‘ĞˆSKM‘ĞˆÔÑ
ÈÕˆÑXšX[‹X˜\ÙYXY\ÜÈ™^ÛİYİÜ˜YÙHÛİYÛÙ\ˆ˜XÚÙ[™	ˆ™]ÛÜšÈ˜XÚİ\Ÿ
Š¨XÙ\‹XZ[Ø
ŠˆXÙ\ˆ\Ü\™HMŒL[[ÛÜ™Hˆ]XYNMMLÈNĞˆSHYÚÙZYÚ[^™YÚYHÛY\[™È‹YYXH›ÙH	ˆ[XšY[İ]\È[Ûš]ÜˆŸ
Š˜œK]˜
Šˆ˜\Ü™\œHHˆ]XYPÛÜ™HT“KİËTSH›Ùš[H˜\Ü™\œHHÔÈˆ\Ú›Ø\™ÛÌÈÙX”•Èİ™X[Z[™È	ˆÙ\›™[U[™YYYXHŸ
Š˜[Øš[KYYÙX
Šˆ˜]™[šYÈ™X[YHQÈ
È[[]ÛHŒÌ™]›ÛÚÈ[™›ÚYÈ[^
“‘TÊH™\›ËQ\[™[˜ŞHÜX›HÙ™›[™HXYÛ›ÜİXÈšYÈ‚‹KKB‚ˆÈÈ<'æ`]Z[Y›ÙH[˜[\Ú\Â‚ˆÈÈÈKˆZ[K\Ø8 %š[X\HÛÜšÜİ][Ûˆ	ˆØØ[RH[™™\™[˜ÙH›ÙB‹H
Š•HZ\ÜÚ[ÛŠŠˆHZ[KYš]™\ˆÛÛ[X[™Ù[\ˆ›ÜˆRKX\ÜÚ\İY]™[ÜY[
•šX™HÛÙ[™ÈŠKÛÛZ[™\ˆ]™[ÜY[[™ØØ[ÔHXØÙ[\˜][Û‹‚‹H
Š’\™Ø\™H›Ùš[NŠŠ‚ˆH
ŠÔNŠŠˆ[[ÛÜ™HMKMLÈ
ÛÜ™\ÈËLÒˆ˜\ÙK\ÈËLÚˆ\˜›ÊK‚ˆH
Š”SNŠŠˆÌˆĞˆŒÈX[XÚ[›™[‚ˆH
Š‘ÔNŠŠˆ•’QPHÙQ›Ü˜ÙHÕLŒ‘ĞˆX[
ÔLˆ\ØØ[
H
È[[Ü˜\XÜÈŒ‚ˆH
Š“ÔÎŠŠˆV[^HÑHØ^[[™
XšX[ˆLÈš^YH˜\ÙK[^‹ŒLˆÙ\›™[
K‚‹H
Š‘ÔH\˜Ú]Xİ\™H	ˆ[™Ú[™Y\š[™ÎŠŠ‚ˆH
‘\ÚİÜÙ\\˜][ÛŠˆH\ÚİÜÕRH[™Z[H\Ü^\È[ˆ[\™[HÛˆH[YÜ˜]Y[[Œ
NLMXš]™\ŠKÙY\[™È\Ü^H][˜ŞH[™\[™[ÙˆÔHÛÛ\]HØY‚ˆH
‘š]™\ˆ[›š[™ÎŠˆ\ØØ[XÚÜÈHÔHŞ\İ[H›ØÙ\ÜÛÜˆ
ÔÔ
HÛÜ›ØÙ\ÜÛÜ‹XZÚ[™ÈšYXKZÙ\›™[[Ü[‹YÛ\Ø˜Z[Èš[™ˆÛÛ™šYİ\™YT[›š[™È
Ù]ËØ\Ü™Y™\™[˜Ù\Ë™ÛšYXKYXšX[‹œ™Y˜
HÈØÚÈXšX[ˆ›ÜšY]\Hš]™\ˆMLŒMŒØÚ]›İ]™X]X›XÚÛ\İY‚ˆH
•”SDG›˜[ZXÈÜ˜Ú\İ˜]ÜŠˆÚ]Û›HˆĞˆ”SK[›š[™ÈØØ[\È
[XK\Ù\™\˜™\Ù\š[™ÈKŒÎĞŠHØ]\ÙY[[YYX]Hİ]SÙ‹SY[[ÜHÜ˜\Ú\ÈÚ[ˆ][˜Ú[™ÈİX[H›İÛˆØ[Y\Ëˆ]™[ÜYØİX[KU”SKSX[˜YÙ\˜JÎ‹ËÙÚ]X‹˜ÛÛKÛZ[MMKÔİX[KU”SKSX[˜YÙ\ŠH
İX[KYÜK]Ü˜\Èœ˜[K\›İÛ˜
HÈ]]ÛX]XØ[HİÜ[XKœÙ\šXÙX›\ÚÕQHY[[ÜK[˜X›H’SQHÙ™›ØY[™ØY™[H™\İÜ™HHSHÙ\šXÙH\Ûˆ^]‚ˆH
•š\X[^˜][ÛŠˆÚ[™İÜÈLHQSUEKVM virtual machine dedicated to specialized tools (Perplexity Comet browser, Codex desktop).

### 2. `has` â‚” Home Automation Server (Headless Laptop with Built-in UPS)
- **The Mission:** 24/7 central automation brain, network hygiene, and Model Context Protocol (MCP) gateway.
- **The Hardware Trick (Built-in Zero-Latency UPS):** Instead of an expensive rackmount server or dedicated enterprise UPS,yHAS runs on a repurposed headless laptop. The functioning internal laptop battery acts as a native uninterruptible power supply, completely insulating the system against grid micro-outages and voltage sags without extra hardware cost.
- **Operating System:** Alpine Linux for ultra-minimal RAM overhead, hardened musl-based security, and lightning-fast container startups.
- **Active Workloads (24 Docker Containers):**
  - **Home Assistant:** Central smart home automation and Zigbee/Z-Wave coordination.
  - **Mosquitto MQTT:** High-throughput messaging broker between IOT sensors and microservices.
  - **AdGuard Home:** Local DNS sinkhole providing zero-ad browsing and telemetry blocking network-wide.
  - **Mega-Orchestrator MCP Cluster:** Multi-agent MCP server gateway (Filesystem, Git, Terminal, Database, Memory, Qdrant vector database, and Marketplace).
  - **Tailscale Funnel:** Secure TLS ingress exposing authorized orchestration endpoints without opening router ports.

### 3. `optiplex` â‚” Dell OptiPlex (Storage Cloud & Coder Backend)
- **The Mission:** High-capacity local network storage, continuous backup destination, and remote web development environment.
- **Hardware Profile:**
  - **Chassis:** Dell OptiPlex Small Form Factor / Desktop.
  - **CPU:** Intel Core 2 Quad Q9550 (4 cores, 12MB L2 cache, 2.83GHz).
  - **RAM:** 16 GB RAM.
  - **Storage:** 256 GB SSD (OS & containers) + 3 TB high-capacity HDD (partition `Backup` shared via Samba and SSH) .
  - **Network:** Static local IP (`192.168.0.41`) + Tailscale static mesh node.
- **The "No AVX" Post-Mortem & Architectural Pivot:**
  - *The Historical Mistake:* This node was originally nicknamed "LLMS" with the intention of hosting quantized language models on CPU.
  - *The Hardware Bottleneck:* The Intel Core 2 Quad architecture (Penryn / Yorkfield) **completely lacks AVX and AVX2 vector instruction extensions**. Modern LLM inference engines (such as `llama.cpp` or `ollama`) and vector math libraries rely on AVX/AVX2 for matrix operations; without them, CPU inference falls back to slow scalar execution or throws invalid instruction faults.
  - *The Senior Pivot:* Rather than discarding the machine, it was re-architected into its optimal role: an exceptionally stable, cool-running Storage Cloud running **Nextcloud** and a containerized **Coder** server. A strict operational policy bans AVX-dependent workloads from this machine, saving power and CPU cycles.

### 4. `acer-aio` â‚” Acer Aspire Z5610 (2010 Relic)
- **The Mission:** Bedside ambient status monitor, streaming media player, and bedroom TV terminal.
- **Hardware Profile:** 23-inch All-in-One PC from 2009/2010, Core 2 QuadQ9550 / E8400, 8 GB DDR3 RAM.
- **Thermal Engineering & MSR Throttling:**
  - *The Problem:* Upgrading the compact AIO chassis with a higher TDP quad-core processor created severe thermal saturation under heavy I/O, hitting the BIOS safety cutoff at 82Â°C and shutting down.
  - *The Solution:* Engineered [`PowerManagement`](https://github.com/milhy545/PowerManagement)â€”a custom Linux daemon communicating directly with CPU Model-Specific Registers (MSR) to dynamically throttle multiplier states, smooth fan PWM curves, and multiplex core utilization before thermal thresholds are breached.

### 5. `rpi-tv` â€” Raspberry Pi Dumb TV Dashboard
- **The Mission:** Low-power living room entertainment hub, home camera monitor, and lightweight system control.
- **HardwarmH›Ùš[NŠŠˆXÛÜ™HT“H˜\Ü™\œHHÚ]İšXİSHÛÛœİ˜Z[È
QĞ‹L‘ĞŠK‚‹H
Š’Ù\›™[Ü˜Ú\İ˜][Ûˆ	ˆÛÜ™HY™š[š]NŠŠ‚ˆH
ÛÜ™HŠˆ\ÛÛ]Y^Û\Ú]™[H›Üˆ[^™]ÛÜšÚ[™ÈİXÚËÚKQšHš]™\œË[™›Y]ÛİT”H›ØÙ\ÜÚ[™Ë‚ˆH
ÛÜ™HÎŠˆØÚÙY›ÜˆHSĞH]Y[ÈİXÚÈÈ[[Z[˜]H]Y[È›Üİ]È[™Y™™\ˆ[™\œ[œÈ\š[™ÈYYXH^X˜XÚË‚ˆH
ÛÜ™\ÈH	ˆŠˆYXØ]YÈHTˆYYXH^X˜XÚÈ[™Ú[™KÚ][˜[ZXÈ\œİ™\ÚÛØÚY[[™È
MŒ	H%CPU Load) offloading spikes to Core 3 during high-bitrate scenes.
- **Software Stack:** Python Textual TUI, FastAPI WebUI with WebSocket terminal (port 8099), and `go2rtc` for sub-second RTSP/WebRTC ğIP camera streaming.

### 6. `mobile-edge` â€” Travel Rig (Offline RNDIS Cluster)
- **The Mission:** Portable diagnostic rig and zero-dependency terminal for field operations.
- **Topology:** A Realme 8 5G cellphone running Termux Linux environment (compute node) tethered directly via USB (RNDIS) to an Intel Atom N270 Netbook (keyboard & display client).
- **Advantage:** Forms a private `192.168.42.x` offline network capable of running shell scripts, network scanners, and local tools in environments with zero Wi-Fi or cellular connectivity.

---

### ğŸ Network Mesh & Zero-Trust Infrastructure

The entire fleet communicates across a hybrid network topology:
1. **Local High-Throughput Layer:** Fast Gigabit Ethernet and private subnets (`192.168.0.x`) for high-volume storage transfers (Samba, Nextcloud, Docker image pulls).
2. **Tailscale Zero-Trust WireGuard Mesh:** Every node maintains an encrypted peer-to-peer Tailscale connection, allowing seamless SSH management, unified dotfile synchronization, and inter-node API communication regardless of whether a machine is behind CGNAT or roaming.
3. **Public Ingress Control:** Strict zero-open-ports policy on home routers. External webhook or dashboard access is gated exclusively through Tailscale Funnel.

---

## ğŸ’¡ Why This Hardware Mastery Matters for Logistics & Enterprise IT

1. **Root-Cause Triage Over Blind Replacement:** Having repaired electronics at the PCB level and tuned registers on 15-year-old CPUs, I do not assume a system failure requires an expensive hardware replacement. I trace kernel logs, verify thermal envelopes, inspect cabling, and resolve the root bottleneck.
2. **Warehouse-Grade Reliability:** In an Avonmouth distribution warehouse, an RF scanner dropping off Wi-Fi or a thermal printer dropping its driver halts pickers and delays departures. Building resilient systems on resource-constrained hardware instills the exact same discipline: systems must not crash under pressure.
3. **Extreme Resource Efficiency:** Knowing how to squeeze full performance out of low-spec hardware translates directly into writing cleaner, more efficient code and designing cost-effective cloud architectures where RAM and CPU are paid for by the minute.

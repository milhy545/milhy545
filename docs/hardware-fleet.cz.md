# 🏰 Architektura bare-metal homelabu a hardwarové flotily

> **Inženýrská filozofie:** *„3xR: Reuse, Refix, Recycle — Vymáčkni z každého cyklu maximum.“*  
> Moderní softwarové inženýrství se často schovává za neomezené rozpočty v cloudu a předimenzované Kubernetes clustery. Tento repozitář dokumentuje odolnou, produkční 5uzlovou bare-metal flotilu postavenou výhradně na zachráněném, zrecyklovaném a tepelně optimalizovaném hardwaru.

---

## 📊 Rychlá přehledová matice flotily

| ID uzlu | Zařízení | Hardwarové parametry | Primární OS | Hlavní produkční role |
| :--- | :--- | :--- | :--- | :--- |
| **`milhy-pc`** | MILHY-PC | Intel i5-4690K (4J/4V @ 3.90GHz), 32GB DDR3, GTX 1060 6GB | MX Linux (SysVinit / XFCE) | Hlavní pracovní stanice, kompilace, denní vývoj a virtualizace |
| **`has`** | HAS Server | Compaq Presario CQ57 (AMD E-300 APU 2J, 4GB RAM, 240GB SSD, vestavěná UPS) | Debian 13 (trixie) | Centrální domácí automatizace, 25 Docker kontejnerů, Mega-Orchestrator MCP cluster |
| **`optiplex`** | Dell OptiPlex | Intel Core 2 Quad Q9550, 16GB DDR2, 256GB SSD + 3TB HDD | Debian GNU/Linux (Headless) | Privátní úložný cloud, Nextcloud a kontejnerizovaný vývojový Coder server |
| **`acer-aio`** | Acer Aspire Z5610 | Core 2 Quad Q9550, 8GB DDR3, 23" dotykové AIO | Linux (vlastní PowerManagement) | Noční ambientní stavový terminál, přehrávač médií a telemetrický displej |
| **`rpi-tv`** | RPi Dumb TV Hub | Raspberry Pi 3 Model B (4J Cortex-A53, 1GB LPDDR2, MicroSD) | Debian 13 (trixie) | Dashboard pro obývací pokoj (hloupá TV), Textual TUI / FastAPI a go2rtc RTSP kamery |

---

## 🖥️ Detailní profily uzlů a inženýrské počiny

### 1. `milhy-pc` — Hlavní pracovní stanice a denní vývoj
- **Mise:** Vysoce výkonná vývojářská stanice, vícemonitorové centrum produktivity a virtualizační uzel.
- **Hardwarový profil:**
  - **CPU:** Intel Core i5-4690K (Haswell 4 jádra, 3.50GHz základ / 3.90GHz boost).
  - **RAM:** 32 GB Dual-Channel DDR3.
  - **GPU:** NVIDIA GeForce GTX 1060 6GB (Dual Fan).
  - **Úložiště:** NVMe/SATA SSD disky pro rychlé kompilace + velkokapacitní lokální disky.
  - **Monitory:** Dvouobrazovková sestava (AOC 24B1W + Philips 223V5).
- **Architektura operačního systému:**
  - Běží na **MX Linuxu** se **SysVinit** (záměrná volba eliminující zbytečnou režii systemd a zajišťující deterministické plánování procesů).
  - Minimalistický a bleskurychlý desktop **XFCE** s upravenými klávesovými zkratkami, precizními dotfiles v terminálu a tmavým režimem šetřícím zrak.
  - Provozuje dedikované vývojové kontejnery a specializované virtuální stroje QEMU/KVM pro bezpečné testování.

### 2. `has` — Home Automation Server (Compaq Presario CQ57 s vestavěnou UPS)
- **Mise:** Nepřetržitý mozek domácí automatizace, síťová hygiena a centrální multimodální brána pro Model Context Protocol (MCP).
- **Hardwarový profil:**
  - **Model:** Compaq Presario CQ57 Notebook PC (Hewlett-Packard).
  - **CPU:** AMD E-300 APU s Radeon HD Graphics (2 jádra @ 1.30 GHz).
  - **RAM:** 4 GB DDR3.
  - **Úložiště:** 240 GB SSD (systém a Docker perzistentní svazky).
  - **OS:** Debian GNU/Linux 13 (trixie, Linux jádro 6.12).
- **Hardwarový trik (vestavěná nulově nákladová UPS):** Namísto nákupu drahého serveru a externí záložní UPS běží HAS na vyřazeném headless notebooku. Funkční interní baterie slouží jako přirozený záložní zdroj napájení (UPS), který udrží server v chodu i při kolísání sítě nebo krátkodobém výpadku bez jediného haléře navíc.
- **Běžící služby (25 Docker kontejnerů):**
  - **Home Assistant:** Srdce chytré domácnosti a koordinace senzorů (`ghcr.io/home-assistant/home-assistant:stable`, port 10002 -> 8123).
  - **Mega-Orchestrator MCP Gateway (port 7000) & Security Gateway (port 7080):** Centrální multimodální brána propojující specializované MCP servery.
  - **MCP mikroservisy:** Filesystem (7001), Git (7002), Terminal (7003), Database (7004), Memory (7005), Security (7008), Config (7009), Log (7010), Advanced Memory (7012), FORAI (7016), MQTT (7019), Code Graph (7020), Marketplace (7034), Vault (7070).
  - **Datová vrstva:** PostgreSQL 15 (7021), Redis 7 (7022), Qdrant vektorová paměť (7026).
  - **Monitoring & síť:** Grafana (7031), Promtail, Mosquitto MQTT a Tailscale Funnel.

### 3. `optiplex` — Dell OptiPlex (Úložný cloud a backend pro Coder)
- **Mise:** Velkokapacitní síťové úložiště, cíl nepřetržitých záloh a vzdálené webové vývojové prostředí.
- **Hardwarový profil:**
  - **Šasi:** Dell OptiPlex Small Form Factor / Desktop.
  - **CPU:** Intel Core 2 Quad Q9550 (4 jádra, 12MB L2 cache, 2.83GHz).
  - **RAM:** 16 GB RAM.
  - **Úložiště:** 256 GB SSD (OS a kontejnery) + 3 TB vysokokapacitní HDD (oddíl `Backup` sdílený přes Sambu a SSH).
  - **Síť:** Statická lokální IP (`192.168.0.41`) + uzel v síti Tailscale.
- **Případová studie „No AVX“ a inženýrský obrat:**
  - *Původní omyl:* Uzel měl původně přezdívku „LLMS“ se záměrem spouštět kvantizované LLM modely na CPU.
  - *Hardwarové omezení:* Architektura Intel Core 2 Quad (Penryn / Yorkfield) **zcela postrádá vektorové instrukční sady AVX a AVX2**. Moderní LLM knihovny (`llama.cpp`, `ollama`) a vektorové výpočty jsou na AVX/AVX2 striktně závislé; bez nich kód havaruje nebo běží v neúnosně pomalém skalárním režimu.
  - *Seniorský obrat:* Namísto vyřazení stroje došlo k přehodnocení jeho role: stal se z něj stabilní a tichý privátní úložný cloud pro **Nextcloud** a kontejnerizovaný server **Coder**. Striktní pravidlo zakazuje běh úloh vyžadujících AVX, což šetří energii i CPU cykly.

### 4. `acer-aio` — Acer Aspire Z5610 (Relikvie z roku 2010)
- **Mise:** Noční monitor stavu domácnosti, přehrávač médií a ložnicový TV terminál.
- **Hardwarový profil:** 23palcový All-in-One počítač z roku 2009/2010, Core 2 Quad Q9550 / E8400, 8 GB DDR3 RAM.
- **Teplotní inženýrství a throttling přes MSR:**
  - *Problém:* Osazení kompaktního AIO šasi čtyřjádrovým procesorem s vyšším TDP způsobilo při zátěži přehřívání, dosažení limitu BIOSu 82 °C a tvrdé vypnutí.
  - *Řešení:* Vyvinut démon [`PowerManagement`](https://github.com/milhy545/PowerManagement) — vlastní Linux služba komunikující přímo s registry procesoru (MSR), která dynamicky škrtí násobiče, vyhlazuje PWM křivky ventilátoru a multiplexuje jádra dříve, než dojde k překročení limitů.

### 5. `rpi-tv` — Raspberry Pi Dumb TV Dashboard
- **Mise:** Nízkoenergetické centrum v obývacím pokoji pro hloupou TV, monitor bezpečnostních kamer a systémový ovladač.
- **Hardwarový profil:** Raspberry Pi 3 Model B Rev 1.2 (Broadcom BCM2837 4jádrový Cortex-A53 @ 1.2GHz, 1 GB LPDDR2, Debian 13 trixie).
- **Architektura přiřazování jader (Core Affinity Pinning):**
  - Hardwarové dekódování videa je striktně přiřazeno na **Jádro 0 a Jádro 1**.
  - Telemetrie na pozadí, síťové dotazy a WebSocket spojení běží na **Jádru 2**.
  - Zajišťuje bleskovou odezvu uživatelského rozhraní (pod 15 % CPU load) a přelévá zátěž na Jádro 3 během náročných scén.
- **Softwarový stack:** Python Textual TUI, FastAPI WebUI s WebSocket terminálem (port 8099) a `go2rtc` pro okamžité streamování bezpečnostních RTSP kamer.

---

## 🌐 Síťová architektura a Zero-Trust infrastruktura

Celá flotila komunikuje v hybridním síťovém uspořádání:
1. **Lokální vysokorychlostní vrstva:** Gigabitový Ethernet a privátní podsítě (`192.168.0.x`) pro velké objemy dat (Samba, Nextcloud, Docker image).
2. **Šifrovaný Tailscale WireGuard Mesh:** Každý uzel udržuje bezpečné spojení bod-bod v síti Tailscale. Umožňuje bezpečný přístup přes SSH, synchronizaci dotfiles a API volání bez ohledu na to, zda je uzel za CGNAT nebo na cestách.
3. **Řízení vstupu z internetu:** Striktní politika nulových otevřených portů na domácím routeru. Přístup zvenčí je povolen výhradně přes Tailscale Funnel.

---

## 💡 Proč je toto hardwarové mistrovství klíčové pro logistiku a podnikové IT

1. **Analýza kořenových příčin namísto slepé výměny dílů:** Díky zkušenostem s opravami elektroniky na úrovni plošných spojů a laděním registrů na 15 let starých procesorech vím, že výpadek neznamená nutnost nákupu nového hardwaru. Hledám záznamy v kernel logu, ověřuji teplotní profily a kabeláž a řeším skutečné úzké hrdlo.
2. **Spolehlivost na úrovni distribučního centra:** V logistickém skladu v Avonmouthu může výpadek Wi-Fi na RF skeneru nebo pád ovladače tiskárny štítků zastavit expedici. Provozování systémů na hardwarově omezených strojích buduje identickou disciplínu: systémy nesmí selhat pod tlakem.
3. **Extrémní efektivita zdrojů:** Schopnost vymáčknout maximum z nízkonákladového hardwaru se přímo promítá do psaní čistšího kódu a návrhu nákladově efektivních cloudových architektur, kde se za RAM a CPU platí každou minutu.

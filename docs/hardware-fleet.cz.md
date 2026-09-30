# 🖥️ Hardwarová flotila: Křemík z pre-AI éry v moderní produkci

> *„Pokud systém spolehlivě běží na starém Core 2 Quad, v cloudu doslova poletí. A pokud přežije provoz v mrazáku při -25 °C, přežije v podnikové produkci cokoliv.“*

[![Live Showcase](https://img.shields.io/badge/PORTFOLIO-LIVE_SHOWCASE-2ea44f?style=for-the-badge&logo=githubpages&logoColor=white)](https://milhy545.github.io/milhy545-showcase/)
[![LinkedIn](https://img.shields.io/badge/LINKEDIN-SPOJIT_SE-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/stanislav-muller)
[![Docs EN](https://img.shields.io/badge/DOCS-ENGLISH-blue?style=for-the-badge)](./hardware-fleet.md)

---

## 🧭 Architektonická filozofie: Princip 3xR

V odvětví, které je posedlé vyhazováním tisíců dolarů za zbytečně předimenzované cloudové instance a nákupem nového hardwaru pro každou drobnost, je můj homelab postaven na diametrálně odlišném přístupu: **Reuse, Refix, Recycle (3xR)** řízený **Goat principem** (*Funkčnost > Estetika*).

Každý kousek křemíku v této laboratoři – od veterána Intel Core 2 Quad až po vyřazený notebook – byl detailně diagnostikován na úrovni součástek, softwarově zkrocen nízkoúrovňovým tuningem Linuxového jádra a dostal přísně vymezenou produkční roli. Pokud hardware nestačí moderním požadavkům v továrním nastavení, nevyhazujeme ho: najdeme úzké hrdlo, napíšeme systémový wrapper nebo MSR regulátor frekvence, služby zkontejnerizujeme a postavíme neprůstřelný systém.

Strojově čitelný katalog topologie: [`data/hardware-fleet.json`](../data/hardware-fleet.json)

---

## 🗺️ Přehled flotily & topologie uzlů

| Uzel (Node ID) | Stroj | Hardwarová specifikace | Primární OS | Hlavní produkční role |
| :--- | :--- | :--- | :--- | :--- |
| **`milhy-pc`** | MILHY-PC | Intel i5-4690K, 32GB RAM, GTX 1060 6GB Dual | MX Linux 25 (Debian 13) | Hlavní Vibe Coding stanice & lokální AI inference na GPU |
| **`has`** | HAS Server | Repasovaný headless laptop (vestavěná UPS) | Alpine Linux | 24 Docker kontejnerů, Home Assistant, Mega-Orchestrator MCP |
| **`optiplex`** | Dell OptiPlex | Intel Core 2 Quad Q9550, 16GB RAM, 256GB SSD + 3TB HDD | Debian-based Headless | Síťové úložiště Nextcloud, Coder backend a síťové zálohy |
| **`acer-aio`** | Acer Aspire Z5610 | Intel Core 2 Quad Q9550 / E8400, 8GB RAM | Odlehčený Linux | Ložnicová TV, multimediální streaming & ambientní monitor |
| **`rpi-tv`** | Raspberry Pi TV | 4jádrový ARM, nízko-paměťový profil | Raspberry Pi OS | TV Dashboard, go2rtc WebRTC streamování kamer & tuning jádra |
| **`mobile-edge`**| Cestovní sestava| Realme 8 5G + Intel Atom N270 Netbook | Android / Linux (RNDIS) | Zcela nezávislá offline diagnostická a terminálová stanice |

---

## 🛠️ Detailní analýza jednotlivých uzlů

### 1. `milhy-pc` — Hlavní pracovní stanice a lokální AI inference uzel
* **Účel:** Řídicí centrum pro každodenní práci, asistovaný vývoj pomocí AI („Vibe Coding“), vývoj v Dockeru a akceleraci lokálních modelů na grafice.
* **Hardwarový profil:**
  * **CPU:** Intel Core i5-4690K (4 jádra @ 3.50GHz, turbo až 3.90GHz).
  * **RAM:** 32 GB DDR3 (dual-channel).
  * **GPU:** NVIDIA GeForce GTX 1060 6GB Dual (GP106 Pascal) + Intel HD Graphics 4600.
  * **OS:** MX Linux 25 KDE Wayland (Debian 13 Trixie, Linux jádro 6.12).
* **Architektura GPU a inženýrské řešení:**
  * *Oddělení zobrazení a výpočtů:* Grafické rozhraní desktopu běží čistě na integrované Intel HD 4600 (ovladač `i915`). Tím je zaručeno, že plynulost desktopu nikdy neklesne pod zátěží CUDA výpočtů na dedikované grafice.
  * *Přesné pinování ovladačů:* Architektura Pascal nemá hardwarový koprocesor GSP, což způsobuje pád otevřených modulů `nvidia-kernel-open-dkms`. Nastaveno striktní APT pinování (`/etc/apt/preferences.d/nvidia-debian.pref`) s prioritou pro oficiální Debian proprietární ovladač `550.163` a zablokováním `nouveau`.
  * *Dynamický správce VRAM:* Při 6 GB VRAM obsadí lokální LLM (`llama-server`) zhruba 5.38 GB paměti, což při spuštění hry ve Steamu vedlo k okamžitému pádu na Out-Of-Memory. Vyvinut nástroj [`Steam-VRAM-Manager`](https://github.com/milhy545/Steam-VRAM-Manager) (`steam-gpu-wrap` / `vram-proton`), který před spuštěním hry čistě zastaví `llama.service`, uvolní VRAM, zapne PRIME offload a po ukončení hry službu automaticky oživí.
  * *Virtualizace:* Virtuální stroj Windows 11 (QEMU/KVM) dedikovaný pro nástroje vázané na Windows (Perplexity Comet browser, Codex desktop).

### 2. `has` — Home Automation Server (Headless laptop s vestavěnou UPS)
* **Účel:** Nepřetržitý běh domácí automatizace, síťová hygiena a centrální brána pro Model Context Protocol (MCP).
* **Hardwarový trik (vestavěná nulově nákladová UPS):** Namísto nákupu drahého serveru a externí záložní UPS běží HAS na vyřazeném headless notebooku. Funkční interní baterie slouží jako přirozený záložní zdroj napájení (UPS), který udrží server v chodu i při kolísání sítě nebo krátkodobém výpadku bez jediného haléře navíc.
* **Operační systém:** Alpine Linux pro minimální režii RAM, robustní zabezpečení a bleskový start kontejnerů.
* **Běžící služby (24 Docker kontejnerů):**
  * **Home Assistant:** Srdce chytré domácnosti a koordinace senzorů.
  * **Mosquitto MQTT:** Rychlý zprávový broker propojující IoT prvky a mikroservisy.
  * **AdGuard Home:** Lokální DNS server blokující reklamy a telemetrii na úrovni celé domácí sítě.
  * **Mega-Orchestrator MCP Cluster:** Multimodální brána MCP serverů (Filesystem, Git, Terminal, Database, Memory, Qdrant vektorová paměť, Marketplace).
  * **Tailscale Funnel:** Šifrovaný TLS tunel pro bezpečný přístup k vybraným endpointům bez otevírání portů na routeru.

### 3. `optiplex` — Dell OptiPlex (Úložiště Nextcloud & Coder backend)
* **Účel:** Vysokokapacitní centrální úložiště dat v síti, zálohovací terč a vývojové prostředí v kontejneru.
* **Hardwarový profil:**
  * **Šasi:** Dell OptiPlex Desktop.
  * **CPU:** Intel Core 2 Quad Q9550 (4 jádra, 12MB L2 cache, 2.83GHz).
  * **RAM:** 16 GB RAM.
  * **Úložiště:** 256 GB SSD (systém a kontejnery) + 3 TB HDD (dedikovaný oddíl `Backup` sdílený přes Sambu a SSH).
  * **Síť:** Statická lokální IP (`192.168.0.41`) + Tailscale uzel.
* **Architektonický post-mortem: Proč tento stroj NENÍ pro LLM:**
  * *Původní omyl:* Stroj nesl pracovní přezdívku „LLMS“ s myšlenkou provozovat kvantizované jazykové modely čistě na procesoru.
  * *Tvrdý limit hardwaru:* Architektura Core 2 Quad (Penryn/Yorkfield) **zcela postrádá instrukční sady AVX a AVX2**. Moderní AI knihovny a inferenční enginy (`llama.cpp`, `ollama`) staví maticové výpočty na AVX instrukcích; bez nich CPU buď spadne na neplatnou instrukci, nebo degraduje na nepoužitelnou rychlost.
  * *Inženýrský obrat:* Namísto vyřazení dostal stroj ideální roli: tiché, stabilní síťové úložiště **Nextcloud**, zálohovací uzel pro celou síť a backend pro **Coder** kontejnery. Pravidlo v paměti striktně zakazuje nasazovat na tento uzel úlohy vyžadující AVX.

### 4. `acer-aio` — Acer Aspire Z5610 AIO (Pamětník z roku 2010)
* **Účel:** Noční multimediální terminál, přehrávač streamů u postele a ambientní systémový monitor.
* **Hardwarový profil:** 23palcový All-in-One počítač z let 2009/2010, osazený procesorem Core 2 Quad Q9550 / E8400 a 8 GB DDR3 RAM.
* **Termální inženýrství & řízení přes MSR:**
  * *Problém:* Osazení výkonnějšího čtyřjádrového CPU do stísněného těla AIO způsobovalo při vyšším zatížení masivní přehřívání a nouzové vypínání při 82 °C.
  * *Řešení:* Vyvinuta vlastní softwarová suita [`PowerManagement`](https://github.com/milhy545/PowerManagement) komunikující přímo s MSR registry CPU (Model-Specific Registers). Dynamicky koriguje násobiče frekvencí, upravuje PWM křivky ventilátorů a předchází teplotnímu kolapsu.

### 5. `rpi-tv` — Raspberry Pi Dumb TV Dashboard
* **Účel:** Úsporné multimediální centrum pro televizi, zobrazení bezpečnostních kamer a systémové ovládání.
* **Hardwarový profil:** 4jádrový ARM Raspberry Pi s paměťovým limitem 1–2 GB RAM.
* **Ladění jádra a izolace CPU jader (Core Affinity):**
  * **Core 0:** Vyhrazeno výhradně pro obsluhu síťového stacku, Wi-Fi a Bluetooth přerušení (IRQ).
  * **Core 3:** Uzamčeno pro ALSA zvukový subsystém, aby nedocházelo k lupání či výpadkům zvuku.
  * **Cores 1 a 2:** Dedikováno pro vykreslovací engine přehrávače MPV s dynamickým přeléváním špiček na Core 3 při překročení 160% zátěže.
* **Software:** Python Textual TUI, FastAPI WebUI s WebSocket terminálem (port 8099) a nízko-latenční streamovací server `go2rtc` (WebRTC/RTSP).

### 6. `mobile-edge` — Cestovní diagnostický uzel (Offline RNDIS Cluster)
* **Účel:** Zcela nezávislý přenosný diagnostický terminál pro práci v terénu.
* **Topologie:** Telefon Realme 8 5G (výpočetní uzel v prostředí Termux) propojený přes USB tethering (RNDIS) se starým netbookem s procesorem Intel Atom N270 (klávesnice a displej).
* **Výhoda:** Vytváří privátní offline síť `192.168.42.x`, na které lze spouštět diagnostické skripty a síťové nástroje v místech bez mobilního signálu či Wi-Fi.

---

## 🌐 Síťová architektura & Zero-Trust topologie

Komunikace mezi uzly probíhá ve dvou vrstvách:
1. **Lokální vysokorychlostní síť:** Gigabitový Ethernet a privátní podsíť (`192.168.0.x`) pro velké objemy dat (Samba zálohy, Nextcloud synchronizace, stahování Docker image).
2. **Šifrovaný Tailscale WireGuard Mesh:** Každý uzel má přidělenou bezpečnou peer-to-peer adresu v síti Tailscale. To umožňuje přímé SSH tunely a synchronizaci konfigurací bez ohledu na to, zda je uzel za domácím NATem nebo na cestách.
3. **Zabezpečení vstupu:** Nulové otevírání portů na domácím routeru. Veškerý vzdálený přístup je chráněn přes Tailscale Funnel s autorizací.

---

## 💡 Proč je toto hardwarové mistrovství klíčové pro IT infrastrukturu a logistiku

1. **Skutečná diagnostika namísto bezhlavé výměny kus za kus:** Když člověk opravuje elektroniku s páječkou v ruce a ladí registry na 15 let starých procesorech, neřeší systémové potíže automatickou výměnou drahého hardwaru. Hledá příčinu v logách jádra, měří teploty, testuje kabeláž a řeší skutečný kořen problému.
2. **Spolehlivost prověřená skladovým provozem:** Ve velkoskladu v Avonmouthu znamená výpadek Wi-Fi na RF skeneru nebo zaseknutý tiskový spooler na tiskárně Zebra okamžité zastavení expedice a zpoždění kamionů. Schopnost postavit stabilní systém na hardwarových limitech zaručuje stejnou nekompromisní spolehlivost i v podnikovém prostředí.
3. **Nulové plýtvání zdroji:** Znalost toho, jak vyždímat maximum z limitovaného křemíku, se přímo promítá do psaní efektivního, optimalizovaného kódu a návrhu cloudových architektur, kde se za každý megabyte RAM platí penězi.

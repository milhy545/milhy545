# 🔧 Stanislav "Milhy" Muller

### SysAdmin | Vibe Coder | Bývalý skladový operátor | Hardwarový pragmatik
📍 *Newport, South Wales, UK* | 🇬🇧 *Britské standardy & Otevřený pozicím v IT infrastruktuře, logistice a systémové podpoře*  

[![Live Showcase](https://img.shields.io/badge/PORTFOLIO-LIVE_SHOWCASE-2ea44f?style=for-the-badge&logo=githubpages&logoColor=white)](https://milhy545.github.io/milhy545-showcase/)
[![LinkedIn](https://img.shields.io/badge/LINKEDIN-SPOJIT_SE-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/stanislav-muller)
[![Docs EN](https://img.shields.io/badge/DOCS-ENGLISH-blue?style=for-the-badge)](./README.md)

> *"Pokud systém spolehlivě běží na starém Core 2 Quad, v cloudu doslova poletí. A pokud přežije provoz v mrazáku při -25 °C, přežije v podnikové produkci cokoliv."*

---

## 👨‍💻 Propojení fyzické logistiky a IT infrastruktury

Než jsem přešel na plný úvazek k administraci Linuxu, automatizaci a orchestraci AI („Vibe Coding“), strávil jsem **7 let přímo na ploše velkých distribučních center ve Velké Británii (Avonmouth)** řízením retraku (Reach Truck), prací s hlasovým vychystáváním a ručními RF terminály, podložených **12 lety elektrotechnické diagnostiky na úrovni součástek**.

Ve velkých skladech a logistice **se výpadky neměří na sekundy, ale na zpožděné kamiony a neodbavené palety**:
- Když Wi-Fi roaming ve skladu shodí spojení na RF skeneru uprostřed zaskladňování, práce stojí.
- Když průmyslová termotiskárna Zebra zasekne tiskový spooler nebo ztratí ovladač, expedice kolabuje.
- Když Warehouse Management System (WMS) ztratí soketové spojení, celá automatická linka se zastaví.

Nepíšu skripty jen pro efekt; stavím odolné a robustní systémy navržené tak, aby bezpečně ustály reálný provozní chaos.

---

## 🚀 Reálně funkční nástroje a produkční systémy
*Aktivní, v praxi prověřený software navržený k řešení konkrétních provozních a hardwarových úzkých hrdel.*

### 🎮 [Steam-VRAM-Manager](https://github.com/milhy545/Steam-VRAM-Manager)
**Desktopově agnostický orchestrátor GPU VRAM a lokálních LLM**
- **Reálný problém:** Běh lokálních jazykových modelů (`llama.cpp` / `llama-server` na plný offload do GPU) zabírá **~5.38 GB VRAM**. Spuštění moderní Steam hry na 6GB grafice (GTX 1060) způsobí okamžitý kolaps na Out-Of-Memory (Vulkan crash).
- **Inženýrské řešení:** Univerzální wrapper navázaný na životní cyklus hry ve Steamu a systémové `systemd` démony. Před startem hry čistě zastaví `llama.service`, uvolní CUDA kontext (5.4 GB volných), aktivuje NVIDIA PRIME offload a hru pustí s plnou 6GB pamětí. Po vypnutí hry dialogové okno (kdialog/zenity/yad) s 60sekundovým odpočtem automaticky vrátí AI službu zpět do chodu.
- **Dokumentace:** [Anglický README](https://github.com/milhy545/Steam-VRAM-Manager/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/Steam-VRAM-Manager/blob/main/README.cz.md)

### 🛡️ [MyVoiceTranslator](https://github.com/milhy545/MyVoiceTranslator) *(Milhy's Interview Shield)*
**Nízkonákladový real-time STT a překladový štít (EN ➔ CS)**
- **Reálný problém:** Překonání technické jazykové bariéry v reálném čase při britských online pohovorech a odborných školeních bez závislosti na pomalém cloudu.
- **Inženýrské řešení:** Odlehčené Python Textual TUI s **CPU-first fallback strategií** a přímým PipeWire/PulseAudio zvukovým loopbackem. Nabízí automatické logování relace do Markdownu a instalaci jedním příkazem (`~/.local/bin/myvoice`).
- **Dokumentace:** [Anglický README](https://github.com/milhy545/MyVoiceTranslator/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/MyVoiceTranslator/blob/main/README.cz.md)

### 🧠 [Orchestration Platform](https://github.com/milhy545/orchestration)
**14-kontejnerová Docker MCP platforma a paměťová páteř**
- **Architektura:** Kompletní multi-agentní systém provozující 14 modulárních mikroservis přes Docker (Filesystem, Git, Terminal, Database, Memory, FORAI Code Tracking, Qdrant vektorová paměť a Marketplace).
- **Hardwarová ironie:** Tento centrální mozek celé sítě běží na **nejstarším a nejslabším hardwaru v celém mém labu**. Nástroje MCP a API brány nepotřebují gigahertze hrubého výkonu procesoru – potřebují stabilní RAM a nepřetržitou síťovou dostupnost. Provozování nervové soustavy na starém železe dokazuje maximální efektivitu.
- **Dokumentace:** [Anglický README](https://github.com/milhy545/orchestration/blob/master/README.md) | [Česká dokumentace](https://github.com/milhy545/orchestration/blob/master/README.cz.md)

### ⚡ [PowerManagement](https://github.com/milhy545/PowerManagement)
**Správa napájení Linuxu, kontrola MSR registrů a thermal throttling**
- **Reálný problém:** Osazení podstatně výkonnějšího procesoru do All-in-One PC z roku 2010 vedlo k extrémnímu přehřívání a nouzovému vypínání při 82 °C.
- **Inženýrské řešení:** Vlastní suite pro správu napájení přistupující přímo k MSR (Model-Specific Registers) procesoru. Dynamicky krokuje frekvence, řídí PWM křivky ventilátorů a multiplexuje vytížení jader, aby zabránil tepelnému kolapsu.
- **Dokumentace:** [Anglický README](https://github.com/milhy545/PowerManagement/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/PowerManagement/blob/main/README.cz.md)

---

## 🧪 Znalostní laby a inženýrské případové studie
*Hluboké technické experimenty, kde nedokončený kód přinesl hluboké porozumění systémům a limitům hardwaru.*

### 📺 [RPi-TV Dashboard](https://github.com/milhy545/RPi) *(Tuning Linuxového jádra a CPU afinity)*
- **Co mě to naučilo:** Vyždímat plynulé přehrávání 1080p streamů a Steam Link z hardwarově limitovaného 4jádrového ARM Raspberry Pi.
- **Orchestrace jader:**
  - **Core 0:** Dedikováno výhradně pro síťový stack, Wi-Fi a Bluetooth přerušení (IRQ šum).
  - **Core 3:** Zamčeno pro ALSA zvukový subsystém (eliminace praskání a zpoždění zvuku).
  - **Cores 1 & 2:** Dedikováno pro přehrávač MPV s dynamickým přeléváním špiček na Core 3 při překročení 160% zátěže.
- **Dokumentace:** [Anglický README](https://github.com/milhy545/RPi/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/RPi/blob/main/README.cz.md)

### 📚 [kindle_butler](https://github.com/milhy545/kindle_butler) *(Automatizace USB periferií přes Linux udev)*
- **Co mě to naučilo:** Reakce na události Linuxového jádra a správa periferií přes `udev` pravidla.
- **Implementace:** Automatická synchronizace po připojení USB kabelu, integrace Gemini AI pro normalizaci metadat a reformátování složitých technických tabulek do textu čitelného na E-Ink displeji.
- **Dokumentace:** [Anglický README](https://github.com/milhy545/kindle_butler/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/kindle_butler/blob/main/README.cz.md)

### 🔑 [Unification](https://github.com/milhy545/Unification) *(Kronika SSH pekla)*
- **Co mě to naučilo:** Zdokumentovaný post-mortem z více než 150 chyb a slepých uliček při správě SSH klíčů, portů a vnořených tmux relací na různých serverech. Důvod, proč jsem přešel na striktní automatizaci.
- **Dokumentace:** [Anglický README](https://github.com/milhy545/Unification/blob/main/README.md) | [Česká dokumentace](https://github.com/milhy545/Unification/blob/main/README.cz.md) | [Kronika SSH pekla (EN)](https://github.com/milhy545/Unification/blob/main/docs/stories/ssh-hell-chronicle-en.md)

### 💡 Inženýrský obrat: MyCoder ➔ `pi`
- **Architektonická lekce:** Přúvodně jsem vyvíjel vlastní kódovací CLI (`MyCoder`). Ve chvíli, kdy vyšel open-source nástroj `pi` (`p-coding-agent`), který byl modulární, lehký a dělal přesně to samé bez zbytečného balastu, jsem vývoj MyCoderu okamžitě ukončil.
- **Seniorní přístup:** Skutečný inženýr neztrácí čas vymýšlením kola, když existuje vynikající open-source nástroj, který vyřeší problém lépe.

---

## 🛠️ Technologický stack & Hardwarový lab

| Kategorie | Technologie & Nástroje |
| :--- | :--- |
| **Operační systémy & Shell:** | Debian / MX Linux, Raspberry Pi OS, Bash, Zsh, Oh My Zsh, tmux |
| **Kontejnery & Virtualizace:** | Docker, Docker Compose, systemd user services, QEMU/KVM |
| **Sítě & Topologie:** | Tailscale (WireGuard mesh), SSH automatizace, PipeWire / PulseAudio |
| **Jazyky & Ekosystém:** | Python (uv, Textual, FastAPI), Node.js, Shell skripty, Git, GitHub Actions |
| **AI & Inference:** | `llama.cpp` (NVIDIA CUDA offload), Model Context Protocol (MCP), Pi, Codex, AGY |
| **Uzly v síti:** | [Kompletní architektura flotily](./docs/hardware-fleet.cz.md) & [`data/hardware-fleet.json`](./data/hardware-fleet.json) — MILHY-PC (i5/GTX 1060), HAS (Alpine/vestavěná UPS), OptiPlex (úložiště/Coder NAS), Acer AIO, RPi TV |

---
*Vytvořeno s důrazem na GitOps disciplínu — Kontakt: [GitHub Profil](https://github.com/milhy545)*

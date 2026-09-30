# 🔧 Stanislav "Milhy" Muller

### SysAdmin | Vibe Coder | Bývalý skladový operátor | Hardwarový pragmatik
📍 *Newport, Jižní Wales, UK* | 🚀 *Otevřen rolím v IT infrastruktuře, Service Desku & logistických technologiích*

> **"Pokud to běží na Core 2 Quad, v cloudu to poletí. A pokud to přežije mrazicí komoru při -25 °C, v ostrém provozu to nespadne."**

---

## 👨‍💻 O mně
Bývalý elektrikář a skladový operátor se 7 lety praxe, přecházející do **správy linuxových systémů, IT infrastruktury a AI vývoje ("Vibe Coding")**.

Propojuji reálný provoz logistiky s IT infrastrukturou. Po letech práce na Reach trucku, s voice pickingem a RF scannery v distribučních centrech v Avonmouthu **přesně vím, co se stane, když vypadne terminál, zasekne se Zebra tiskárna nebo spadne spojení s WMS uprostřed směny: výroba a expedice stojí.**

Můj technický základ tvoří 12 let diagnostiky slaboproudých i silnoproudých systémů až na úroveň součástek v kombinaci s praktickou systémovou administrací: provoz kontejnerizovaných služeb, MCP serverů a lokálních LLM na optimalizovaném moderním i starším hardwaru.

---

## 🖥️ Topologie domácí laboratoře a infrastruktury

* **MILHY-PC (Hlavní pracovní stanice & AI výpočetní uzel):**
  * *Parametry:* Intel Core i5-4690K | 32 GB RAM | NVIDIA GeForce GTX 1060 6GB | MX Linux (Debian)
  * *Zátěž:* Každodenní vývojové prostředí, Docker kontejnery, lokální inference přes `llama.cpp` (Qwen 7B / Mistral).
  * *Vlastní nástroje:* Vlastní dynamická správa VRAM (`steam-gpu-wrap`), která efektivně rozděluje paměť grafické karty mezi AI služby a systém.
* **HAS (Home Automation Server):**
  * *Parametry:* Repurposed laptop (baterie funguje jako vestavěná UPS) běžící na Alpine Linuxu.
  * *Zátěž:* 24 Docker kontejnerů, Home Assistant, AdGuard Home, MQTT a klastr Mega-Orchestrator MCP bezpečně vystavený přes Tailscale Funnel.
* **Optiplex (3xR úložiště & backend):**
  * *Parametry:* Intel Core 2 Quad Q9550 | 16 GB RAM | 256GB SSD + 3TB HDD | Headless Docker Host
  * *Zátěž:* Síťový sklad (Nextcloud) a Coder backend. Praktický důkaz principu **Reuse, Refix, Recycle**.

---

## 🛠️ Technický arzenál

| Kategorie | Stack a nástroje |
| :--- | :--- |
| **Operační systémy** | Linux (Debian, Arch, Alpine, MX Linux), Systemd daemony, SSH klíče a tunely |
| **Logistika & IT Ops** | Diagnostika skladového HW, RF čtečky kódů, Zebra tiskárny štítků, L1 Desktop podpora (Win 11) |
| **Kontejnery & Sítě** | Docker, Docker Compose, Portainer, TCP/IP, základy VLAN, WireGuard, Tailscale, Sing-box |
| **Skriptování & Automatizace**| Bash/Zsh (Oh-My-Zsh), Python (system daemony, API, FastMCP servery), Node.js |
| **AI Orchestrace** | Model Context Protocol (MCP), Pi CLI, AGY (Antigravity), Jules, Claude Code, llama.cpp |
| **Fyzický hardware** | Součástková diagnostika, strukturovaná kabeláž Cat6, rozvaděče, řízení spotřeby a teplot CPU |

---

## 🏗️ Hlavní aktivní projekty

* **[RPi-TV](https://github.com/milhy545/RPi):** Nenáročný televizní dashboard pro Raspberry Pi s Textual TUI rozhraním, go2rtc (WebRTC/RTSP) streamováním a Playwright testy.
* **[orchestration](https://github.com/milhy545/orchestration):** Modulární Mega-Orchestrator agregující Model Context Protocol (MCP) služby napříč lokálním hardwarem s Qdrant vektorovou databází.
* **[PowerManagement](https://github.com/milhy545/PowerManagement):** Linux Power Suite s řízením MSR registrů pro kontrolu frekvencí a teplot vícejádrových procesorů.
* **[reed-openapi-spec](https://github.com/milhy545/reed-openapi-spec):** Čistá specifikace OpenAPI pro agregaci britského pracovního trhu.

---

## ⚡ Proč je tato kombinace klíčová pro IT podporu

1. **Znalost skladové reality:** IT podporu nevnímám jako sezení v kanclu u ticketů. Vím, jaký je tlak na pick targety, střídání směn a časové okno nakládky kamionů.
2. **Hardwarová diagnostika:** 12 let elektromechaniky znamená, že nerestartuji naslepo, ale proměřím kabely, ověřím kontinuitu a vyřeším příčinu problému.
3. **Pragmatická automatizace:** Píšu skripty a stavím kontejnery, abych odstranil zbytečnou manuální rutinu a provozní záseky.

---

## 📬 Kontakt & Odkazy
* **GitHub:** [github.com/milhy545](https://github.com/milhy545)
* **LinkedIn:** [linkedin.com/in/stanislav-muller](https://www.linkedin.com/in/stanislav-muller)
* **Lokalita:** Newport, South Wales (NP19 7LY)

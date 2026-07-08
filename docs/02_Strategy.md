# DömösAiTech AI Ügynök Ökoszisztéma Stratégia (2026.07.06)

## Visió
Piacvezető, európai szabványoknak megfelelő, decentralizált AI szolgáltatóvá válni multi-szektor (ökoház, vállalat, kormányzat, tartalomgyártó) felhasználással, kiberbiztonsági védelemmel, felhasználói élmény központú megközelítéssel.

## Célpiacok és Szektorok

### 1. Smart Home / Okosotthon
- **Célcsoport**: Lakossági felhasználók, IoT integrátorok
- **Termék**: SiriHU (már létező lokális magyar hangasszisztens)
- **Integráció**: HomeKit, Home Assistant, Matter protokoll
- **Differenciáló tényező**: 100% lokális adatfeldolgozás, magyar nyelv, EU szabványok

### 2. Vállalati / Enterprise
- **Célcsoport**: KKV-k, nagyvállalatok, közszféra
- **Termék**: Decentralizált agent hálózat (CARL, Franz, DrHans, MyJarvis)
- **Integráció**: GDPR compliance, auditálható működés, eIDAS
- **Differenciáló tényező**: Szuverén AI, adatok nem hagyják el a vállalatot

### 3. Kormányzati / Government
- **Célcsoport**: Közigazgatás, egészségügy, oktatás
- **Termék**: Compliance-first AI asszisztensek
- **Integráció**: EU AI Act Article 6 (high-risk), Article 53 (GPAI)
- **Differenciáló tényező": Teljes auditálhatóság, szabványos riportolás

### 4. Tartalomgyártó / Content Creator
- **Célcsoport**: Szerkesztőségek, influencer-ek, oktatók
- **Termék**: NotebookLM + Hermes hibrid ("második agy")
- **Integráció**: Research brain + orchestration layer
- **Differenciáló tényező": Adat-szuverenitás, lokális modellek

## Technológiai Stack és Architektúra

### Core Rétegek (LOKA / OAP ihlette)
```
L5: Application Layer - SiriHU, MyJarvis, CARL, Franz
L4: Orchestration Layer - Hermes Agent, Genesis Orchestrator
L3: Agent Protocol Layer - MCP, A2A, Inai Protocol
L2: Identity & Trust Layer - DID/VC (eIDAS compliant), OAP OAEP
L1: Compute Layer - Lokális MLX/Ollama, DePIN (Akash, Phala, io.net)
L0: Storage Layer - Obsidian vault, SQLite, IPFS
```

### Agent Hálózat (Inai ihlette)
| Agent | Szerep | Provider | Status |
|---|---|---|---|
| CARL v7.2 | Memory archivist, SmartRouter | jarvis-server | Élesben |
| Franz | Kódoló agent, fejlesztési ciklusok | ollama-launch | Élesben |
| DrHans | Diagnosztika, debug | genesis-ai | Élesben |
| MyJarvis | Orchestrator, fő platform | nous | Élesben |
| Hermes | Fejlesztési asszisztens (ez!) | nous | Élesben |
| Pi | Kódgenerálás, részletes feladatok | ollama-launch | Élesben |

### Kiberbiztonsági Védelem
- **Zero Trust Architektúra**: Minden agentnek verifiable identity
- **End-to-end encryption**: DIDComm v2, mátrix titkosítás
- **Sandboxing**: Minden agent izolált környezetben fut
- **Audit trail**: Minden interakció JSONL naplózás (CARL)
- **Self-Improving Agent**: Automatikus hibajavítás, Defender protokoll

## EU AI Act Compliance Roadmap

### Phase 1: Foundation (2025 Q4 - 2026 Q2)
- [x] Lokális modellek (nincs cloud dependency)
- [x] DID/VC identitás kezdeményezése
- [x] GDPR compliance by design
- [ ] Technical documentation standardizálása (Annex XI)
- [ ] Model card készítése minden nyilvános modellre
- [ ] AI literacy program szervezése

### Phase 2: High-Risk Ready (2026 Q2 - 2027 Q2)
- [ ] Conformity assessment folyamat kidolgozása
- [ ] Risk management system (ISO 31000 ihlette)
- [ ] Human oversight mechanism-ek
- [ ] Bias detection és mitigation
- [ ] EU AI Act Article 6 compliance audit

### Phase 3: Full Certification (2027 Q2+)
- [ ] CE jelzés megszerzése high-risk termékekre
- [ ] Nemzeti hatósággal való regisztráció
- [ ] Folyamatos monitoring és riporting rendszer

## Üzleti Modell és Bevétel

### Subscription Tiers
1. **Personal** (Smart Home): Havi €9.99 - SiriHU, lokális agent-ek
2. **Pro** (Vállalati): Havi €49.99 - Multi-agent, team kollegiálás
3. **Enterprise** (Government): Egyedi árazás - Teljes compliance, dedikált támogatás
4. **Creator** (Tartalom): Havi €19.99 - NotebookLM integráció, research pipeline

### Resales / Partner Program
- **System Integratorok**: 30% reseller margin
- **IoT Gyártók**: White-label SiriHU integráció
- **Közigazgatási beszállítók**: EU-s szabványokra pályázatok
- **Oktatási intézmények**: Kedvezményes licenc, oktatási csomag

## Konkurencia Elemzés és Differenciáló Tényezők

| Szolgáltató | Erősség | Gyengeség | DömösAiTech Előny |
|---|---|---|---|
| OpenAI / ChatGPT | Minőség, skála | Zárt, USA, nem GDPR-safe | Szuverén, lokális, EU |
| Anthropic Claude | Biztonság | Drága, zárt | Hasonló minőség, nyíltabb |
| Google / Gemini | Integráció | Adatéhség, USA | Magyar nyelv, helyi adat |
| Mistral AI | Európai | Korai szakasz, kevés integráció | Már működő ökoszisztéma |
| D･･m･sAiTech | Szuverén, lokális, magyar | Skála, brand | Egyetlen magyar nyelvű, EU-s, lokális AI stack |

## Következő Lépések
1. **SiriHU** befejezése és publikálás (Q3 2026)
2. **Agent hálózat** standardizálása (Inai/OAP kompatibilis)
3. **EU AI Act** compliance dokumentáció elkészítése
4. **Resales partner** program indítása
5. **Pályázati** anyagok készítése (Horizon Europe, NFU)

## Rizikók és Mitigáció
| Rizikó | Valószínűség | Hatás | Mitigáció |
|---|---|---|---|
| EU AI Act változások | Közepes | Magas | Rugalmas architektúra, proaktív monitoring |
| Nagy tech cégek versenye | Magas | Magas | Nich stratégia, szuverenitás fókusz |
| Skálázási nehézségek | Közepes | Közepes | DePIN compute, cloud hybrid |
| Tehetség felvétel | Közepes | Magas | Nyílt forráskód, közösség építés |

---
*Létrehozva: 2026.07.06 | Szerző: Hermes AI*
*Kapcsolódó fájlok: 01_Kutatas_Eredmenyek.md*

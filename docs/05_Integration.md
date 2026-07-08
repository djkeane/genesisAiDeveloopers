# OpenClaw + OpenCode Integrációs Kutatás és Együttműködési Minták (2026.07.06)

## Áttekintés

**OpenClaw** = Saját AI asszisztens gateway (lokális, multi-channel, plugin-alapú)
**OpenCode** = Nyílt forráskódú AI kódoló agent (terminal-alapú, multi-agent)

A kettő kombinációja egy **"agyközpont + végrehajtókar"** modellt alkot.

---

## 1. Együttműködési Minták (Cooperation Patterns)

### Pattern A: Controller Skill (Közvetlen Vezérlés)
- OpenClaw `opencode-controller` skill-je elindítja az OpenCode-ot parancssorból
- OpenClaw = parancs kiadója, OpenCode = végrehajtó
- **Használat**: Egy-kattintásos kódfeladatok Telegramról/Discordról
- **Parancs**: `opencode run --agent sisyphus "implement JWT auth"`

### Pattern B: ACP Protokoll (Agent Client Protocol)
- OpenCode ACP szerverként fut (`opencode acp` vagy `opencode serve`)
- OpenClaw JSON-RPC üzeneteket küld a 8080-as porton keresztül
- **Használat**: IDE-szerű, folyamatos kollaboráció, monitorozható folyamat
- **Előny**: Valós idejű progress tracking, tool call event-ek láthatók

### Pattern C: OpenResponses API (Universal Bridge)
- Bármely külső agent bekapcsolható OpenClaw-ba egy adapter szerverrel
- POST `/v1/responses` végpont implementálása
- **Használat**: Ha OpenCode más frameworkbe (LangChain, CrewAI) van csomagolva
- **Előny**: Framework-agnostic, model-agnostic

### Pattern D: Plan → Execute Workflow (Elválasztott Tervezés/Végrehajtás)
1. **OpenClaw Plan Agent** (Prometheus mód): Elemzés és architektúrális terv
2. **OpenCode Build Agent** (Atlas mód): Kód implementálás a terv alapján
3. **OpenCode Explore Agent**: Kódbázis feltárás és review
- **Előny**: A tervezés nem módosít fájlokat, a végrehajtás fókuszált

### Pattern E: Brain + Hands (Aszinkron Munkavégzés)
- Nappal: Te az OpenCode-t használod interaktív terminal fejlesztésre
- Éjszaka/hétvégén: OpenClaw cron job indít OpenCode batch feladatokat
- **Példa**: `cron` minden éjjel 2-kor `opencode run --agent build "refactor legacy module"`

### Pattern F: Multi-Agent Routing (OpenClaw Gateway)
- OpenClaw több izolált agentet futtat egy gatewayben
- Minden agentnek saját workspace, session store, tool profilja van
- **Használat**: A mi 10 ügynök csapatának mindegyike külön OpenClaw agent lehet

---

## 2. OpenCode Multi-Agent Architektúra

| Agent | Szerep | Tool Hozzáférés |
|---|---|---|
| **build** | Alapértelmezett, teljes kódolás | Minden tool (write, edit, bash, stb.) |
| **plan** | Tervezés és elemzés | Csak olvasási tool-ok |
| **general** | Általános sub-agent | Majdnem minden tool |
| **explore** | Gyors kódfeltárás | Csak kereső tool-ok |
| **scout** | Külső dependency kutatás | Read-only + web fetch |
| **compaction** | Kontextus tömörítés | Belső, nem választható |
| **title** | Session cím generálás | Belső, nem választható |

**Delegáció**: A `build` agent `@explore` megemlésével indíthat sub-agentet

---

## 3. OpenClaw Tanulási Módok (Learning Modes)

### 3.1 Passzív Tanulás (Passive Learning)
- **Mit csinál**: Rögzíti, hogy mely tool-okat és skill-eket használja a modell
- **Hogyan**: Thompson Sampling Bayesian bandit minden "arm"-re (tool/skill)
- **Output**: Posterior statisztikák — mely tool-ok segítenek, melyek nem
- **Konfig**: `"learning.phase": "passive"` (alapértelmezett)

### 3.2 Aktív Tanulás (Active Learning)
- **Mit csinál**: Token budget alapján kiválasztja a leghasznosabb tool-okat/skill-eket
- **Hogyan**: Thompson Sampling + token budget (pl. 8000 token)
- **Output**: Csak a releváns tool-ok kerülnek a promptba → token megtakarítás
- **Konfig**: `"learning.phase": "active"`

### 3.3 OpenClaw-RL (Megerősítéses Tanulás)
- **Forrás**: github.com/Gen-Verse/OpenClaw-RL
- **Két módszer**:
  - **Binary RL (GRPO)**: User feedback (👍/👎) → PRM reward model → policy update
  - **OPD (On-Policy Distillation)**: Rich textual feedback („használd inkább ezt a könyvtárat”) → token-level tanulás
- **Async**: Szolgáltatás, judging, training 3 független loop
- **Gyakorlati eredmény**: 36 interakció után már szignifikáns javulás

### 3.4 EvoClaw (Skill Evolúció)
- **Forrás**: github.com/evoclaw-agent/evoclaw
- **Mit csinál**: PRM scoring + skill injection + LoRA training Tinker cloud-on
- **Folyamat**:
  1. Intercept üzenet
  2. PRM score (0.0-1.0)
  3. Releváns skill-ek beinjektálása
  4. Buffer turn → batch N darab
  5. LoRA training cloud-ban
  6. Hot-swap weights → agent fejlődik

### 3.5 Self-Learning Loop (Automata Skill Készítés)
- **Forrás**: github.com/CassiaResearch/openclaw-self-learn
- **Szabály**: Ha egy task 5+ tool call-t használ, és reusable, és novel → auto skill creation
- **3 kérdés evaluáció**:
  1. Count: 5+ tool call?
  2. Reusable: Hasznos más sessionben?
  3. Novel: Nem triviális megoldás?
- **Output**: `skills/self-learned-<név>/SKILL.md`

---

## 4. Hiányzó Skill-ek a DömösAiTech Stackhez

| Skill | Cél | Prioritás |
|---|---|---|
| **opencode-controller** | OpenClaw-ból OpenCode indítása (custom, 10-agent kompatibilis) | 🔴 Magas |
| **openclaw-orchestrator** | Multi-agent routing és delegáció gateway szinten | 🔴 Magas |
| **openclaw-rl-monitor** | OpenClaw-RL/EvoClaw tanulási folyamat monitorozása | 🟡 Közepes |
| **dömosaitech-workflow** | A 10 ügynök csapatának integrált workflow-ja | 🔴 Magas |
| **opencode-acp-bridge** | ACP protokoll kezelése OpenClaw-ból | 🟡 Közepes |
| **auto-skill-curator** | Self-learned skill-ek review, merge, dedup | 🟡 Közepes |

---

## 5. Konfigurációs Példák

### OpenClaw Learning Beállítás
```json
{
  "learning": {
    "enabled": true,
    "phase": "active",
    "strategy": "thompson",
    "tokenBudget": 8000,
    "baselineRate": 0.10,
    "minPulls": 5
  }
}
```

### OpenClaw → OpenCode Provider Regisztráció
```json
{
  "models": {
    "providers": {
      "opencode-local": {
        "baseUrl": "http://localhost:8080/v1",
        "apiKey": "${OPENCODE_API_KEY}",
        "api": "openai-responses",
        "models": [{"id": "build", "name": "OpenCode Build"}]
      }
    }
  }
}
```

### OpenCode Agent Definíció (Markdown)
```markdown
---
name: dömosaitech-architect
description: DömösAiTech rendszertervező agentje
permissions:
  read: allow
  edit: ask
  bash: deny
  task: allow
model: openai/gpt-5.4
---
Te a DömösAiTech fő rendszertervezője vagy...
```

---

*Kutatási források: openclaw.ai/docs, opencode.ai/docs, github.com/Gen-Verse/OpenClaw-RL, github.com/evoclaw-agent/evoclaw, github.com/CassiaResearch/openclaw-self-learn*
*Létrehozva: 2026.07.06*

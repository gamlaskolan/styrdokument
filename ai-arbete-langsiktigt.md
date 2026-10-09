# Underlag — långsiktigt AI-arbete

**Dokumenttyp:** Underlag. Inte en plan, inte ett uppdrag.
**Skapat:** 2026-10-09
**Källa:** Samtal mellan VÅ och DS 2026-10-09.
**Ämne:** Hur människa och AI arbetar tillsammans över tid, med dokumentation som bär mellan sessioner.
**Status:** Vilande. Ingen åtgärd krävs. Ändras bara av VÅ.

---

## Varför detta dokument finns

DS minns inget mellan sessioner. Filerna gör det — se `rollkontrakt.md` → Kontext.
Samtalet handlade om nästa steg i det: vad som händer när fler AI-verktyg än DSH
ska läsa samma filer, och när plapp slutar vara ett privat verktyg.

Detta är vad som sades, sammanfattat. Läs det om sex månader.

---

## 1 — Vad som diskuterades

Fyra frågor drev samtalet:

- **Vem läser dokumentationen?** I dag VÅ och DS. I morgon flera AI-verktyg parallellt.
- **Vad räcker för en extern AI?** Kan en AI klippa in `.md`-filerna och börja arbeta utan förklaring?
- **Behöver plapp en standard?** ISO, Microsofts riktlinjer och LC-OS nämndes som möjliga ramar.
- **Ska en agent sköta dokumentationen?** En agent som bara håller ordning och hjälper andra AI:er följa reglerna.

Frågorna hör till plapp-nivån, men svaren ligger utanför plapp.

---

## 2 — Standarder och ramverk som nämndes

| Namn | Vad det är | Varför det kom upp | VÅ:s hållning |
|---|---|---|---|
| **ISO 9241-210** | Internationell standard för människocentrerad design av interaktiva system. | Gäller om plapp släpps som tjänst. | Bakgrund. Inte nu. |
| **Microsofts riktlinjer för människa-AI-interaktion** | 18 evidensbaserade riktlinjer i fyra faser: vid första mötet, under interaktionen, när systemet har fel, över tid. Från en CHI-artikel 2019. | De fyra kategorierna i samtalet motsvarar dessa faser. | Bakgrund. Inte nu. |
| **LC-OS** (Lean Collaboration Operating System) | Ramverk för långsiktigt människa-AI-samarbete. Begreppen som nämndes: Running Documents, Step Mode, Challenge Protocol, Error-Recovery Protocol, Stability Pings. | Beskriver samma problem som filerna redan löser. | Bakgrund. Inte nu. Källa ej verifierad av DS. |
| **AGENTS.md** | Öppet format — "en README för agenter". En fil i roten som kodagenter läser nativt: Codex, Cursor, Gemini CLI, VS Code med flera. Drygt 60 000 öppna projekt använder den. Förvaltas av Agentic AI Foundation under Linux Foundation. | Låter en extern AI börja arbeta utan förklaring. | Bra. Ligger efter plapp. |
| **CLAUDE.md / GEMINI.md / AGENT.md** | Tunna omdirigeringar till samma innehåll som `AGENTS.md`. | Undviker en fil per verktyg. | Samma beslut som `AGENTS.md`. |
| **Conversation Journal** | Protokoll för automatiskt sparande av beslut och fel per session. | Löser "DS minns inget" med automatik i stället för rutin. | Ej beslutat. Källa ej verifierad av DS. |
| **A2A** (Agent2Agent) | Protokoll för agent-till-agent-kommunikation. Från Google, överlämnat till Linux Foundation. | Skulle låta agenter prata med varandra i stället för via filer. | Provat av VÅ med LAI — problemen löstes inte. Inte nu. |
| **Dokumentationsagent** | En agent som bara sköter dokumentation och hjälper andra AI:er att arbeta efter reglerna. | Reglerna finns — någon måste hålla dem levande. | Eget framtida projekt. Inte nästa steg. |

---

## 3 — VÅ:s hållning

- **ISO och LC-OS är för stora för plapp i dag.** De får ligga i bakgrunden som principer, och blir aktuella först om plapp släpps som tjänst.
- **Det som behövs först är dokumentationen.** Tillräckligt bra för att en extern AI ska kunna klippa in `.md`-filerna och börja arbeta utan förklaring.
- **AGENTS.md är nästa naturliga steg — efter plapp.** Idén är bra, ordningen är plapp först.
- **Dokumentationsagenten är ett eget framtida projekt.** Inte ett nästa steg.
- **A2A är provat och lämnat.** Det löste inte problemen.

---

## 4 — Best practice i dag

- **En ingång, inte många.** `start_har.md` är startpunkten. Läsordningen står där och på ett ställe.
- **Kort och specifikt slår långt och generellt.** En regel som går att följa slår en sida som går att tolka.
- **Pekare slår kopior.** Gäller redan som regel — se `regelverk.md` DEL 7.
- **Skrivet slår kommet ihåg.** Det som inte står i filerna finns inte.
- **Ett format som alla läsare förstår.** Vanlig Markdown, inga proprietära register — se INV10 i `plapp.md` DEL 5.
- **`AGENTS.md`-mönstret i sig:** en fil i roten, skriven för maskin, som pekar vidare i stället för att upprepa.

---

## 5 — Vad som INTE ska göras nu

- Ingen ISO-implementering, ingen certifiering, ingen processmodell.
- Inget A2A-ramverk.
- Ingen agent-arkitektur — ingen dokumentationsagent, ingen AI-organisation — förrän plapp fungerar.
- Ingen `AGENTS.md` i roten förrän plapp är klart.
- Ingen ny fil som upprepar `rollkontrakt.md` eller `regelverk.md`. Pekare, inte kopior.

---

## 6 — Vad DS inte vet

- **LC-OS.** Var ramverket kommer ifrån, och om det är publicerat eller VÅ:s eget. De fem begreppen är återgivna som de sades i samtalet.
- **Conversation Journal.** Samma sak — källa ej verifierad.
- **LAI.** Vad förkortningen står för i detta sammanhang.
- **Om DSH läser `AGENTS.md` i dag.** Inte prövat.

---

**Slut på underlaget.**

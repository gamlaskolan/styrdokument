# {{NAMN}} — arkitekturen

**Version:** 0.1
**Status:** Låst. Ändras bara vid beslut av VÅ.
**Dokumenttyp:** Arkitektur och teknisk specifikation

---

## DEL 0 — VAD DETTA DOKUMENT ÄR

Detta är arkitekturen för {{NAMN}}.

Det beskriver **vad systemet är** och **vad som är låst**. Inte stegen för att
bygga det. Stegen och läget bor i `projektplan.md`. Rollkontraktet bor i
`styrdokument/rollkontrakt.md`.

Om detta dokument och `projektplan.md` säger olika om arkitekturen — detta
dokument vinner. Om detta dokument och verkligheten säger olika — verkligheten
vinner, och detta dokument uppdateras.

---

## DEL 1 — SYSTEMETS MÅL

{{SYSTEMETS_MAL}}

---

## DEL 1B — ARKITEKTPRINCIPER (LÅSTA)

De fyra principerna styr hur systemet byggs — filstruktur, modulgränser,
sanning och grindar. De är låsta på samma sätt som kärnbegreppen i DEL 3.
Rubrikerna nedan är fältens namn i fliken "Nytt projekt" (cell 4, Struktur);
platshållarna fylls av formuläret.

**En fil äger en sak**
{{EN_FIL_AGER_EN_SAK}}

**Korta moduler och kontextgräns**
{{KORTA_MODULER_OCH_KONTEXTGRANS}}

**Single Source of Truth**
{{SINGLE_SOURCE_OF_TRUTH}}

**Körbar grind framför skriftliga påminnelser**
{{KORBAR_GRIND_FRAMFOR_SKRIFTLIGA_PAMINNELSER}}

---

## DEL 2 — ORGANISATION (LAGER)

Systemet har tre lager. Regeln är fast: **UI pratar aldrig direkt med lagring.
UI pratar med logiken. Logiken pratar med lagring.**

┌─────────────────────────────┐
│ UI (tkinter idag)           │ ← bytbar
├─────────────────────────────┤
│ Logik (regler, data)        │ ← stabil
├─────────────────────────────┤
│ Lagring (Markdown)          │ ← AI-gränssnittet
└─────────────────────────────┘

**Varför:** när VÅ vill byta från tkinter till något modernt byts bara UI-lagret.
Logik och lagring är orörda. Koden ligger därefter: `produktion/main.py` är UI,
`produktion/logik/` är logiken, `produktion/ui/` är ledigt för nya UI-delar.

**Projektets mapp:**

projekt/{{SLUG}}/
├── projektplan.md
├── {{SLUG}}.md
├── ai.md
├── va.md
├── data/
│   └── logg.jsonl
└── produktion/
    ├── logik/
    └── ui/

---

## DEL 3 — KÄRNBEGREPP (LÅSTA)

Dessa begrepp får inte omdefinieras i senare faser.

{{KARNBEGREPP}}

**Regler:**
- Markdown är sanningen. Inget JSON-register. Inget dubbelt register.
- En panel tillhör exakt en flik.
- En flik har minst en panel.

---

## DEL 4 — DATAFLÖDE (LÅST)

Användare → UI → Logik → Lagring (Markdown)
                              ↑
                        AI läser Markdown direkt

Fyra relationer:

1. Användare → UI (klick, skriv)
2. UI → Logik (funktionsanrop)
3. Logik → Lagring (läs/skriv)
4. AI → Lagring (läser direkt, utanför appen)

**UI → Lagring är förbjudet.** Om UI behöver data frågar den logiken.

---

## DEL 5 — SYSTEMINVARIANTER

Testbara påståenden. Varje invariant ska kunna köras mot koden.

{{INVARIANTER}}

---

## DEL 6 — DATAMODELLEN (LÅST)

{{DATAMODELL}}

---

## DEL 7 — APPENS UTSEENDE

{{TOMT}}

---

## DEL 8 — ARKITEKTONISKA TESTFALL (LÅSTA)

{{TOMT}}

---

## DEL 9 — DETTA ÄR INTE MED

- Ingen data i Steg 1
- Ingen flik i Steg 1
- Ingen logik i Steg 1
- Ingen AI-koppling i Steg 1
- Ingen JSON i Steg 1
- Ingen Git-integration i appen
- Inga filuppladdningar
- Inget JSON-register
- Ingen proprietär struktur som bara detta projekt förstår

Om ett framtida steg kräver att ett kärnbegrepp ändras — då är steget fel
avgränsat, inte kärnan.

---

**Slut på arkitekturen.**

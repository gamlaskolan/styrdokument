# PROJEKTMALL — de fyra filerna

**Dokumenttyp:** Styrdokument. Mall.
**Status:** Låst. Ändras bara vid beslut av VÅ.
**Gäller:** Alla projekt under `projekt/`.

Denna fil är kontraktet för vad ett nytt projekt är. Fliken "Nytt projekt" i
plapp bygger mot den. En ny chatt läser mappen — inget mer behövs.

`projektplan.md` samlar sedan 2026-10-09 det som förut låg i två filer: mål,
syfte, struktur, arbetsgång, checklista och status.

---

## DEL 1 — MAPPEN

**Mappnamn:** `projekt/{{SLUG}}/`

- `{{SLUG}}` = **hela mappnamnet, inklusive numret** — `miniraknare-001`. Koden bygger det av projektets namn: gemener, `å ä ö` → `a a o`, mellanslag och skiljetecken → `-`.
- Namn utan nummer får `-001` pålagt. Är numret upptaget ger appen nästa lediga i samma serie.
- Datumet står inte i mappnamnet sedan 2026-10-09.
- Exempel: `projekt/miniraknare-001/`
- **Skriv aldrig `{{SLUG}}-001`:** `{{SLUG}}` innehåller redan numret, och `{{SLUG}}-001` skulle ge `miniraknare-001-001`.

**Dubblett:** om mappen redan finns läggs suffix till: `-2`, `-3`, och så vidare.
Appen skriver aldrig över en befintlig mapp.

**Mappstruktur:**

```
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
```

**Mappar** skapas när projektet skapas — inte vid behov: `data/` och
`produktion/` med `logik/` och `ui/`. Två mappar i roten, två i produktion/.
`logg.jsonl` skrivs med en rad per skapad fil. Fler mappar finns inte —
`bilder/` ströks 2026-10-09 och `dokument/` + `anteckningar/` ströks
2026-10-10, eftersom koden inte skriver något i dem.

---

## DEL 2 — FÄLTEN I FLIKEN "NYTT PROJEKT"

Platshållare har formen {{NAMN}}. Koden ersätter dem med fältets värde.

Fälten nedan är filernas platshållare — fjorton stycken, i denna ordning. Vilka av
dem appen samlar, och med vilka rubriker, står i `plapp.md` DEL 7. Detta
dokument äger filinnehållet.

| # | Fält | Typ | Hamnar i |
|---|---|---|---|
| 1 | Namn | en rad | `projektplan.md` rubrik + `{{SLUG}}.md` rubrik |
| 2 | Konkreta leverabler | flerradig | `projektplan.md` → `**Konkreta leverabler**` |
| 3 | Definition of Done (DoD) | flerradig | `projektplan.md` → `**Definition of Done (DoD)**` |
| 4 | Prioriteringsordning vid kravkrock | flerradig | `projektplan.md` → `**Prioriteringsordning vid kravkrock**` |
| 5 | Avgränsning | flerradig | `projektplan.md` → `**Avgränsning**` |
| 6 | Orsaker till regler och förbud | flerradig | `projektplan.md` → `**Orsaker till regler och förbud**` |
| 7 | Riktlinjer vid osäkerhet | flerradig | `projektplan.md` → `**Riktlinjer vid osäkerhet**` |
| 8 | Systemets mål (DEL 1) | flerradig | `{{SLUG}}.md` → DEL 1 |
| 9 | Kärnbegrepp (DEL 3) | flerradig | `{{SLUG}}.md` → DEL 3 |
| 10 | Invarianter (DEL 5) | flerradig | `{{SLUG}}.md` → DEL 5 |
| 11 | Datamodell (DEL 6) | flerradig | `{{SLUG}}.md` → DEL 6 |
| 12 | Saker som ska göras | flerradig → checklista | `projektplan.md` → checklista |
| 13 | Öppna frågor | flerradig | `projektplan.md` → Öppna frågor. `ai.md` pekar dit. |
| 14 | Första anteckningar | flerradig | `va.md` |

**Regler:**
- Alla fjorton fält kan lämnas tomma. Ett tomt fält ger en tom platshållare i
  filen — aldrig borttagen rubrik.
- Fält 1 är en rad. Långa beskrivningar hör i fält 2–7 (`projektplan.md`) eller
  i DEL 1 (`{{SLUG}}.md`).
- Fält 12: en rad per sak. Raderna numreras `1`, `2`, `3` i den ordning VÅ skrev dem.
- **Färg** väljs i paletten vid Spara — 20 färger, obligatorisk. Färgen hamnar i
  `projektplan.md` → `**Färg:**`, och följer projektets knapp och projektets rad.

**Platshållare som koden räknar fram:**

- `{{NASTA}}` — första raden i **Konkreta leverabler**. Om tomt: "Ej angivet".
- `{{N}}` — radnummer i fält 12. 1, 2, 3 ...
- `{{SAK}}` — radens text i fält 12.
- `{{DATUM}}`, `{{DATUM_KORT}}`, `{{SLUG}}` och `{{TOMT}}` — dagens datum i två
  former, mappnamnet, och en tom rad.

`{{FAS1}}` finns inte längre. Fasens namn räknades ur fältet *Saker som ska
göras*, som togs bort ur formuläret 2026-10-09, så rubriken blev alltid
"Fas 1 — Ej namngiven". Raderna står nu som `| Fas 1 |` och `## Fas 1`, och
VÅ skriver fasens namn direkt i `projektplan.md` när fasen börjar.

Värdena räknas fram av koden. Mallen beskriver dem.

**Platshållare som står kvar oskrivna:**

`{{SYSTEMETS_MAL}}`, `{{KARNBEGREPP}}`, `{{INVARIANTER}}` och `{{DATAMODELL}}`
samlar appen inte in — formuläret har inga fält för dem. De står kvar i
`{{SLUG}}.md` som en markering av vad VÅ behöver fylla i, och VÅ skriver
texten för hand. **Att ge dem fält i formuläret kräver en ny panel:** cell 4
är full (fyra fält, filkryss och skrivruta på 278 px). Beslutet är VÅ:s och
står öppet i `projekt/plapp/ai.md`.

`{{OPPNA_FRAGOR}}` finns **bara** i `projektplan.md`. Den ägs av ett ställe —
`ai.md` har rubriken kvar men pekar dit, eftersom en fråga inte ska stå i två
filer.

Samma sak gäller `{{ANTECKNINGAR}}` i `va.md`: fältet Anteckningar togs bort
2026-10-09, och `spara_nytt_projekt()` sätter en tom sträng så att
platshållaren inte blir stående. Ett nytt projekts `va.md` har rubriken och
inget mer.

---

## DEL 3 — FIL 1: `projektplan.md`

Projektets nav. Mål och syfte överst, läget i mitten, arbetsgången och
checklistan under. Det som förut låg i två filer ligger här.

```markdown
# {{NAMN}}

**Färg:** {{FARG}}

**Konkreta leverabler**
{{KONKRETA_LEVERABLER}}

**Definition of Done (DoD)**
{{DEFINITION_OF_DONE_DOD}}

**Prioriteringsordning vid kravkrock**
{{PRIORITERINGSORDNING_VID_KRAVKROCK}}

**Avgränsning**
{{AVGRANSNING}}

**Orsaker till regler och förbud**
{{ORSAKER_TILL_REGLER_OCH_FORBUD}}

**Riktlinjer vid osäkerhet**
{{RIKTLINJER_VID_OSAKERHET}}

**Läget**
**Status:** Fas 0 — inte påbörjad.
**Nästa:** {{NASTA}}

**Filer**
- Startpunkt: ny_chat.md
- Arkitektur: {{SLUG}}.md
- Arbetsgång: projektplan.md
- Lokalt läge: ai.md
- VÅ:s anteckningar: va.md

**AI-läsning**
En extern AI som får denna mapp börjar med `projektplan.md` och följer sedan
filordningen i repots `styrdokument/ny_chat.md`. Appen behövs inte — allt VÅ skriver
står i Markdown, och invarianterna i `{{SLUG}}.md` är garantin för det.
Bilder i mappen är inte data.

**Skapat:** {{DATUM}}
**Uppdaterat:** {{DATUM}}

---

## Arbetsgång

| Fas | Status |
|---|---|
| Fas 1 | 🔄 Pågår |
| Fas 2 | ⏳ Inte öppnad |

> När en fas är klar: flytta stegen till `projektplan_fasN.md`. Checklistan börjar om
> med nästa fas.

## Fas 1

**Checklista — appen läser denna.** Appen visar momenten grupperade efter
markören i checklistan — `[H]` Historik, `[A]` Aktuella, `[K]` Kommande.
Raderna nedan skrivs som `[ ]` och får sin markör när projektet skapas.

<!-- per sak -->
- [ ] {{N}} {{SAK}}
<!-- /per sak -->

Nummer och titel i checklistan måste stämma med rubrikerna nedan.

**Steg i detalj**

<!-- per sak -->
### Steg {{N}} — {{SAK}}
**Vad:**
**Test:**
**Commit:**
<!-- /per sak -->

**JEV-status.** `projektplan.md` använder `[JA]`/`[NEJ]`/`[VET EJ]` på
testrader. Övriga filer gör det inte. Markören betyder "uppfyllt" och hör till
påståenden som kan vara icke-uppfyllda.

- `[JA]` — uppfyllt
- `[NEJ]` — inte uppfyllt
- `[VET EJ]` — behöver utredas

## Öppna frågor

{{OPPNA_FRAGOR}}
```

**Anmärkning:** tom `Saker som ska göras` → checklistan blir tom. Fasen heter
`Fas 1` tills VÅ namnger den.

**Status och Nästa ägs av `projektplan.md`** — mallen skriver dit dem. Fasfilerna (`projektplan_fasN.md`) bär de
avslutade stegen; checklistan i denna fil bär de aktuella.

---

## DEL 4 — FIL 2: `{{SLUG}}.md`

Nio delar. DEL 0, 2, 4, 9 ärvs ordagrant från `projekt/plapp/plapp.md` (med projektets
namn insatt). DEL 1, 3, 5 får VÅ:s text. DEL 6, 7, 8 är tomma platshållare.
Datamodellen (DEL 6) får ingen generisk text — den fylls i av VÅ.

```markdown
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
```

---

## DEL 5 — FIL 3: `ai.md`

```markdown
# AI — lokalt läge för {{NAMN}}

**Rollkontraktet bor i `styrdokument/rollkontrakt.md`.** Läs det först.
**Denna fil är projektets läge.** Vad som är öppet, vad som väntar, vad som
behöver veta just nu.

---

## Läget

- **Fas 0.** Projektet skapat {{DATUM}}. Inte påbörjat.
- **Nästa:** {{NASTA}}

---

## Vad som behöver veta om detta projekt

- Fyra filer: `projektplan.md`, `{{SLUG}}.md`, `va.md`, `ai.md`.
- **Markdown är sanningen.** Inget JSON-register.
- **Arkitekturen bor i `{{SLUG}}.md`.** Det som är låst.
- **Checklistan i `projektplan.md` äger steg-status.** Rubrikerna är beskrivning.

---

## Öppna frågor

Listan står i `projektplan.md`. Skriv bara frågor som hör till just detta projekt.

---

## Vad som görs härnäst

1. Läser i den ordning repots `styrdokument/ny_chat.md` anger.
2. Svarar enligt svarsformen i `ny_chat.md`.
3. Väntar på VÅ:s svar innan arbete börjar.

---

**Uppdaterat:** {{DATUM}}
```

---

## DEL 6 — FIL 4: `va.md`

```markdown
---
id: {{DATUM_KORT}}-001
uppdaterad: {{DATUM}}
typ: va-anteckningar
---

# VÅ — Anteckningar

{{ANTECKNINGAR}}
```

---

## DEL 7 — REGLER FÖR SKAPANDET

1. Klick Spara → mappen skapas → fyra filer skrivs → klart. Projektet är igång.
2. Alla fyra filer skrivs alltid. Ingen fil hoppas över.
3. Befintlig mapp skrivs aldrig över. Suffix `-2`, `-3`.
4. Frontmatter finns **bara** i `va.md`.
5. `{{DATUM}}` — dagens datum, `YYYY-MM-DD`.
6. `{{DATUM_KORT}}` — dagens datum, `YYYYMMDD`. Används i mappnamn och id.
7. Status i `projektplan.md` blir alltid `Fas 0 — inte påbörjad` vid skapandet.
   VÅ ändrar till `Fas 1` när arbetet börjar, och skriver fasens namn i
   rubriken `## Fas 1`.

---

**Slut på projektmallen.**

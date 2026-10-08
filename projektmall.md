# PROJEKTMALL — de fem filerna

**Dokumenttyp:** Styrdokument. Mall.
**Status:** Låst. Ändras bara vid beslut av VÅ.
**Gäller:** Alla projekt under `projekt/`.

Denna fil är kontraktet för vad ett nytt projekt är. Fliken "Nytt projekt" i
Controlltower bygger mot den. En ny chatt läser mappen — inget mer behövs.

---

## DEL 1 — MAPPEN

**Mappnamn:** `projekt/<datum>-<slug>/`

- `<datum>` = `YYYYMMDD`
- `<slug>` = projektets namn: gemener, `å ä ö` → `a a o`, mellanslag och skiljetecken → `-`
- Exempel: `20261008-minnesapp`

**Dubblett:** om mappen redan finns läggs suffix till: `-2`, `-3`, och så vidare.
Appen skriver aldrig över en befintlig mapp.

**Undermappar** skapas vid behov, inte i förväg: `produktion/`, `bilder/`, `data/`.

---

## DEL 2 — FÄLTEN I FLIKEN "NYTT PROJEKT"

Allt VÅ fyller i vid skapandet. Elva fält, i denna ordning.

| # | Fält | Typ | Hamnar i |
|---|---|---|---|
| 1 | Namn | en rad | `projekt.md` rubrik + `<slug>.md` rubrik |
| 2 | Vad | en rad | `projekt.md` → `**Vad:**` |
| 3 | Syfte | en rad | `projekt.md` → `**Syfte:**` |
| 4 | Personal | en rad | `projekt.md` → `**Personal:**` |
| 5 | Systemets mål (DEL 1) | flerradig | `<slug>.md` → DEL 1 |
| 6 | Kärnbegrepp (DEL 3) | flerradig | `<slug>.md` → DEL 3 |
| 7 | Invarianter (DEL 5) | flerradig | `<slug>.md` → DEL 5 |
| 8 | Datamodell (DEL 6) | flerradig | `<slug>.md` → DEL 6 |
| 9 | Saker som ska göras | flerradig → checklista | `pp.md` → checklista |
| 10 | Öppna frågor | flerradig | `ds.md` → Öppna frågor |
| 11 | Första anteckningar | flerradig | `va.md` |

**Regler:**
- Alla elva fält kan lämnas tomma. Ett tomt fält ger en tom platshållare i filen —
  aldrig borttagen rubrik.
- Fält 2 och 3 är enradiga och korta. Långa beskrivningar hör i DEL 1
  (`<slug>.md`).
- Fält 9: en rad per sak. Raderna numreras `1`, `2`, `3` i den ordning VÅ skrev dem.

---

## DEL 3 — FIL 1: `projekt.md`

```markdown
# <Namn>

**Vad:** <Vad>
**Syfte:** <Syfte>

**Läget**
**Status:** Fas 0 — inte påbörjad.
**Nästa:** <första raden i Saker som ska göras, annars "Fyll i Vad och Syfte">

**Personal:** <Personal>

**Filer**
- Startpunkt: START_HÄR.md
- Arkitektur: <slug>.md
- Arbetsgång: pp.md
- Lokalt läge: ds.md
- VÅ:s anteckningar: va.md

**Skapat:** <datum>
**Uppdaterat:** <datum>
```

---

## DEL 4 — FIL 2: `<slug>.md`

Nio delar. DEL 0, 2, 4, 9 ärvs ordagrant från `controlltower.md` (med projektets
namn insatt). DEL 1, 3, 5 får VÅ:s text. DEL 6, 7, 8 är tomma platshållare.
Datamodellen (DEL 6) får ingen generisk text — den fylls i av VÅ.

```markdown
# <NAMN> — arkitekturen

**Version:** 0.1
**Status:** Låst. Ändras bara vid beslut av VÅ.
**Dokumenttyp:** Arkitektur och teknisk specifikation

---

## DEL 0 — VAD DETTA DOKUMENT ÄR

Detta är arkitekturen för <Namn>.

Det beskriver **vad systemet är** och **vad som är låst**. Inte stegen för att
bygga det. Stegen bor i `pp.md`. Läget bor i `projekt.md`. Rollkontraktet bor i
`styrdokument/ROLLKONTRAKT.md`.

Om detta dokument och `pp.md` säger olika om arkitekturen — detta dokument vinner.
Om detta dokument och verkligheten säger olika — verkligheten vinner, och detta
dokument uppdateras.

---

## DEL 1 — SYSTEMETS MÅL

<VÅ:s text>

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
Logik och lagring är orörda.

**Projektets mapp:**

projekt/<datum>-<slug>/
├── projekt.md
├── <slug>.md
├── pp.md
├── ds.md
└── va.md

---

## DEL 3 — KÄRNBEGREPP (LÅSTA)

Dessa begrepp får inte omdefinieras i senare faser.

<VÅ:s text>

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

<VÅ:s text>

---

## DEL 6 — DATAMODELLEN (LÅST)

<tomt — fylls i av VÅ>

---

## DEL 7 — APPENS UTSEENDE

<tomt — fylls i senare>

---

## DEL 8 — ARKITEKTONISKA TESTFALL (LÅSTA)

<tomt — fylls i senare>

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

## DEL 5 — FIL 3: `pp.md`

```markdown
# Produktionsplan — <Namn>

**Detta är arbetsgången.** Vad som gjorts, vad som görs, vad som väntar.
**Status och Nästa bor i `projekt.md`.** Här bor stegen.

> När Fas 1 är klar: flytta stegen till `pp_fas1.md`. `pp.md` börjar om med Fas 2.

---

## Status

| Fas | Status |
|---|---|
| Fas 1 — <första raden i Saker som ska göras, annars "Ej namngiven"> | 🔄 Pågår |
| Fas 2 | ⏳ Inte öppnad |

---

## Fas 1 — <samma som ovan>

**Checklista — appen läser denna.** Appen visar första ockryssade steget + fem
närmaste (`ANTAL_AKTUELLA_STEG = 6`).

- [ ] 1 <sak 1>
- [ ] 2 <sak 2>

Nummer och titel i checklistan måste stämma med rubrikerna nedan.

**Steg i detalj**

### Steg 1 — <sak 1>
**Vad:**
**Test:**
**Commit:**

### Steg 2 — <sak 2>
**Vad:**
**Test:**
**Commit:**

---

## Öppna frågor

<tomt — fylls i av VÅ>

---

**Slut på produktionsplanen.**
```

**Anmärkning:** tom `Saker som ska göras` → rubriken blir `Fas 1 — Ej namngiven`
och checklistan blir tom. Ingen rad hittas på.

---

## DEL 6 — FIL 4: `ds.md`

```markdown
# DS — lokalt läge för <Namn>

**Rollkontraktet bor i `styrdokument/ROLLKONTRAKT.md`.** Läs det först.
**Denna fil är projektets läge.** Vad som är öppet, vad som väntar, vad DS ska
veta just nu.

---

## Läget

- **Fas 0.** Projektet skapat <datum>. Inte påbörjat.
- **Nästa:** <första raden i Saker som ska göras, annars "Fyll i Vad och Syfte">

---

## Vad DS ska veta om detta projekt

- Fem filer: `projekt.md`, `<slug>.md`, `pp.md`, `ds.md`, `va.md`.
- **`projekt.md` äger Status och Nästa.** Inte `pp.md`, inte `ds.md`.
- **Markdown är sanningen.** Inget JSON-register.
- **Arkitekturen bor i `<slug>.md`.** Det som är låst.
- **Checklistan i `pp.md` äger steg-status.** Rubrikerna är beskrivning.

---

## Öppna frågor

<VÅ:s text>

---

## Vad DS gör härnäst

1. Läser i kanonisk ordning: `START_HÄR.md` → `ROLLKONTRAKT.md` → `REGELVERK.md`
   → `projekt.md` → `<slug>.md` → `pp.md` → `ds.md` → `va.md`.
2. Säger LÄST / FÖRSTÅTT / SAKNAS / FRÅGA.
3. Väntar på VÅ:s svar innan arbete börjar.

---

**Uppdaterat:** <datum>
```

---

## DEL 7 — FIL 5: `va.md`

```markdown
---
id: <datum>-001
uppdaterad: <datum>
typ: va-anteckningar
---

# VÅ — Anteckningar

<VÅ:s text>
```

---

## DEL 8 — REGLER FÖR SKAPANDET

1. Klick Spara → mappen skapas → fem filer skrivs → klart. Projektet är igång.
2. Alla fem filer skrivs alltid. Ingen fil hoppas över.
3. Befintlig mapp skrivs aldrig över. Suffix `-2`, `-3`.
4. Frontmatter finns **bara** i `va.md`.
5. `<datum>` = dagens datum, `YYYY-MM-DD`.
6. Status i `projekt.md` blir alltid `Fas 0 — inte påbörjad` vid skapandet.
   VÅ ändrar till `Fas 1` när arbetet börjar.

---

**Slut på projektmallen.**

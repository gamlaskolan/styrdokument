# PROJEKTMALL — de fem filerna

**Dokumenttyp:** Styrdokument. Mall.
**Status:** Låst. Ändras bara vid beslut av VÅ.
**Gäller:** Alla projekt under `projekt/`.

Denna fil är kontraktet för vad ett nytt projekt är. Fliken "Nytt projekt" i
plapp bygger mot den. En ny chatt läser mappen — inget mer behövs.

---

## DEL 1 — MAPPEN

**Mappnamn:** `projekt/{{SLUG}}-<NNN>/`

- `{{SLUG}}` = projektets namn: gemener, `å ä ö` → `a a o`, mellanslag och skiljetecken → `-`
- `<NNN>` = tresiffrigt nummer. Namn utan nummer får `-001`. Är numret upptaget ger appen nästa lediga i samma serie.
- Datumet står inte i mappnamnet sedan 2026-10-09.
- Exempel: `projekt/miniraknare-001/`

**Dubblett:** om mappen redan finns läggs suffix till: `-2`, `-3`, och så vidare.
Appen skriver aldrig över en befintlig mapp.

**Undermappar** skapas vid behov, inte i förväg: `produktion/`, `bilder/`, `data/`, `dokument/`.

---

## DEL 2 — FÄLTEN I FLIKEN "NYTT PROJEKT"

Platshållare har formen {{NAMN}}. Koden ersätter dem med fältets värde.

Fälten nedan är filernas platshållare — tio stycken, i denna ordning. Vilka av
dem appen samlar, och med vilka rubriker, står i `plapp.md` DEL 7. Detta
dokument äger filinnehållet.

| # | Fält | Typ | Hamnar i |
|---|---|---|---|
| 1 | Namn | en rad | `projekt.md` rubrik + `{{SLUG}}.md` rubrik |
| 2 | Mål | en rad | `projekt.md` → `**Mål:**` |
| 3 | Syfte | en rad | `projekt.md` → `**Syfte:**` |
| 4 | Systemets mål (DEL 1) | flerradig | `{{SLUG}}.md` → DEL 1 |
| 5 | Kärnbegrepp (DEL 3) | flerradig | `{{SLUG}}.md` → DEL 3 |
| 6 | Invarianter (DEL 5) | flerradig | `{{SLUG}}.md` → DEL 5 |
| 7 | Datamodell (DEL 6) | flerradig | `{{SLUG}}.md` → DEL 6 |
| 8 | Saker som ska göras | flerradig → checklista | `pp.md` → checklista |
| 9 | Öppna frågor | flerradig | `ds.md` Öppna frågor och `pp.md` Öppna frågor. Samma text. |
| 10 | Första anteckningar | flerradig | `va.md` |

**Regler:**
- Alla tio fält kan lämnas tomma. Ett tomt fält ger en tom platshållare i filen —
  aldrig borttagen rubrik.
- Fält 2 och 3 är enradiga och korta. Långa beskrivningar hör i DEL 1
  (`{{SLUG}}.md`).
- Fält 8: en rad per sak. Raderna numreras `1`, `2`, `3` i den ordning VÅ skrev dem.
- **Färg** väljs i paletten vid Spara — 20 färger, obligatorisk. Färgen hamnar i
  `projekt.md` → `**Färg:**`, och följer projektets knapp och projektets rad.

**Platshållare som koden räknar fram:**

- `{{NASTA}}` — första raden i Saker som ska göras. Om tomt: "Fyll i Mål och Syfte".
- `{{FAS1}}` — första raden i Saker som ska göras. Om tomt: "Ej namngiven".
- `{{N}}` — radnummer i fält 8. 1, 2, 3 ...
- `{{SAK}}` — radens text i fält 8.

Värdena räknas fram av koden. Mallen beskriver dem.


---

## DEL 3 — FIL 1: `projekt.md`

```markdown
# {{NAMN}}

**Mål:** {{MAL}}
**Syfte:** {{SYFTE}}
**Färg:** {{FARG}}

**Läget**
**Status:** Fas 0 — inte påbörjad.
**Nästa:** {{NASTA}}

**Filer**
- Startpunkt: start_har.md
- Arkitektur: {{SLUG}}.md
- Arbetsgång: pp.md
- Lokalt läge: ds.md
- VÅ:s anteckningar: va.md

**AI-läsning**
En extern AI som får denna mapp börjar med `projekt.md` och följer sedan
filordningen i repots `start_har.md`. Appen behövs inte — allt VÅ skriver
står i Markdown, och invarianterna i `{{SLUG}}.md` är garantin för det.
Bilder i mappen är inte data.

**Skapat:** {{DATUM}}
**Uppdaterat:** {{DATUM}}
```

---

## DEL 4 — FIL 2: `{{SLUG}}.md`

Nio delar. DEL 0, 2, 4, 9 ärvs ordagrant från `plapp.md` (med projektets
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
bygga det. Stegen bor i `pp.md`. Läget bor i `projekt.md`. Rollkontraktet bor i
`styrdokument/rollkontrakt.md`.

Om detta dokument och `pp.md` säger olika om arkitekturen — detta dokument vinner.
Om detta dokument och verkligheten säger olika — verkligheten vinner, och detta
dokument uppdateras.

---

## DEL 1 — SYSTEMETS MÅL

{{SYSTEMETS_MAL}}

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

projekt/{{SLUG}}-001/
├── projekt.md
├── {{SLUG}}-001.md
├── pp.md
├── ds.md
└── va.md

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

## DEL 5 — FIL 3: `pp.md`

```markdown
# Produktionsplan — {{NAMN}}

**Detta är arbetsgången.** Vad som gjorts, vad som görs, vad som väntar.
**Status och Nästa bor i `projekt.md`.** Här bor stegen.

> När en fas är klar: flytta stegen till `pp_fasN.md`. `pp.md` börjar om med nästa fas.

---

## Status

| Fas | Status |
|---|---|
| Fas 1 — {{FAS1}} | 🔄 Pågår |
| Fas 2 | ⏳ Inte öppnad |

---

## Fas 1 — {{FAS1}}

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

---

## Öppna frågor

{{OPPNA_FRAGOR}}

---

**Slut på produktionsplanen.**
```

**Anmärkning:** tom `Saker som ska göras` → rubriken blir `Fas 1 — Ej namngiven`
och checklistan blir tom. Ingen rad hittas på.

---

## DEL 6 — FIL 4: `ds.md`

```markdown
# DS — lokalt läge för {{NAMN}}

**Rollkontraktet bor i `styrdokument/rollkontrakt.md`.** Läs det först.
**Denna fil är projektets läge.** Vad som är öppet, vad som väntar, vad DS ska
veta just nu.

---

## Läget

- **Fas 0.** Projektet skapat {{DATUM}}. Inte påbörjat.
- **Nästa:** {{NASTA}}

---

## Vad DS ska veta om detta projekt

- Fem filer: `projekt.md`, `{{SLUG}}.md`, `pp.md`, `ds.md`, `va.md`.
- **`projekt.md` äger Status och Nästa.** Inte `pp.md`, inte `ds.md`.
- **Markdown är sanningen.** Inget JSON-register.
- **Arkitekturen bor i `{{SLUG}}.md`.** Det som är låst.
- **Checklistan i `pp.md` äger steg-status.** Rubrikerna är beskrivning.

---

## Öppna frågor

{{OPPNA_FRAGOR}}

---

## Vad DS gör härnäst

1. Läser i den ordning repots `start_har.md` anger.
2. Svarar enligt svarsformen i `promptform.md`.
3. Väntar på VÅ:s svar innan arbete börjar.

---

**Uppdaterat:** {{DATUM}}
```

---

## DEL 7 — FIL 5: `va.md`

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

## DEL 8 — REGLER FÖR SKAPANDET

1. Klick Spara → mappen skapas → fem filer skrivs → klart. Projektet är igång.
2. Alla fem filer skrivs alltid. Ingen fil hoppas över.
3. Befintlig mapp skrivs aldrig över. Suffix `-2`, `-3`.
4. Frontmatter finns **bara** i `va.md`.
5. `{{DATUM}}` — dagens datum, `YYYY-MM-DD`.
6. `{{DATUM_KORT}}` — dagens datum, `YYYYMMDD`. Används i mappnamn och id.
7. Status i `projekt.md` blir alltid `Fas 0 — inte påbörjad` vid skapandet.
   VÅ ändrar till `Fas 1` när arbetet börjar.

---

**Slut på projektmallen.**

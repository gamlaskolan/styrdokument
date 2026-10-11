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

# PROJEKTMALL — de fyra filerna

**Dokumenttyp:** Styrdokument. Mall.
**Status:** Låst. Ändras bara vid beslut av VÅ.
**Gäller:** Alla projekt under `projekt/`.

Denna fil är kontraktet för vad ett nytt projekt är. Fliken "Nytt projekt" i
en app bygger mot den. Läsordningen i en ny chatt står i `AGENTS.md` → Start av en chatt.

**Filerna i sig ligger i `projekt/plapp/produktion/mallar/`** — en fil per fil:
`projektplan.md`, `arkitektur.md` (mallen; projektfilen heter `<slug>.md`),
`ai.md`, `va.md`. `skapa_projekt()` läser dem därifrån. Denna fil beskriver;
den innehåller inte. Filuppsättningen i ett färdigt projekt — fyra filer plus
arkiverade fasfiler — står i `AGENTS.md` → Projektets filer.

---

## DEL 1 — MAPPEN

**Mappnamn:** `projekt/{{SLUG}}/`

- `{{SLUG}}` = **hela mappnamnet, inklusive numret** — `miniraknare-001`. Koden bygger det av projektets namn: gemener, `å ä ö` → `a a o`, mellanslag och skiljetecken → `-`.
- Namn utan nummer får `-001` pålagt. Är numret upptaget ger appen nästa lediga i samma serie.
- Datumet står inte i mappnamnet sedan 2026-10-09.
- Exempel: `projekt/miniraknare-001/`
- **Skriv aldrig `{{SLUG}}-001`:** `{{SLUG}}` innehåller redan numret, och `{{SLUG}}-001` skulle ge `miniraknare-001-001`.

Appen skriver aldrig över en befintlig mapp.

**Mappstruktur:** `data/` och `produktion/` med `logik/` och `ui/` skapas när
projektet skapas. Två mappar skapas senare, av appen: `dokument/` när en fil
läggs in, och `anteckningar/` när den första momentanteckningen skrivs.

**Fyra filer skrivs alltid**, och ingen av dem får bli tom. Saknas någon kastar
`skapa_projekt()` ett fel och projektmappen blir aldrig liggande halvfärdig.

---

## DEL 2 — FÄLTEN

Platshållare har formen `{{NAMN}}`. Koden ersätter dem med fältets värde.
Vilka fält formuläret har, och i vilken ordning, äger koden: `falt_nytt` i
`projekt/plapp/produktion/ui/nytt_projekt.py` och `PROJEKTFALT` i `filer.py`.
Detta dokument äger var värdena hamnar.

**Formuläret samlar elva fält:**

| # | Fält | Typ | Hamnar i |
|---|---|---|---|
| 1 | Namn | en rad | `projektplan.md` rubrik + `<slug>.md` rubrik |
| 2 | Konkreta leverabler | flerradig | `projektplan.md` → `**Konkreta leverabler**` |
| 3 | Definition of Done (DoD) | flerradig | `projektplan.md` → `**Definition of Done (DoD)**` |
| 4 | Prioriteringsordning vid kravkrock | flerradig | `projektplan.md` → `**Prioriteringsordning vid kravkrock**` |
| 5 | Avgränsning | flerradig | `projektplan.md` → `**Avgränsning**` |
| 6 | Orsaker till regler och förbud | flerradig | `projektplan.md` → `**Orsaker till regler och förbud**` |
| 7 | Riktlinjer vid osäkerhet | flerradig | `projektplan.md` → `**Riktlinjer vid osäkerhet**` |
| 8 | En fil äger en sak | flerradig | `<slug>.md` → DEL 1B |
| 9 | Korta moduler och kontextgräns | flerradig | `<slug>.md` → DEL 1B |
| 10 | Single Source of Truth | flerradig | `<slug>.md` → DEL 1B |
| 11 | Körbar grind framför skriftliga påminnelser | flerradig | `<slug>.md` → DEL 1B |

Fält 2–11 visas och ändras sedan i projektsidans panel Projekt.

**Skrivs för hand — formuläret samlar dem inte:** Systemets mål (`<slug>.md`
DEL 1), Kärnbegrepp (DEL 3), Invarianter (DEL 5), Datamodell (DEL 6), Appens
utseende (DEL 7) och Arkitektoniska testfall (DEL 8). DEL 7 och 8 börjar tomma.
Platshållarna `{{SYSTEMETS_MAL}}`, `{{KARNBEGREPP}}`, `{{INVARIANTER}}` och
`{{DATAMODELL}}` står kvar i filen tills VÅ skriver dem.

**Regler:**

- Alla fält kan lämnas tomma. Ett tomt fält ger en tom rad under rubriken — aldrig borttagen rubrik.
- Fält 1 är en rad. Långa beskrivningar hör i fält 2–7 (`projektplan.md`) eller i DEL 1 (`<slug>.md`).
- **Färg** väljs i paletten vid Spara — 20 färger, obligatorisk. Färgen hamnar i `projektplan.md` → `**Färg:**`, och följer projektets knapp och projektets rad.
- `va.md` har frontmatter överst: `id`, `uppdaterad` och `typ` — se `projekt/plapp/produktion/mallar/va.md`.

**Platshållare som koden räknar fram:** `{{NASTA}}` (första raden i **Konkreta
leverabler**, annars "Ej angivet"; skrivs fältet senare på projektsidan byts
"Ej angivet" mot första raden), `{{DATUM}}` (`YYYY-MM-DD`), `{{DATUM_KORT}}`
(`YYYYMMDD`), `{{SLUG}}`, `{{FARG}}` och `{{TOMT}}`. `{{N}}` och `{{SAK}}`
fyller checklistan bara om värdet `Saker` skickas — formuläret gör det inte
sedan 2026-10-09, så checklistan i ett nytt projekt är tom.

**Platshållare som blir tomma:** `{{OPPNA_FRAGOR}}` i `projektplan.md` och
`{{ANTECKNINGAR}}` i `va.md`.

---

**Slut på projektmallen.**

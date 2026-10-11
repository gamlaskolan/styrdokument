# PROJEKTMALL — de fyra filerna

**Dokumenttyp:** Styrdokument. Mall.
**Status:** Låst. Ändras bara vid beslut av VÅ.
**Gäller:** Alla projekt under `projekt/`.

Denna fil är kontraktet för vad ett nytt projekt är. Fliken "Nytt projekt" i
plapp bygger mot den. En ny chatt läser mappen — inget mer behövs.

**Filerna i sig ligger i `styrdokument/mallfiler/`** — en fil per fil:
`projektplan.md`, `arkitektur.md`, `ai.md`, `va.md`. `skapa_projekt()` läser
dem därifrån. Denna fil beskriver; den innehåller inte.

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

**Mappstruktur:** `data/` och `produktion/` med `logik/` och `ui/` skapas när
projektet skapas — inte vid behov. Fler mappar finns inte.

**Fyra filer skrivs alltid**, och ingen av dem får bli tom. Saknas någon kastar
`skapa_projekt()` ett fel och projektmappen blir aldrig liggande halvfärdig.

---

## DEL 2 — FÄLTEN

Platshållare har formen `{{NAMN}}`. Koden ersätter dem med fältets värde.

Fälten nedan är filernas platshållare — fjorton stycken, i denna ordning. Vilka
av dem appen samlar, och med vilka rubriker, står i `plapp.md` DEL 7. Detta
dokument äger filinnehållet.

| # | Fält | Typ | Hamnar i |
|---|---|---|---|
| 1 | Namn | en rad | `projektplan.md` rubrik + `arkitektur.md` rubrik |
| 2 | Konkreta leverabler | flerradig | `projektplan.md` → `**Konkreta leverabler**` |
| 3 | Definition of Done (DoD) | flerradig | `projektplan.md` → `**Definition of Done (DoD)**` |
| 4 | Prioriteringsordning vid kravkrock | flerradig | `projektplan.md` → `**Prioriteringsordning vid kravkrock**` |
| 5 | Avgränsning | flerradig | `projektplan.md` → `**Avgränsning**` |
| 6 | Orsaker till regler och förbud | flerradig | `projektplan.md` → `**Orsaker till regler och förbud**` |
| 7 | Riktlinjer vid osäkerhet | flerradig | `projektplan.md` → `**Riktlinjer vid osäkerhet**` |
| 8 | Systemets mål (DEL 1) | flerradig | `arkitektur.md` → DEL 1 |
| 9 | Kärnbegrepp (DEL 3) | flerradig | `arkitektur.md` → DEL 3 |
| 10 | Invarianter (DEL 5) | flerradig | `arkitektur.md` → DEL 5 |
| 11 | Datamodell (DEL 6) | flerradig | `arkitektur.md` → DEL 6 |
| 12 | Saker som ska göras | flerradig → checklista | `projektplan.md` → checklista |
| 13 | Öppna frågor | flerradig | `projektplan.md` → Öppna frågor |
| 14 | Första anteckningar | flerradig | `va.md` |

**Regler:**

- Alla fjorton fält kan lämnas tomma. Ett tomt fält ger en tom platshållare i filen — aldrig borttagen rubrik.
- Fält 1 är en rad. Långa beskrivningar hör i fält 2–7 (`projektplan.md`) eller i DEL 1 (`arkitektur.md`).
- Fält 12: en rad per sak. Raderna numreras `1`, `2`, `3` i den ordning VÅ skrev dem.
- **Färg** väljs i paletten vid Spara — 20 färger, obligatorisk. Färgen hamnar i `projektplan.md` → `**Färg:**`, och följer projektets knapp och projektets rad.
- `va.md` har frontmatter överst: `id`, `uppdaterad` och `typ`.

**Platshållare som koden räknar fram:** `{{NASTA}}` (första raden i **Konkreta
leverabler**), `{{N}}` och `{{SAK}}` (raden i fält 12), samt `{{DATUM}}`
(`YYYY-MM-DD`), `{{DATUM_KORT}}` (`YYYYMMDD`), `{{SLUG}}` och `{{TOMT}}`.

**Platshållare som står kvar oskrivna:** `{{SYSTEMETS_MAL}}`, `{{KARNBEGREPP}}`,
`{{INVARIANTER}}` och `{{DATAMODELL}}` samlar appen inte in — VÅ skriver dem för
hand i `arkitektur.md`. `{{OPPNA_FRAGOR}}` finns **bara** i `projektplan.md`, och
`{{ANTECKNINGAR}}` i `va.md` sätts till en tom sträng.

---

**Slut på projektmallen.**

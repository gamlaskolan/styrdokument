> **Äger:** vad ett projekt består av: projektmappen, projektets filer och hur projektet skapas
> **Typ:** Referens
> **Hänvisas från:** styrdokument/strukturplan.md, styrdokument/PRO.md

# Projektmall

Gäller alla projekt under `projekt/`. Mallarna för projektets filer ligger i `styrdokument/mallar/`. Den här filen beskriver projektet men innehåller inga mallar. Repots delade struktur står i [strukturplan.md](strukturplan.md).

## Delat och per projekt

| Del av ramverket | Plats | Antal |
| --- | --- | --- |
| Startfil | `AGENTS.md` | en i repot |
| Regelfiler, begreppslista, projektmall | `styrdokument/`, ett eget repo som AI:n bara läser | en uppsättning i repot |
| Källdokument | `styrdokument/kallor/` | en uppsättning i repot |
| `testa.py` | `verktyg/testa.py` | en i repot, körs per projekt |
| Delad strukturplan | `styrdokument/strukturplan.md` | en i repot |
| Delat filregister | `filregister.md` i repots rot | en i repot |
| Statusfil | `projekt/<slug>/projektdokument/status.md` | en per projekt |
| Strukturplan | `projekt/<slug>/referens/strukturplan.md` | en per projekt |
| Filregister | `projekt/<slug>/referens/filregister.md` | en per projekt |
| Fasernas projektdokument och ADR | `projekt/<slug>/projektdokument/` | per projekt |

## Projektmappen

**Mappnamn:** `projekt/<slug>/`

- `<slug>` är hela mappnamnet inklusive nummer, till exempel `miniraknare-001`.
- Slug bildas av projektets namn: gemener, `å ä ö` → `a a o`, mellanslag och skiljetecken → `-`.
- Ett namn utan nummer får `-001`. Är numret upptaget används nästa lediga nummer i samma serie.
- `<slug>` innehåller redan numret. Skriv därför aldrig `<slug>-001`, eftersom det skulle ge till exempel `miniraknare-001-001`.
- En befintlig projektmapp skrivs aldrig över.

**Mappar i projektet:**

| Mapp | Innehåll | Skapas |
| --- | --- | --- |
| `projektdokument/` | statusfilen, fasernas leverabler och anpassningsplanen | när projektet skapas |
| `projektdokument/adr/` | ett arkitekturbeslut per fil, `ADR-NNN-<namn>.md` | vid första ADR:en |
| `referens/` | strukturplan, filregister och projektets övriga referensfiler | när projektet skapas |
| `handledning/`, `instruktion/`, `forklaring/` | projektets dokumentation per Diátaxis-typ | vid första filen av typen |
| `produktion/` | kod och tester, med en mapp per lager enligt projektets strukturplan | i fas 0; lagren fastställs i fas 4 |
| `data/` | projektets data | när projektet skapas |

**Valfritt underlag**, som AI:n bara läser när utvecklaren hänvisar dit:

| Plats | Innehåll |
| --- | --- |
| `va.md` | utvecklarens fria anteckningar (typ Projektdokument) |
| `dokument/` | inlagda filer, till exempel pdf:er |
| `anteckningar/` | anteckningar från arbetsmoment |

## Skapa ett projekt

Ett projekt skapas i fas 0 (Processdokumentet, Del 1, fas 0). Den som skapar projektet, AI:n eller ett verktyg, gör följande:

1. Bildar `<slug>` enligt reglerna ovan.
2. Skapar mapparna `projektdokument/`, `referens/`, `produktion/` och `data/`.
3. Skriver tre filer ur mallarna och ersätter platshållarna:

   | Mall | Projektfil |
   | --- | --- |
   | `mallar/status.md` | `projektdokument/status.md` |
   | `mallar/strukturplan.md` | `referens/strukturplan.md` |
   | `mallar/filregister.md` | `referens/filregister.md` |

4. Lägger till projektets sökväg under Projekt i `filregister.md` i repots rot.

Ingen av de tre filerna får vara tom. Misslyckas ett moment tas mappen bort, så att ingen halvfärdig projektmapp blir kvar. Därefter fortsätter fas 0 med aktiviteterna i processdokumentet: grindparametrar, `testa.py` och, i ett befintligt projekt, en nulägesinventering.

**Ett projekt utan `projektdokument/status.md` har inte passerat fas 0.** Ett tomt projekt räknas som ett nytt projekt. Ett projekt som redan har kod eller dokumentation räknas som ett befintligt projekt och får en nulägesinventering.

## Fasdokument

Fasernas projektdokument skapas ur sina mallar när fasen påbörjas. Gate-kriterierna står i processdokumentet, Del 1, och upprepas inte i mallarna.

| Fas | Projektfil | Mall |
| --- | --- | --- |
| 0, befintligt projekt | `projektdokument/anpassningsplan.md` | `mallar/anpassningsplan.md` |
| 1 | `projektdokument/vision.md` | `mallar/vision.md` |
| 2 | `projektdokument/krav.md` | `mallar/krav.md` |
| 3 | `projektdokument/icke_funktionella_krav.md` | `mallar/icke_funktionella_krav.md` |
| 4 | `projektdokument/arkitektur.md` och `projektdokument/adr/ADR-NNN-<namn>.md` | `mallar/arkitektur.md`, `mallar/adr/ADR-NNN.md` |
| 6 | `projektdokument/teststrategi.md` | `mallar/teststrategi.md` |
| 7 | `projektdokument/drift.md` | `mallar/drift.md` |

Fas 5 har inget eget projektdokument.

## Platshållare i mallarna

| Platshållare | Värde |
| --- | --- |
| `{{NAMN}}` | projektets namn, en rad |
| `{{SLUG}}` | projektmappens namn inklusive nummer |
| `{{DATUM}}` | dagens datum, `YYYY-MM-DD` |
| `{{NNN}}` | ADR:ens löpnummer, tre siffror |
| `{{TITEL}}` | ADR:ens rubrik |

Platshållare som saknar värde ersätts med "Ej angivet". Ingen rubrik tas bort.

## Sessionsstart

Se PRO-17: sessionen startar med raden `Läs AGENTS.md och följ den. Projekt: <slug>.` ([PRO.md](PRO.md)). `<slug>` i startfilens länkar är det projekt som startraden anger.

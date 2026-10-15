> **Äger:** vad ett projekt består av, hur det skapas och vilka filer det har
> **Typ:** Referens
> **Hänvisas från:** styrdokument/strukturplan.md

# Så ser ett projekt ut

En del av ramverket ligger i repots rot och gäller alla projekt. Resten ligger i projektets egen mapp.

| Del | Var |
| --- | --- |
| Startfil, regelfiler, ordlista, projektmall, repots strukturplan, repots filregister, kontrollen och källdokumenten | repots rot och `styrdokument/` |
| Statusfil, projektets strukturplan, projektets filregister, fasdokument och arkitekturbeslut | `projekt/<slug>/` |

## Mappnamnet

`<slug>` är hela mappnamnet, med nummer: små bokstäver, `å ä ö` blir `a a o`, mellanslag och skiljetecken blir `-`. Ett namn utan nummer får `-001`. Är numret taget används nästa lediga i samma serie. En mapp som redan finns skrivs aldrig över.

## Mapparna

| Mapp | Innehåll | Skapas |
| --- | --- | --- |
| `projektdokument/` | statusfilen, fasdokumenten och anpassningsplanen | när projektet skapas |
| `referens/` | strukturplan, filregister och andra referensfiler | när projektet skapas |
| `produktion/` | kod och tester, en mapp per lager enligt projektets strukturplan | i fas 0 |
| `data/` | projektets data | när projektet skapas |

Mappen för arkitekturbeslut skapas när det första beslutet skrivs. Mappar för dokumentation (`handledning/`, `instruktion/`, `forklaring/`) skapas när den första filen av den sorten skrivs.

Underlag som bara läses när VÅ hänvisar dit: `va.md`, `dokument/` och `anteckningar/`.

## Så skapas projektet

1. Bilda `<slug>`.
2. Skapa mapparna.
3. Skriv `projektdokument/status.md`, `referens/strukturplan.md` och `referens/filregister.md` ur mallarna. Fyll i projektets namn, slug och datum.
4. Fyll i projektets strukturplan: mapplistan och de kontroller projektet använder (se mallen).
5. Skriv in projektets rad i repots filregister.
6. Lägg en tom platshållare i `produktion/` så att mappen versionshanteras.

Ingen av de tre första filerna får vara tom. Går ett moment fel tas mappen bort igen. Ett projekt utan `projektdokument/status.md` har inte passerat fas 0.

## Fasdokumenten

De skapas ur sin mall när fasen börjar:

| Fas | Fil |
| --- | --- |
| 1 | `vision.md` |
| 2 | `krav.md` |
| 3 | `icke_funktionella_krav.md` |
| 4 | `arkitektur.md` och `adr/ADR-NNN-<namn>.md` |
| 5 | inget eget dokument |
| 6 | `teststrategi.md` |
| 7 | `drift.md` |

Kriterierna för varje fas står i processdokumentet och upprepas inte i mallarna.

## Meta-fällan

Ett verktyg får inte hantera sig självt vid sidan om. Allt som hör till
verktyget — dess kod, moduler, data och konfiguration — ska lösas **på samma
sätt som allt annat i projektet**. Ingen egen filväg, ingen egen rutt, ingen
parallell lagringsplats, och aldrig en andra sanning.

**Skälet:** det som ligger vid sidan om granskas inte, och det som inte
granskas glider ifrån. Ett verktyg med en bakväg in i sig själv har två
sanningar om sig själv — och då vet ingen vilken som gäller.

**Så prövas regeln:** för varje fil, väg och rutt som bara verktyget använder —
fråga om den skulle finnas där om det gällde ett annat projekt. Svaret ska vara
ja. Verktygets eget projekt är ett projekt som alla andra, märkt i listan och
lika granskat som resten.

## Beroenden och bygge

Ett projekt med beroenden utanför standardbiblioteket har en **låst beroendefil** i `produktion/`, spårad i git. En klon ska gå att sätta upp utan att någon behöver minnas vilka paket som behövdes.

Det som måste byggas — en frontend, en paketering — har ett **byggkommando** i projektets strukturplan under rubriken `## Bygge`. Projektets CI-jobb kör det före testerna, så att ett trasigt bygge upptäcks i tid.

## Platshållare

`{{NAMN}}` projektets namn, `{{SLUG}}` mappnamnet, `{{DATUM}}` dagens datum, `{{NNN}}` arkitekturbeslutets nummer, `{{TITEL}}` dess rubrik. Saknar en platshållare värde skrivs "Ej angivet", och ingen rubrik tas bort.

> **Äger:** reglerna för dokumentations- och instruktionsfiler (område DOK)
> **Typ:** Referens
> **Hänvisas från:** AGENTS.md

# DOK – dokumentation

Varje uppgift ägs av en enda fil, och varje dokumentationsfil har ett ägarblock och en Diátaxis-typ. Instruktionsfilerna är korta och entydiga. Kontrollen anger en grind i `verktyg/testa.py` eller omdöme. Källan anger avsnittet i källdokumenten i `styrdokument/kallor/`.

## Regler med körbar kontroll

| ID | Regel | Motivering | Kontroll | Källa | Vid osäkerhet |
| --- | --- | --- | --- | --- | --- |
| DOK-03 | MÅSTE: varje dokumentations- och instruktionsfil inleds med ett ägarblock som anger vad filen äger, vilken typ filen har (Handledning, Instruktion, Referens, Förklaring eller Projektdokument) och vilka filer som hänvisar hit. | Ägaren till en uppgift ska gå att hitta direkt. | testa.py: ansvar | System design, princip 7, regel 1 | Stoppa och fråga |
| DOK-04 | MÅSTE: en regel formuleras på ett enda ställe, och övriga filer länkar dit. | Kopior glider isär och ger två olika svar. | testa.py: dubbletter | System design, princip 7, regel 2 | Stoppa och fråga |
| DOK-06 | MÅSTE: filregistret förtecknar sökvägen till varje versionshanterad fil, inget mer, och uppdateras i samma ändring som en fil skapas, flyttas eller tas bort. Filens ansvar och typ står i filens huvud och upprepas inte i registret. | Registret ska alltid stämma med repot. | testa.py: struktur | System design, princip 7, regel 4 | Stoppa och fråga |
| DOK-07 | MÅSTE: startfilen innehåller endast läsordning och länkar till statusfilen, filregistret, begreppslistan, regelfilerna per område och processdokumentet. Startfilen innehåller inga regler och inga beteendekrav. | Startfilen ska vara en karta, inte en regelsamling. | testa.py: struktur | System design, princip 8, regel 1 | Stoppa och fråga |
| DOK-08 | MÅSTE: varje regelfil täcker ett område (arkitektur, process eller dokumentation) och hålls så kort att den läses i sin helhet. En storlek över varningsnivån utlöser granskning. | En regelfil som inte läses i sin helhet följs inte. | testa.py: struktur | System design, princip 8, regel 2 | Stoppa och fråga |
| DOK-09 | MÅSTE: nivåorden MÅSTE, FÅR INTE och BÖR används konsekvent och endast med den betydelsen. | Entydiga nivåord gör varje regel kontrollerbar. | testa.py: regelregister | System design, princip 8, regel 3 | Stoppa och fråga |
| DOK-10 | MÅSTE: omdömesregler (kontroll: omdöme) listas i en egen sektion i varje regelfil och granskas vid varje fasbyte. | Regler utan körbar kontroll behöver en återkommande granskning. | testa.py: regelregister | System design, princip 8, regel 6 | Stoppa och fråga |

## Omdömesregler

| ID | Regel | Motivering | Kontroll | Källa | Vid osäkerhet |
| --- | --- | --- | --- | --- | --- |
| DOK-01 | MÅSTE: en instruktionsfil har en kort sammanfattning överst och detaljerna under. | Läsaren ska sällan behöva mer än toppen. | omdöme | System design, princip 2, regel 4 | Stoppa och fråga |
| DOK-02 | MÅSTE: varje dokumentationsfil har ett ansvar, på samma sätt som varje `.py`-fil. | En fil med flera ansvar ändras av flera orelaterade skäl. | omdöme | System design, princip 3, regel 4 | Stoppa och fråga |
| DOK-05 | MÅSTE: referensfiler innehåller fakta utan resonemang, och bakgrund och resonemang ligger i förklaringsfiler. Motiveringen på en mening i en regelfil räknas som en del av regeln. | Läsaren som slår upp fakta ska inte behöva läsa resonemang. | omdöme | System design, princip 7, regel 3 | Stoppa och fråga |
| DOK-11 | MÅSTE: varje FÅR INTE-regel kompletteras med det tillåtna alternativet. | Ett förbud utan alternativ lämnar det tillåtna öppet för tolkning. | omdöme | System design, princip 10, Negationer | Stoppa och fråga |

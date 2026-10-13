> **Äger:** reglerna för kod, lager och grindar (område ARK)
> **Typ:** Referens
> **Hänvisas från:** AGENTS.md

# ARK – arkitektur

Varje fil och modul har ett ansvar, och beroenden pekar endast inåt mot domänen. Databaser, ramverk och UI ligger ytterst bakom gränssnitt. Kontrollen anger en grind i `verktyg/testa.py` eller omdöme. Källan anger avsnittet i källdokumenten i `styrdokument/kallor/`.

## Regler med körbar kontroll

| ID | Regel | Motivering | Kontroll | Källa | Vid osäkerhet |
| --- | --- | --- | --- | --- | --- |
| ARK-04 | MÅSTE: ansvaret står i filens huvud, som en docstring i `.py`-filer och ett ägarblock överst i dokumentations- och instruktionsfiler. | Ansvaret ska gå att läsa utan att resten av filen läses. | testa.py: ansvar | System design, princip 1, regel 4 | Stoppa och fråga |
| ARK-05 | MÅSTE: storleksgränser används endast som varningsnivå som utlöser granskning av ansvaret. | Radantal är en signal, inte ett skäl att dela en fil. | testa.py: struktur | System design, princip 1, regel 5 | Stoppa och fråga |
| ARK-07 | FÅR INTE: interna hjälpfunktioner, datastrukturer och mellanresultat exponeras. I Python markeras de med inledande understreck och lämnas utanför `__all__`. | Ett litet gränssnitt håller ändringar inne i modulen. | testa.py: publika_granssnitt | System design, princip 2, regel 2 | Stoppa och fråga |
| ARK-09 | MÅSTE: varje modul tillhör exakt ett lager, och lagret framgår av mappen. | Lagret ska gå att avgöra utan att koden läses. | testa.py: struktur | System design, princip 3, regel 1 | Stoppa och fråga |
| ARK-10 | MÅSTE: moduler kommunicerar via gränssnitt, aldrig via varandras interna data. | Interna data som delas binder ihop modulerna. | testa.py: publika_granssnitt | System design, princip 3, regel 2 | Stoppa och fråga |
| ARK-12 | MÅSTE: varje modul går att enhetstesta utan databas, filsystem, nätverk eller UI. | Isolerade tester avslöjar dolda beroenden. | testa.py: enhetstester | System design, princip 3, regel 5 | Stoppa och fråga |
| ARK-13 | MÅSTE: varje lager har en egen mapp, och importer följer lagerordningen inåt. | Håller domänen oberoende av ramverk. | testa.py: import_riktning | System design, princip 4, regel 1 | Stoppa och fråga |
| ARK-15 | FÅR INTE: domänen och användningsfallen importerar externa bibliotek för lagring, webb eller UI. Sådant nås via gränssnitt i det inre lagret enligt ARK-17. | De inre lagren ska fungera utan teknisk plattform. | testa.py: rena_inre_lager | System design, princip 4, regel 3 | Stoppa och fråga |
| ARK-17 | MÅSTE: gränssnitt (ports) ligger i det inre lager som behöver dem, aldrig i det yttre. | Källkodsberoendet pekar då inåt även när anropet går utåt. | testa.py: import_riktning | System design, princip 5, regel 1 | Stoppa och fråga |
| ARK-18 | MÅSTE: implementationer (adapters) ligger i det yttre lagret. | Tekniken ska gå att byta utan att de inre lagren ändras. | testa.py: import_riktning | System design, princip 5, regel 2 | Stoppa och fråga |
| ARK-19 | MÅSTE: gränssnitt och implementation kopplas ihop på ett enda ställe, kompositionsroten (till exempel `main.py`). | Ett enda kopplingsställe gör beroendena synliga och utbytbara. | testa.py: import_riktning | System design, princip 5, regel 3 | Stoppa och fråga |
| ARK-20 | MÅSTE: tester av användningsfall använder enkla fejkimplementationer av gränssnitten i stället för en riktig databas. | Logiken ska kunna bevisas utan databas. | testa.py: enhetstester | System design, princip 5, regel 4 | Stoppa och fråga |
| ARK-23 | FÅR INTE: databasbegrepp (tabeller, SQL, ORM-modeller) eller UI-begrepp (widgets, HTML, events) förekommer i domänen eller användningsfallen. De hör hemma i adapter- och ramverkslagret. | Domänlogiken ska inte kopplas ihop med en teknisk plattform. | testa.py: rena_inre_lager | System design, princip 6, regel 3 | Stoppa och fråga |
| ARK-25 | MÅSTE: varje ny regel med kontrollen testa.py får sin kontroll i `testa.py` innan regeln räknas som gällande. Omdömesregler gäller utan körbar kontroll men granskas vid varje fasbyte. | En regel som bara står skriven bryts förr eller senare. | testa.py: regelregister | System design, princip 9, regel 2 | Stoppa och fråga |

## Omdömesregler

| ID | Regel | Motivering | Kontroll | Källa | Vid osäkerhet |
| --- | --- | --- | --- | --- | --- |
| ARK-01 | MÅSTE: varje fil har ett ansvar som går att beskriva i en mening utan ordet "och". | En fil med ett ansvar har en enda anledning att ändras. | omdöme | System design, princip 1, regel 1 | Stoppa och fråga |
| ARK-02 | MÅSTE: en fil delas när den har fått fler än ett ansvar, inte när den har blivit lång. | Att dela efter storlek klyver sammanhängande logik. | omdöme | System design, princip 1, regel 2 | Stoppa och fråga |
| ARK-03 | MÅSTE: två filer slås ihop när ansvaret i praktiken är detsamma och filerna alltid ändras samtidigt. | Filer som alltid ändras tillsammans är i praktiken en enhet. | omdöme | System design, princip 1, regel 3 | Stoppa och fråga |
| ARK-06 | MÅSTE: gränssnittet utformas efter vad anroparen behöver, inte efter hur modulen är byggd inuti. | Anroparen ska bara behöva känna till gränssnittet. | omdöme | System design, princip 2, regel 1 | Stoppa och fråga |
| ARK-08 | MÅSTE: moduler som bara skickar vidare anrop till en annan modul (pass-through) slås ihop eller tas bort. | En grund modul tillför komplexitet utan att dölja något. | omdöme | System design, princip 2, regel 3 | Stoppa och fråga |
| ARK-11 | FÅR INTE: moduler delar tillstånd. Data skickas uttryckligen som argument eller returvärden. | Delat tillstånd ger dolda kopplingar mellan moduler. | omdöme | System design, princip 3, regel 3 | Stoppa och fråga |
| ARK-14 | MÅSTE: data som korsar en gräns inåt är enkla datastrukturer, aldrig databasrader eller ramverksobjekt. | De inre lagren ska inte känna till yttre teknik. | omdöme | System design, princip 4, regel 2 | Stoppa och fråga |
| ARK-16 | MÅSTE: ett behov av att peka utåt löses med beroendeinversion enligt ARK-17–ARK-19. | Beroenderegeln gäller även när anropet går utåt. | omdöme | System design, princip 4, regel 4 | Stoppa och fråga |
| ARK-21 | MÅSTE: domän och användningsfall byggs och testas först, med enkla minnesbaserade implementationer av lagringsgränssnitten. | Logiken ska fungera innan tekniken väljs. | omdöme | System design, princip 6, regel 1 | Stoppa och fråga |
| ARK-22 | MÅSTE: val av databas och ramverk dokumenteras som en ADR med motivering mot kraven, först när ett verkligt behov kräver valet. | Sena beslut fattas när kunskapen om behoven är som störst. | omdöme | System design, princip 6, regel 2 | Stoppa och fråga |
| ARK-24 | MÅSTE: ett byte av databas eller UI kräver endast ändringar i adapter- och ramverkslagret. | Tekniken är en utbytbar detalj i det yttersta lagret. | omdöme | System design, princip 6, regel 4 | Stoppa och fråga |
| ARK-26 | MÅSTE: utskriften från `testa.py` anger för varje fynd nivå, grind, fil, rad, regel-ID och åtgärd, och för en varning från baslinjen även avvikelsens ID. Formatet är `<fel\|varning> <grind> <fil>:<rad> <regel-ID> <åtgärd>`, följt av en rad per grind: `<pass\|fail> <grind> (<antal fel> fel, <antal varningar> varningar)`. | Ett fynd ska gå att rätta utan att leta. | omdöme | System design, princip 9, regel 3 | Stoppa och fråga |
| ARK-27 | MÅSTE: `testa.py` följer själv systemets principer, och varje kontroll är en egen funktion med ett ansvar. | Grindarna ska hålla samma kvalitet som koden de kontrollerar. | omdöme | System design, princip 9, regel 5 | Stoppa och fråga |

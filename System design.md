# System design

2026-10-13 · Victor

## Översikt

Systemdesignen bestämmer hur kod och instruktionsfiler delas upp, var gränserna går och hur reglerna kontrolleras. Grunden är **ansvar och gränser, inte radantal**: en fils storlek säger lite om filens kvalitet, medan antalet ansvarsområden säger nästan allt.

Dokumentet gäller lika för källkod (`.py` och andra språk) som för instruktions- och dokumentationsfiler. Båda typerna är delar av systemet och följer samma principer.

Principerna bygger på varandra i tre lager:

- **Formen på delarna (princip 1–3):** varje modul har ett ansvar, ett enkelt gränssnitt och få beroenden.
- **Riktningen mellan delarna (princip 4–6):** beroenden pekar inåt mot domänen; databaser, ramverk och UI ligger ytterst som utbytbara detaljer.
- **Hur reglerna hålls (princip 7–10):** en fil äger en sak, instruktioner till AI:n är entydiga, och reglerna kontrolleras av körbara grindar i stället för skriftliga påminnelser.

Varje princip beskrivs med samma struktur: huvudfråga, princip, regler, körbar grind och avvägningar. Reglerna i dokumentet får ID när reglerna förs in i regelfiler i fas 0 (princip 8); dessförinnan hänvisas till en regel som "System design, princip X regel Y".

**Samspel med processdokumentet:** Processdokumentet styr *när* – faser, gates och arbetsflöde. System design styr *hur* kod och filer formas – lager, regler och körbara grindar. Vid motsägelse gäller processdokumentet för faser och arbetsflöde och System design för struktur och regler; motsägelsen flaggas och rättas i ägardokumentet. Efter fas 0 är regelfilerna den operativa källan till regler och processdokumentet den operativa källan till processbeskrivningen; när AI:n läser källdokumenten anger läsfallen i processdokumentets översikt (System design, princip 7, regel 5).

## Begrepp

Begreppen nedan används på exakt samma sätt i båda dokumenten. Listan ägs av System design och återges ordagrant i processdokumentet; ändringar görs i System design först och förs över till processdokumentet i samma ändring, med samma version. Versionen är datumet för den senaste ändringen av listan. Filnamn och mappar bestäms när ramverket byggs; begreppen anger roller, inte namn. Två undantag är fasta så att AI:n alltid hittar in: startfilens namn och regelfilernas namn. Version 2026-10-13.

**Process**

- **Fas:** en av delarna i processen: förberedelse (fas 0) följd av sju faser, från vision (fas 1) till drift (fas 7). Varje fas avslutas med en fasgate.
- **Fasgate (gate):** ett beslut, godkänt av utvecklaren, att en fas är klar. Kriterierna står under "Gate – klart när" i processdokumentet.
- **Körbar grind:** en automatisk kontroll i `testa.py` som ger `pass` eller `fail`. Varje fynd från en grind är antingen ett fel eller en varning. Grinden ger `fail` om minst ett fynd är ett fel och annars `pass`; varningar ändrar aldrig resultatet. Både fasgate och körbar grind krävs för att gå vidare.
- **Varning:** ett fynd som redovisas men inte stoppar flödet. Ett fynd är en varning i exakt två fall: när en fil överskrider en varningsnivå i strukturplanen (System design, princip 1) och när fyndet matchar en post i baslinjen. Alla andra fynd är fel. Öppna varningar förs in i statusfilen och granskas vid fasbyte (System design, princip 9, regel 4).
- **Baslinje:** förteckningen i strukturplanen över kända avvikelser i ett befintligt projekt, en post per avvikelse i anpassningsplanen. Ett fynd som matchar en baslinjepost blir en varning i stället för ett fel. Posten tas bort i samma ändring som avvikelsen åtgärdas, och därefter blir samma fynd ett fel igen. Baslinjen skapas i fas 0 och får därefter bara krympa.
- **Steg (nivå):** ett av de åtta stegen i frågetrappan i fas 1. I spelpedagogiken kallas ett steg även nivå.
- **Ändring:** den minsta arbetsenheten i AI-samarbetet. En ändring följer de åtta stegen i arbetsflödet per ändring (processdokumentet, Del 2). I fas 0, innan regelfilerna och `testa.py` finns, gäller undantagen i processdokumentet, Del 1, fas 0, Undantag i fas 0.
- **Leverabel:** resultatet av en fas. Fas 0 ger ramverket och, i ett befintligt projekt, en anpassningsplan; fas 1–4 och 6–7 ger varsitt projektdokument; fas 5–7 ger dessutom kod, tester eller pipeline. Fasernas projektdokument och arkitekturbesluten (ADR) är undantagna Diátaxis-indelningen (System design, princip 7).
- **Princip:** en numrerad grundsats. System design har princip 1–10; processdokumentet har princip 1–7 för AI-samarbete i Del 2. En hänvisning anger alltid dokument eller del. Etablerade designprinciper som SoC, SRP och låg koppling behåller sina namn.

**Krav och regler**

- **Krav:** vad appen ska göra (funktionellt krav, fas 2) eller hur väl appen ska fungera (icke-funktionellt krav, fas 3).
- **MVP:** den minsta version av appen som ger värde; består av samtliga Must-krav.
- **Regel:** en bindande instruktion för kod, filer eller AI:n, med ID, nivåord (MÅSTE, FÅR INTE, BÖR), motivering, kontroll och källa (System design, princip 8). Vad som räknas som en regel anger System design, princip 8; övrigt innehåll i källdokumenten är förklaring eller processbeskrivning. En regel är aldrig ett krav på appen. Kontrollen är antingen testa.py: \<funktion> eller omdöme; en regel med kontrollen omdöme kallas omdömesregel och granskas vid varje fasbyte.
- **Processbeskrivning:** innehållet i processdokumentets Del 1 – fasernas syfte, aktiviteter, leverabler och gate-kriterier, inklusive metoden i fas 1. Processbeskrivningen förs inte över till regelfilerna; AI:n läser den i processdokumentet enligt läsfallen i processdokumentets översikt.
- **Regelfil:** en fil med regler för ett område. Det finns exakt tre regelfiler, `ARK.md`, `DOK.md` och `PRO.md`, i samma mapp. Varje regel står i exakt en regelfil, i det område som System design, princip 8, anger; andra filer återger regeln endast med markören "Se \<regel-ID>:" och länk (System design, princip 10). Startfilen och regelfilerna kallas tillsammans instruktionsfiler.
- **Startfil:** filen som AI:n läser först i varje session. Startfilen heter `AGENTS.md` och ligger i repots rot. Läser AI-verktyget automatiskt en annan fil (till exempel `CLAUDE.md`), innehåller den filen endast en länk till `AGENTS.md`. Startfilen innehåller endast en rubrik och en numrerad lista där varje punkt är exakt en länk, i läsordning: statusfilen, filregistret, begreppslistan, `ARK.md`, `DOK.md`, `PRO.md` och processdokumentet.
- **Källdokument:** de fullständiga dokumenten System design och processdokumentet; ett utdrag eller en ändringslista är aldrig ett källdokument. Källdokumenten förs in oförändrade i repot i fas 0, i en egen mapp som strukturplanen anger, och läses efter fas 0 enligt läsfallen i processdokumentets översikt. Källdokumenten saknar ägarblock och är undantagna Diátaxis-indelningen och dubblettkontrollen (System design, princip 7).
- **Versionshistorik:** versionshanteringens historik (git log). Ingen separat fil förs; tidigare lägen av en fil läses ur historiken.
- **Ramverk:** startfilen, regelfilerna, begreppslistan, strukturplanen, filregistret, statusfilen, `testa.py` och källdokumenten, som skapas eller förs in i fas 0. Strukturplanen äger projektets mappstruktur, varningsnivåer, baslinje och grindarnas parametrar. Allt som `testa.py` läser ur strukturplanen står i avsnittet `## Grindparametrar`, i exakt ett kodblock märkt `toml` enligt System design, princip 9; övrig text i strukturplanen läses inte av `testa.py`. Filregistret förtecknar sökvägen till varje versionshanterad fil, inget mer; versionshanterad är varje fil som versionshanteringen spårar, och filens ansvar och typ står i filens huvud. Statusfilen beskriver alltid nuläget och har sex fasta delar, som alltid finns med och aldrig lämnas tomma: aktuell fas och senaste godkända gate; pågående ändring och dess steg i arbetsflödet per ändring, eller "Ingen"; sammanfattning av senaste ändringen; nästa ändrings mål i en mening, eller "Ej planerat"; öppna varningar från `testa.py`, eller "Inga"; samt nivåkartan och öppna följdfrågor, utanför fas 1 "Ej aktuellt". Aktuell fas har alltid ett av tre lägen: "pågår", "väntar på gate" eller "avslutad utan gate". Hur statusfilen sätts vid gate, ny release och ärligt avslut står i processdokumentet, Del 2, princip 2; tidigare lägen finns i versionshistoriken.
- **ADR (arkitekturbeslut):** ett dokumenterat beslut med sammanhang, alternativ och konsekvenser, ett beslut per fil.

**Struktur**

- **Ansvar (SRP):** det enda problem en enhet löser. En enhet har ett ansvar och en enda anledning att ändras.
- **Äga, ägare (SSOT, Single Source of Truth):** att vara den enda källan till en uppgift. Gäller både data i systemet (en modul äger en typ av data) och uppgifter i dokumentationen (en fil äger en regel). Övriga läser från eller hänvisar till ägaren, aldrig till en kopia.
- **Enhet:** en funktion, klass, modul eller fil.
- **Modul:** en `.py`-fil eller ett paket med ett ansvar och ett definierat gränssnitt. Ordet komponent används inte.
- **Gränssnitt:** de publika anrop en modul erbjuder andra moduler. Ordet används aldrig om användargränssnittet.
- **UI:** användargränssnittet – det användaren ser och interagerar med.
- **Lager:** domän, användningsfall, adaptrar och ramverk (System design, princip 4). Användningsfall avser alltid lagret; flödena i fas 2 heter användarflöden.

**Roller**

- **Utvecklaren:** personen som leder projektet och äger besluten: godkänner planer, steg och fasgates.
- **Användaren:** den som använder appen. I eget bruk samma person som utvecklaren, men i en annan roll.
- **AI:n:** AI-assistenten som aktivt leder samtalet och arbetsprocessen och utför arbetet enligt reglerna; besluten fattas av utvecklaren.

## 1. Ansvar framför radantal

**Huvudfråga:** Vad avgör hur en fil eller modul delas upp?

**Princip:** Uppdelning styrs av ansvar, inte av storlek. En gräns på antal rader leder till två typiska fel: en sammanhängande modul klyvs mitt i logiken för att hålla gränsen, eller flera orelaterade ansvar samsas i en fil som råkar vara kort. Radantal är en *signal* att granska, aldrig en *regel* att följa.

**Regler**

1. Varje fil har ett ansvar som går att beskriva i en mening utan ordet "och".
2. En fil delas när filen fått fler än ett ansvar, inte när filen blivit lång.
3. Två filer slås ihop när ansvaret i praktiken är detsamma och filerna alltid ändras samtidigt.
4. Ansvaret står i filens huvud: en docstring i `.py`-filer, ett ägarblock överst i dokumentations- och instruktionsfiler.
5. Storleksgränser används endast som varningsnivå som utlöser granskning.

**Körbar grind:** `testa.py` kontrollerar att varje fil har en ansvarsbeskrivning i huvudet. Filer över varningsnivån listas som *varning*, inte som *fel*, och kräver en granskning av ansvaret.

**Avvägning:** En lång fil med ett tydligt ansvar är bättre än tre korta filer som måste läsas tillsammans för att förstås.

## 2. Djupa moduler (Deep Modules)

**Huvudfråga:** Hur hålls källkod och dokumentation hanterbar när systemet växer?

**Princip:** En djup modul har ett enkelt, avskalat yttre gränssnitt men döljer en betydande mängd logik bakom abstraktionen. Värdet av en modul = funktionaliteten som döljs, minus komplexiteten i gränssnittet. En *grund* modul har ett gränssnitt nästan lika komplicerat som innehållet och tillför därför lite.

**Djup modul**

- *Gränssnitt:* få, tydliga anrop.
- *Inre logik:* omfattande och dold.
- *Kunskap som krävs av anroparen:* endast gränssnittet.
- *Effekt vid ändring:* ändringar stannar inne i modulen.

**Grund modul**

- *Gränssnitt:* många anrop, ofta tunna omslag.
- *Inre logik:* liten eller exponerad.
- *Kunskap som krävs av anroparen:* detaljer om det inre.
- *Effekt vid ändring:* ändringar sprids till anroparna.

**Regler**

1. Gränssnittet utformas utifrån vad anroparen behöver, inte utifrån hur modulen är byggd inuti.
2. Interna hjälpfunktioner, datastrukturer och mellanresultat exponeras inte; i Python markeras de med inledande understreck och lämnas utanför `__all__`.
3. Moduler som bara skickar vidare anrop till en annan modul (pass-through) slås ihop eller tas bort.
4. Samma princip gäller dokumentations- och instruktionsfiler: en instruktionsfil har en kort sammanfattning överst och detaljerna under, så att läsaren sällan behöver mer än toppen.

**Körbar grind:** `testa.py` kontrollerar att andra moduler endast importerar publika namn, och flaggar import av namn med inledande understreck över modulgränser.

**Avvägning:** Djupa moduler och principen om ett ansvar samverkar: en modul ska vara djup *inom* ett ansvarsområde, inte bred över flera.

## 3. Rena systemgränser: SoC, SRP och låg koppling

**Huvudfråga:** Hur hålls delarna isär så att en ändring på ett ställe inte sprider sig?

**Princip:** Tre etablerade designprinciper gäller tillsammans. Varje princip angriper samma problem från ett eget håll: SoC delar upp *problemen*, SRP avgränsar *ansvaret* per enhet, och låg koppling begränsar *beroendena* mellan enheterna.

**Separation of Concerns (SoC)**

- *Innebörd:* Olika delar löser helt åtskilda problem. UI hanterar aldrig lagring eller filstrukturer; datalagret känner inte till presentation.
- *Gäller för:* lager och moduler.
- *Tecken på brott:* UI-kod öppnar filer eller databaser; lagringskod formaterar text för visning.

**Single Responsibility Principle (SRP)**

- *Innebörd:* Varje enhet har ett ansvarsområde och en enda anledning att ändras.
- *Gäller för:* klasser, funktioner, `.py`-moduler och dokumentationsfiler.
- *Tecken på brott:* en fil ändras av flera orelaterade skäl; beskrivningen kräver "och".

**Loose Coupling (låg koppling)**

- *Innebörd:* Moduler har minimala direktberoenden av varandra. Enheter går att testa isolerat och byta ut utan spridningseffekter.
- *Gäller för:* relationer mellan moduler.
- *Tecken på brott:* ett test kräver att halva systemet startas; en ändring kräver ändringar i många filer.

**Regler**

1. Varje modul tillhör exakt ett lager, och lagret framgår av mappen.
2. Moduler kommunicerar via gränssnitt, aldrig via varandras interna data.
3. Delat tillstånd mellan moduler är förbjudet; data skickas uttryckligen som argument eller returvärden.
4. Varje dokumentationsfil har ett ansvar, på samma sätt som varje `.py`-fil.
5. Varje modul går att enhetstesta utan databas, filsystem, nätverk eller UI.

**Körbar grind:** `testa.py` bygger en importgraf och kontrollerar att inga importer korsar otillåtna lagergränser och att inga cirkulära beroenden finns. Enhetstesterna körs utan nätverk och filsystem, vilket avslöjar dolda beroenden.

**Avvägning:** Låg koppling har ett pris i form av fler gränssnitt. Gränssnitt införs där utbytbarhet eller testbarhet faktiskt behövs, inte runt varje funktion.

## 4. Beroenderegeln (The Dependency Rule)

**Huvudfråga:** Åt vilket håll får beroenden peka?

**Princip:** Systemet struktureras i koncentriska lager. Källkodsberoenden pekar endast inåt, mot högre nivåer av policy: domänen i kärnan. Ingenting i ett inre lager känner till innehållet i ett yttre lager – varken klasser, funktioner, variabler eller datastrukturer. Resultatet är hög testbarhet och kod som är oberoende av ramverk, databaser och UI.

Domänen i mitten är mest stabil och mest skyddad; ju längre ut, desto mer utbytbar är tekniken.

**Lagren inifrån och ut**

1. **Domän (Entities)** – kärnbegrepp och affärsregler, ren logik. *Får känna till:* ingenting utanför domänen.
2. **Användningsfall (Use Cases)** – applikationens flöden: vad systemet gör. *Får känna till:* domänen.
3. **Adaptrar (Interface Adapters)** – översättning mellan användningsfall och omvärld: controllers, presenters, repository-implementationer. *Får känna till:* användningsfall och domän.
4. **Ramverk och drivrutiner** – databas, webbramverk, UI, filsystem, externa tjänster. *Får känna till:* allt innanför.

**Regler**

1. Varje lager har en egen mapp, och importer följer lagerordningen inåt.
2. Data som korsar en gräns inåt är enkla datastrukturer, aldrig databasrader eller ramverksobjekt.
3. Domänen och användningsfallen importerar inga externa bibliotek för lagring, webb eller UI.
4. Ett behov att peka utåt löses med beroendeinversion (princip 5).

**Körbar grind:** `testa.py` läser alla importer och stoppar varje import som pekar från ett inre lager till ett yttre. Kontrollen ger hård `fail` – en regel som bara står skriven bryts förr eller senare.

**Avvägning:** Fyra lager är en utgångspunkt, inte ett krav. Ett mindre system kan slå ihop adaptrar och ramverk till ett yttre lager; riktningen inåt gäller oavsett antal lager.

## 5. Beroendeinversion (Dependency Inversion)

**Huvudfråga:** Hur når ett inre lager ut till databasen utan att bryta beroenderegeln?

**Princip:** Kontrollflödet i körtid går ibland från ett inre lager till ett yttre, till exempel när ett användningsfall sparar data. Då definierar det inre lagret ett gränssnitt (en abstraktion), och det yttre lagret implementerar gränssnittet. Källkodsberoendet pekar därmed fortfarande inåt, även när anropet går utåt.

**Exempel i Python**

```python
# usecases/ports.py  – inre lager äger gränssnittet
from typing import Protocol

class TaskRepository(Protocol):
    def save(self, task: Task) -> None: ...
    def get(self, task_id: str) -> Task | None: ...

# usecases/create_task.py  – känner bara till gränssnittet
def create_task(repo: TaskRepository, title: str) -> Task:
    task = Task.new(title)
    repo.save(task)
    return task

# adapters/sqlite_repository.py  – yttre lager implementerar
class SqliteTaskRepository:
    def save(self, task: Task) -> None: ...
    def get(self, task_id: str) -> Task | None: ...
```

**Regler**

1. Gränssnitt (ports) ligger i det inre lagret som behöver dem, aldrig i det yttre.
2. Implementationer (adapters) ligger i det yttre lagret.
3. Kopplingen mellan gränssnitt och implementation görs på ett enda ställe: kompositionsroten (till exempel `main.py`).
4. Tester av användningsfall använder enkla fejkimplementationer av gränssnitten i stället för riktig databas.

**Körbar grind:** Importkontrollen från princip 4 täcker även inversionen: en import från `usecases/` till `adapters/` ger `fail`. `testa.py` kontrollerar dessutom att kompositionsroten är den enda filen som importerar både gränssnitt och implementationer.

**Avvägning:** Ett gränssnitt med exakt en implementation och utan testbehov är onödig indirektion. Inversion används vid lagergränser, inte inom ett lager.

## 6. Databaser och UI är detaljer

**Huvudfråga:** När fattas beslut om databas, webbramverk och UI?

**Princip:** Så sent som möjligt. Databas, webbramverk och UI behandlas som utbytbara detaljer i det yttersta lagret. Domänlogiken kopplas därmed aldrig ihop med en teknisk plattform, och tekniska beslut kan fattas när kunskapen om behoven är som störst.

**Regler**

1. Domän och användningsfall byggs och testas först, med enkla minnesbaserade implementationer av lagringsgränssnitten.
2. Val av databas och ramverk dokumenteras som ett arkitekturbeslut (ADR) med motivering mot kraven, först när ett verkligt behov kräver valet.
3. Inga databasbegrepp (tabeller, SQL, ORM-modeller) eller UI-begrepp (widgets, HTML, events) förekommer i domänen eller användningsfallen.
4. Byte av databas eller UI ska endast kräva ändringar i adapter- och ramverkslagret.

**Körbar grind:** `testa.py` söker efter importer av databas-, webb- och UI-bibliotek i de inre lagren och ger `fail` vid träff. Hela testsviten för användningsfall körs mot minnesbaserade implementationer, vilket bevisar att logiken fungerar utan databas.

**Avvägning:** Att skjuta upp ett beslut betyder inte att undvika beslutet. När ett verkligt krav (prestanda, delning, synkronisering) gör valet nödvändigt fattas beslutet – men bakom ett gränssnitt.

## 7. En fil äger en sak och Diátaxis

**Huvudfråga:** Var finns sanningen om en viss sak, och hur förhindras motstridiga uppgifter?

**Princip:** Varje sakuppgift – en regel, ett krav, en sökväg, en konfiguration – ägs av exakt en fil (Single Source of Truth). Övriga filer *hänvisar* till ägaren i stället för att upprepa innehållet. Därmed glider information inte isär, dubbletter uppstår inte och systemet pekar aldrig mot två olika svar.

**Diátaxis-anpassning:** Dokumentationen delas upp efter läsarens behov i fyra typer. Varje dokumentationsfil tillhör exakt en typ, och typerna blandas inte i samma fil. Undantaget är projektdokumenten (se nedan).

- **Handledning (Tutorial)** – för att lära sig från början. Guidat förlopp med garanterat resultat.
- **Instruktion (How-to)** – för att lösa en bestämd uppgift. Numrerade moment mot ett mål.
- **Referens (Reference)** – för att slå upp exakta fakta. Regler, gränssnitt och struktur, utan resonemang.
- **Förklaring (Explanation)** – för att förstå varför. Bakgrund, motiv och avvägningar.

Varje typ har en egen mapp. Fasernas leverabler från processdokumentet, anpassningsplanen och statusfilen är projektdokument.

**Projektdokument är undantagna Diátaxis.** Fasernas leverabler och arkitekturbesluten (ADR) följer processdokumentets struktur och får blanda beslut, fakta och motiveringar. Ägarblocket anger typen projektdokument.

**Källdokumenten och startfilen är undantagna Diátaxis och ägarblock.** Källdokumenten förs in oförändrade och behåller sin egen struktur; startfilen innehåller endast läsordning och länkar (princip 8, regel 1). Källdokumenten är dessutom undantagna dubblettkontrollen, eftersom regelfilerna med avsikt återger källdokumentens regler.

**Regler**

1. Varje dokumentations- och instruktionsfil inleds med ett ägarblock: vad filen äger, vilken typ filen har (en Diátaxis-typ eller projektdokument) och vilka filer som hänvisar hit.
2. En regel formuleras på ett enda ställe; övriga filer länkar dit.
3. Referensfiler innehåller fakta utan resonemang; bakgrund och resonemang ligger i förklaringsfiler. Regelfiler är referensfiler, och motiveringen på en mening i regelformatet (princip 8) räknas som en del av regeln.
4. Filregistret förtecknar sökvägen till varje versionshanterad fil, inget mer, och uppdateras i samma ändring som en fil skapas, flyttas eller tas bort. Filens ansvar och typ står i filens huvud (princip 1, regel 4, och princip 7, regel 1) och upprepas inte i registret.
5. Efter fas 0 läser AI:n i varje session startfilen och därefter filerna i den ordning startfilen anger: statusfilen, filregistret, begreppslistan, regelfilerna och processdokumentet enligt läsfallen i processdokumentets översikt. Regler läses i regelfilerna, aldrig i källdokumenten; processbeskrivningen läses i processdokumentet. Källdokumenten ligger i repot, i den mapp strukturplanen anger. Varje regel anger sin källa i fältet Källa; vid en regeländring läser AI:n det avsnitt som källfältet pekar på och ändrar regelfilen och källdokumentet i samma ändring.

**Körbar grind:** `testa.py` kontrollerar att varje dokumentations- och instruktionsfil har ett ägarblock med giltig typ, att varje fil finns med i registret och att identiska regelformuleringar inte förekommer i flera filer. Källdokumentens mapp och startfilen undantas från kontrollen av ägarblock, och källdokumentens mapp undantas från dubblettkontrollen.

**Avvägning:** Hänvisningar kostar läsbarhet; en läsare som ständigt hoppar mellan filer tappar sammanhanget. Se DRY kontra ARID under princip 10.

## 8. Regelverk för AI-instruktioner

**Huvudfråga:** Hur utformas instruktionsfiler så att AI:n gör exakt det som sägs och varje moment i processen är synligt?

**Princip:** Instruktionsfiler är en del av systemets arkitektur och följer samma principer som koden: ett ansvar per fil, en ägare per regel och korta, entydiga formuleringar. Varje regel är antingen kontrollerbar av en körbar grind eller uttryckligen markerad som omdömesregel.

**Regelstruktur:** Varje regel skrivs i samma format, så att regeln går att läsa, följa och kontrollera:

| Del | Exempel |
| --- | --- |
| ID (unikt, stabilt) | `ARK-03` |
| Regel (nivåord först) | MÅSTE: importer pekar endast inåt |
| Motivering (en mening) | Håller domänen oberoende av ramverk |
| Kontroll (grind eller omdöme) | `testa.py: import_riktning` |
| Källa (regelns ursprung) | System design, princip 4, regel 1 |
| Vid osäkerhet | Stoppa och fråga |

**Giltiga kontroller:** `testa.py: <funktion>`, där funktionen är ett grindnamn i tabellen under princip 9, eller `omdöme`. **Regel-ID** består av område och ett tvåsiffrigt löpande nummer per område, till exempel `ARK-01`; ett ID återanvänds aldrig. **Område per regel:** området anges efter vad regeln styr och prövas i ordningen PRO, ARK, DOK: en regel som styr vad AI:n eller utvecklaren gör får PRO; annars får en regel som styr kod, lager eller grindar ARK; övriga regler får DOK. **Vad som är en regel:** varje numrerad punkt under Regler i princip 1–9 och under Gissningsförbud i princip 10, regeln under Negationer i princip 10, samt princip 1–7 för AI-samarbete i processdokumentet (Del 2). Övrig text i källdokumenten – principer, definitioner, tabeller, exempel och avvägningar – är förklaring och blir inte regler.

**Regler**

1. Startfilen innehåller endast läsordning och länkar: till statusfilen, till filregistret, till begreppslistan, till regelfilerna per område och till processdokumentet. Startfilen innehåller inga regler och inga beteendekrav.
2. Varje regelfil täcker ett område (arkitektur, process, dokumentation) och hålls så kort att filen läses i sin helhet; storlek över varningsnivån utlöser granskning (princip 1).
3. Nivåorden MÅSTE, FÅR INTE och BÖR används konsekvent och endast med den betydelsen.
4. Varje uppgift börjar med att AI:n redovisar vilka regelfiler som lästs och vilka regel-ID:n som berörs. I fas 0, innan regelfilerna finns, redovisar AI:n i stället vilka källavsnitt som berörs, i formen "System design, princip X regel Y" eller "Processdokumentet, Del 2, princip X" (processdokumentet, Del 1, fas 0, Undantag i fas 0).
5. Varje plan och varje sammanfattning hänvisar till regel-ID:n, så att varje ändring går att spåra till en regel.
6. Omdömesregler (kontroll: omdöme) listas i en egen sektion i varje regelfil och granskas vid varje fasbyte.

**Körbar grind:** `testa.py` kontrollerar att varje regel har ID, nivåord och ett kontrollfält, att varje ID är unikt, att varje kontrollfält är omdöme eller pekar på en kontroll som finns i `testa.py`, och att varje regel hänvisar till sin källa. Startfilens innehåll kontrolleras av grind 2.

**Avvägning:** Fler regler ger inte mer styrning. En kort lista entydiga, kontrollerade regler följs bättre än en lång lista goda råd.

## 9. Körbara grindar framför skriftliga påminnelser

**Huvudfråga:** Hur garanteras att reglerna faktiskt följs över tid?

**Princip:** Skriftliga påminnelser i dokumentation och promptinstruktioner försummas över tid. Manuella checklistor glöms, och AI-modeller tappar instruktionskontext när filer växer. Systemets integritet garanteras därför av körbara grindar (Executable Gates): automatiserade testskript som stoppar felaktiga ändringar omedelbart med en hård `pass`/`fail`-exitkod, både lokalt och i CI/CD-pipelinen.

**Körbara grindar i** `testa.py`

| Grind (princip): funktion | Kontrollerar |
| --- | --- |
| 1. Döda referenser (P7): doda_referenser | Sökvägar i dokumentation och kod som saknas |
| 2. Struktur (P1, P7, P8): struktur | Mappar och filer mot strukturplanen; filregistret; startfilens innehåll; filstorlek |
| 3. Ansvar (P1, P7): ansvar | Docstring i .py, ägarblock i dokumentation |
| 4. Importriktning (P3–5): import_riktning | Inga importer utåt, inga cirklar |
| 5. Rena inre lager (P6): rena_inre_lager | Inga databas-, webb- eller UI-bibliotek |
| 6. Publika gränssnitt (P2): publika_granssnitt | Inga interna namn över gränser |
| 7. Regelregister (P8): regelregister | ID, nivåord, kontroll och källhänvisning per regel |
| 8. Dubbletter (P7, P10): dubbletter | Samma regel i flera filer; återgivna regler utan markör och länk |
| 9. Enhetstester (P3): enhetstester | Körs utan nätverk och filsystem |
| 10. Stil (P9): stil | Linter och formatterare utan fel |

**Fel och varningar.** Varje fynd från en grind är ett fel eller en varning. Ett fynd är en varning i exakt två fall: filstorlek över varningsnivån i grind 2 (princip 1), och ett fynd som matchar en post i baslinjen. Alla andra fynd är fel. En grind ger `fail` om minst ett fynd är ett fel och annars `pass`, även när grinden har varningar. `testa.py` avslutas med exitkod 0 när samtliga grindar ger `pass` och annars med exitkod 1. En grind som saknar något att kontrollera, till exempel `import_riktning` innan kod finns, ger `pass`. En grind vars verktyg saknas, till exempel linter för grind 10, ger `fail` med en åtgärd om vad som ska installeras.

**Baslinje.** I ett befintligt projekt får varje avvikelse i anpassningsplanen en post i baslinjen. Ett fynd matchar en post när grind och fil stämmer och raden stämmer eller är 0. Baslinjen gör att `testa.py` ger `pass` från fas 0, med de kända avvikelserna som varningar, samtidigt som varje nytt fel stoppas. En ändring som åtgärdar en avvikelse tar bort dess post i samma ändring; baslinjen får aldrig utökas efter fas 0-gaten.

**Grindparametrar.** `testa.py` läser varningsnivåer, baslinje och grindarnas parametrar ur strukturplanens avsnitt `## Grindparametrar`, som innehåller exakt ett kodblock märkt `toml`. Blocket läses med Pythons `tomllib` och har följande form; mappar och värden är exempel som bestäms i fas 0:

```toml
[varningsniva]
rader_py = 400                 # filstorlek som ger varning i grind 2
rader_md = 300

[grind.ansvar]
undantag = ["kallor/**", "AGENTS.md"]   # källdokumentens mapp och startfilen

[grind.dubbletter]
undantag = ["kallor/**"]

[[baslinje]]
id = "AV-1"                    # avvikelsens ID i anpassningsplanen
grind = "ansvar"
fil = "src/gammal_modul.py"
rad = 0                        # 0 betyder hela filen
```

Namnet efter kolon är grindens funktion i testa.py och det namn som en regels kontroll anger, till exempel testa.py: import_riktning. Integrations-, E2E- och icke-funktionella tester ligger utanför testa.py och körs i pipelinen vid varje push.

**Regler**

1. `testa.py` körs före varje commit och i CI vid varje push. En ändring med `fail` går inte vidare.
2. Varje ny regel med kontrollen testa.py får sin kontroll i `testa.py` innan regeln räknas som gällande; omdömesregler gäller utan körbar kontroll men granskas vid varje fasbyte.
3. Utskriften anger för varje fynd nivå (fel eller varning), grind, fil, rad, regel-ID och åtgärd, så att fyndet går att rätta utan att leta, och för en varning från baslinjen även avvikelsens ID. Formatet är en rad per fynd: `<fel|varning> <grind> <fil>:<rad> <regel-ID> <åtgärd>`, följt av en rad per grind: `<pass|fail> <grind> (<antal fel> fel, <antal varningar> varningar)`.
4. Varningar stoppar inte flödet. AI:n redovisar varje varning i sammanfattningen av ändringen och för in varningen under öppna varningar i statusfilen, där varningarna granskas vid fasbyte.
5. `testa.py` följer själv systemets principer: varje kontroll är en egen funktion med ett ansvar.

**Avvägning:** En för strikt grind som ger falsklarm lär utvecklaren och AI:n att kringgå grinden. Hellre färre kontroller med hög träffsäkerhet än många som ofta behöver undantas.

## 10. Osäkerhet, negationer och avvägningar

**Huvudfråga:** Vad händer när reglerna inte räcker, krockar eller kräver omdöme?

**Princip:** Osäkerhet hanteras öppet, aldrig genom gissning. Förbud formuleras så att det tillåtna alternativet alltid framgår. Avvägningar mellan principer görs medvetet och dokumenteras.

### Gissningsförbud ("do NOT guess")

1. Saknas information för att utföra en uppgift korrekt stoppar AI:n och frågar. Antaganden fylls aldrig i tyst.
2. Frågan anger exakt vad som saknas och vilka alternativ som finns, så att svaret går snabbt.
3. Är ett antagande nödvändigt för att komma vidare redovisas antagandet uttryckligen i planen och godkänns innan arbetet fortsätter.
4. Påståenden om kodbasen ("funktionen finns i …") bygger alltid på faktisk sökning i repot, aldrig på minne.

### Negationer

En regel som bara säger vad som är förbjudet lämnar det tillåtna öppet för tolkning. Varje FÅR INTE-regel kompletteras därför med det tillåtna alternativet.

- *Svagt:* "FÅR INTE importera databaskod i domänen." *Starkt:* "FÅR INTE importera databaskod i domänen. Lagring sker via gränssnitt i `usecases/ports.py`."
- *Svagt:* "Skapa inte nya filer i onödan." *Starkt:* "Ny fil skapas endast när ett nytt ansvar uppstår; annars utökas befintlig ägare."
- *Svagt:* "Gissa inte." *Starkt:* "Vid saknad information: stoppa, beskriv vad som saknas, fråga."

### Arkitekturella avvägningar (trade-offs)

Principerna drar ibland åt olika håll. Valet görs medvetet och dokumenteras som ett arkitekturbeslut (ADR) med alternativ och konsekvenser.

**DRY kontra ARID**

- **DRY (Don't Repeat Yourself)** gäller främst kod och regler. Logik och regler finns på ett ställe; upprepning i kod ger buggar när kopiorna glider isär.
- **ARID (A Requirement for Information Duplication)** gäller främst dokumentation för läsare. Viss upprepning är nödvändig för läsbarhet; en instruktion som tvingar läsaren genom fem länkar följs inte.
- **Lösning:** Regeln *ägs* på ett ställe (DRY). Andra filer får återge regeln kort, inledd med markören "Se \<regel-ID>:" och med länk till ägaren, så att återgivningen skiljs från en fullständig regel och avvikelser upptäcks.

**Övriga avvägningar**

- **Djup modul kontra ett ansvar:** djup inom ett ansvar, aldrig bred över flera.
- **Låg koppling kontra enkelhet:** gränssnitt vid lagergränser och där test kräver utbyte, inte runt varje funktion.

**Körbar grind:** `testa.py` kontrollerar att varje återgiven regel inleds med markören "Se \<regel-ID>:" och länkar till ägarfilen. Att återgivningen inte motsäger ägarens formulering är en omdömesregel som granskas vid varje fasbyte.

# Bilaga: Snabbreferens

## Principerna i korthet

| Princip | Körbar grind i testa.py |
| --- | --- |
| 1. Ansvar framför radantal | Ansvarsbeskrivning; storleksvarning |
| 2. Djupa moduler | Publika gränssnitt |
| 3. Rena systemgränser | Importgraf; isolerade tester |
| 4. Beroenderegeln | Importriktning |
| 5. Beroendeinversion | Importriktning; kompositionsrot |
| 6. Databaser och UI | Rena inre lager |
| 7. En fil äger en sak | Ägarblock; register; dubbletter |
| 8. Regelverk för AI | Regelregister |
| 9. Körbara grindar | Grind 1–10 som helhet; regelregistret (grind 7) |
| 10. Osäkerhet | Återgivna regler bär markör och länk |


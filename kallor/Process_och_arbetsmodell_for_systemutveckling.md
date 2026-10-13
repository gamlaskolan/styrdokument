# Process och arbetsmodell för systemutveckling

2026-10-13 · Victor

## Översikt

Arbetsmodellen beskriver arbetssätt för att bygga appar tillsammans med en AI-assistent. 

Arbetet sker i sju faser, föregångna av en förberedande fas 0. Varje fas avslutas med en gate: ett beslut att fasen är klar innan nästa påbörjas. Faserna går från *varför* och *vad* (idé och krav) via *hur* (arkitektur och kod) till *fungerar lösningen* (test) och *håller lösningen över tid* (drift).

Fyra utgångspunkter gäller genom hela processen:

- **Eget behov först.** Kraven utgår från det egna arbetsflödet. Funktioner för andra användare byggs först när behovet finns, men beslut som stänger dörren för fler användare undviks.
- **Varje fas ger en leverabel.** Det skriftliga underlaget sparas i repot som projektdokument, så att nästa fas bygger på skriftligt underlag och inte på minnet av ett samtal.
- **Gates är skarpa men inte eviga.** En godkänd fas kan öppnas igen när ny kunskap kräver det, men medvetet: tillbaka till fasen, uppdatera dokumentet och passera gaten på nytt.
- **Processen upprepas per release.** Fas 0–4 görs grundligt för MVP:n. En ny funktion börjar därefter i fas 2; fas 3 körs när kvalitetskraven påverkas och fas 4 när arkitekturen påverkas; fas 5–7 körs alltid. Om fas 3 eller 4 påverkas redovisar AI:n med motivering i inventeringen (Del 2, arbetsflöde per ändring, steg 2), och utvecklaren avgör. Fas 1 öppnas igen om problem, användare eller framgångsmått ändras.

Varje fas nedan beskrivs med samma struktur: huvudfråga, syfte, aktiviteter, leverabel och gate-kriterier ("klart när").

Faserna körs i ordning, och varje fas avslutas med en gate som godkänns innan nästa fas påbörjas. Efter drift börjar nästa funktion om från kraven i fas 2.

**Samspel med System design:** Processdokumentet styr *när* – faser, gates och arbetsflöde. System design styr *hur* kod och filer formas – lager, regler och körbara grindar. Vid motsägelse gäller processdokumentet för faser och arbetsflöde och System design för struktur och regler; motsägelsen flaggas och rättas i ägardokumentet. **Regler och processbeskrivning.** Källdokumenten innehåller två slags innehåll som används på olika sätt efter fas 0:

- **Regler** – det System design, princip 8, räknar som regler, bland annat princip 1–7 i Del 2 – förs över till regelfilerna i fas 0 och läses därefter i regelfilerna.
- **Processbeskrivning** – Del 1: fasernas syfte, aktiviteter, leverabler och gate-kriterier, inklusive metoden i fas 1 – förs inte över, eftersom en kopia skulle bryta mot SSOT. AI:n läser processbeskrivningen i processdokumentet, som därför är en operativ fil och inte bara en källa.

**Läsfall.** Källdokumenten ligger i repot efter fas 0, och AI:n läser dem i exakt fyra fall (System design, princip 7, regel 5):

1. **Fasarbete.** Processdokumentet, Del 1, avsnittet för den fas statusfilen anger, samt arbetsflödet per ändring i Del 2: i början av varje session, när en fas påbörjas och vid varje gateavstämning.
2. **Regel- eller begreppsändring.** Det avsnitt som regelns källfält pekar på; källdokumentet och regelfilen ändras i samma ändring.
3. **Motsägelse.** De avsnitt som motsägelsen gäller, för att avgöra ägardokumentet.
4. **Fas 0.** Båda källdokumenten i sin helhet (Del 1, fas 0, Undantag i fas 0).

För att följa en regel läser AI:n alltid regelfilen; källdokumentets formulering läses bara när regeln ska ändras (läsfall 2).

## Begrepp

Begreppen nedan används på exakt samma sätt i båda dokumenten. Listan ägs av System design och återges ordagrant här; ändringar görs i System design först och förs över hit i samma ändring, med samma version. Versionen är datumet för den senaste ändringen av listan. Filnamn och mappar bestäms när ramverket byggs; begreppen anger roller, inte namn. Två undantag är fasta så att AI:n alltid hittar in: startfilens namn och regelfilernas namn. Version 2026-10-13.

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

# Del 1: Fas 0 och de sju faserna i design- och byggprocessen

## 0. Förberedelse – ramverket på plats (Bootstrap)

**Huvudfråga:** Finns ramverket som styr AI:n innan arbetet börjar?

**Syfte:** Skapa startfil, regelfiler, körbara grindar och projektstruktur före fas 1, så att varje ändring från första dagen följer reglerna och syns i statusfilen. I ett befintligt projekt inventeras dessutom nuläget.

**Förutsättning.** Fas 0 kräver båda källdokumenten i fullständig form, med samma begreppslista och samma version. Saknas ett källdokument, i repot eller bland filerna i sessionen, begär AI:n det av utvecklaren och påbörjar inte aktivitet 1 förrän det finns; ett utdrag eller en ändringslista räcker aldrig. Skiljer sig begreppslistorna åt redovisar AI:n skillnaden och föreslår att System design rättas först.

**Undantag i fas 0.** Arbetsflödet per ändring (Del 2) förutsätter regelfiler och `testa.py`, som skapas först i fas 0. Fram till att `testa.py` finns och ger pass gäller därför:

- Källdokumenten är de gällande reglerna. AI:n läser båda i sin helhet (läsfall 4).
- I inventeringen (steg 2) och i planen redovisar AI:n källavsnitt i stället för regel-ID:n, till exempel "System design, princip 8 regel 1" (System design, princip 8, regel 4). När regelfilerna finns används regel-ID:n.
- Verifieringen (steg 6) görs från och med aktivitet 5. Före det anger sammanfattningen "testa.py finns ännu inte", och AI:n kontrollerar i stället de skapade filerna mot gate-kriterierna för fas 0.
- Commit-meddelanden har referensen F0 och utelämnar hakparentesen tills regel-ID:n finns.

Från första gången `testa.py` ger pass gäller arbetsflödet utan undantag.

**Aktiviteter**

1. **Strukturplan.** Skapa mappstrukturen utifrån lagren och dokumentationstyperna i System design (princip 4 och 7) och skriv in strukturen i strukturplanen, som därefter äger strukturen.
2. **Startfil.** Skapa `AGENTS.md` i repots rot enligt begreppet Startfil.
3. **Källdokument och regelfiler.** För in båda källdokumenten oförändrade i repot. För därefter in samtliga regler ur källdokumenten, utan urval, i `ARK.md`, `DOK.md` och `PRO.md` i regelformatet, med ID, område och källa enligt System design, princip 8, som också anger vad som räknas som en regel och hur källfältet skrivs. Begreppslistan förs in i repot som en egen fil av Diátaxis-typen Reference, med ägarblock, och listas i filregistret.
4. **Filregister.** Skapa filregistret med sökvägen till varje versionshanterad fil. Registret uppdateras i samma ändring som en fil skapas, flyttas eller tas bort.
5. **Körbara grindar.** Skriv först in varningsnivåer och grindarnas parametrar i strukturplanens avsnitt `## Grindparametrar` enligt System design, princip 9; där System design inte anger ett värde föreslår AI:n ett värde i planen (Del 2, princip 3) och utvecklaren godkänner. Skapa därefter `testa.py` med samtliga tio grindar, som läser parametrarna därifrån och skiljer på fel och varningar enligt System design, princip 9.
6. **Status.** Skapa statusfilen med de sex fasta delarna enligt begreppet Ramverk och aktuell fas "fas 0 – pågår".
7. **Nulägesinventering (befintligt projekt).** AI:n inventerar befintlig kod och dokumentation och listar avvikelser mot reglerna. Avvikelselistan och en plan för stegvis anpassning dokumenteras i en anpassningsplan, som är ett projektdokument. Varje avvikelse får ett ID (AV-1, AV-2 …) och en post i baslinjen, så att `testa.py` ger pass med de kända avvikelserna som varningar medan varje nytt fel stoppas. Inventeringen görs därför genom att köra `testa.py` utan baslinje: varje fel som då rapporteras är en avvikelse. Anpassningen genomförs som vanliga ändringar enligt Del 2, inte som en omskrivning på en gång. Varje anpassningsändring åtgärdar en eller flera avvikelser och tar bort deras poster i baslinjen i samma ändring. Anpassningsplanen avslutas när baslinjen är tom.

**Ny session utan startfil.** Finns ingen `AGENTS.md` i repots rot har projektet inte passerat fas 0. AI:n startar då fas 0: i ett tomt repo som nytt projekt, i ett repo med kod eller dokumentation som befintligt projekt med nulägesinventering. AI:n kontrollerar först förutsättningen och redovisar sedan vilket fall som gäller i första planen.

**Leverabel:** Ramverket – startfil, regelfiler, begreppslista, strukturplan, filregister, statusfil, `testa.py` och källdokumenten – och i ett befintligt projekt även anpassningsplanen.

**Gate – klart när:**

- [ ] `testa.py` kan köras och ger pass; varningar tillåts och står i statusfilen
- [ ] Startfilen innehåller endast läsordning och länkar
- [ ] Samtliga regler ur båda källdokumenten finns i regelfilerna, och varje regel har ID, nivåord, motivering, kontroll och källa
- [ ] Varje körbar grind har sina parametrar i strukturplanen
- [ ] Filregistret listar varje versionshanterad fil
- [ ] Statusfilen visar "fas 0 – väntar på gate"

**Gate – tillägg för befintligt projekt:**

- [ ] Anpassningsplanen med avvikelselista är godkänd
- [ ] Varje avvikelse har en post i baslinjen, och `testa.py` ger pass med avvikelserna som varningar

## 1. Vision & idégenerering – whiteboardfasen (Discovery & Feasibility)

**Huvudfråga:** Vad är idén, och är idén värd att bygga?

**Syfte:** Ta en lös idé till en färdig, genomtänkt idé, inklusive grunderna i utformningen, innan tid läggs på krav eller kod. Fasen sker på en whiteboard där idén växer fram visuellt, svar för svar. Whiteboarden är arbetsytan under sessionen, i chatten eller i ett whiteboardverktyg; allt som ska bevaras förs över till fasens leverabel innan sessionen avslutas, med skisser som Mermaid-diagram.

### Sokratisk metod med AI som samtalsledare

Idégenereringen bygger på sokratiska frågeställningar. AI:n leder samtalet genom hela fasen och följer fem riktlinjer; utvecklaren äger besluten:

1. **Frågor i stället för svar.** AI:n föreslår inte färdiga lösningar eller beslut utan ställer frågor som gör idén tydligare. AI:n får bidra med idéer i form av alternativa vinklar, mikroexempel och sammanfattningar av tidigare svar. Mikroexempel hämtas alltid från en annan idé eller ett neutralt sammanhang, aldrig från utvecklarens egen idé, så att exemplet inte blir ett färdigt svar.
2. **En fråga i taget.** Varje svar får följdfrågor tills svaret är konkret: "Vad menas med det?", "Vilket exempel finns?", "Vad händer om …?" AI:n leder aktivt genom stegen, ett i taget, inom ramen för den övergripande idén.
3. **Antaganden och motsägelser lyfts fram.** Svar som vilar på ett antagande eller krockar med ett tidigare svar markeras och utreds.
4. **Sammanfattning efter varje steg.** AI:n sammanfattar svaren i några punkter, som fångas på whiteboarden.
5. **Nästa steg först när steget är klart.** Ett steg avslutas när sammanfattningen godkänns.

### Frågetrappan: från Vad? till färdig idé

Idén bryts ner i steg, från det breda till det konkreta. Varje steg bygger på svaren från föregående steg.

| Steg och huvudfråga | Resultat på whiteboarden |
| --- | --- |
| 1. Vad? Vad är idén? | Idén i en mening |
| 2. Varför? Vilket problem löses? | Problembeskrivning |
| 3. För vem? Vilken användare? | Primär och framtida användare |
| 4. Hur i dag? Nuvarande lösning? | Brister i nuvarande lösning |
| 5. Kärnan? Minsta värdefulla version? | Kärnfunktioner (grund för MVP) |
| 6. Utformning? Hur ser appen ut? | Skisser av vyer och flöde |
| 7. Risker? Vad kan gå fel? | Risklista och genomförbarhet |
| 8. Framgång? Hur märks resultatet? | Framgångsmått |

**Exempel på följdfrågor per steg**

1. **Vad?** Hur låter idén i en mening? Vad är idén inte?
2. **Varför?** Vad händer om appen aldrig byggs? Hur ofta uppstår problemet?
3. **För vem?** I vilken situation uppstår behovet? Kan fler användare bli aktuella senare?
4. **Hur i dag?** Vad fungerar med nuvarande lösning? Vad saknas?
5. **Kärnan?** Vad går att ta bort utan att värdet försvinner? Vilken enskild funktion är viktigast?
6. **Utformning?** Vilka vyer behövs? Vilket flöde är vanligast? Vilken känsla ska UI:t ge?
7. **Risker?** Finns tid, teknik och kompetens? Vilket antagande är osäkrast?
8. **Framgång?** Vad går att mäta? Vad är skillnaden mot i dag?

### Spelpedagogik i frågetrappan

Frågetrappan utformas som ett spel med åtta nivåer, dock säger AI:n inte detta utan använder detta som samtalsmetod. Inspirationen kommer från ledande spel (Super Mario Bros., Portal 2) och gamifierade appar (Duolingo): utvecklaren lär sig genom att göra, i en säker miljö, och nästa nivå låses upp först när den förra är bemästrad.

**Utgångspunkt:** Engagemanget byggs på tre drivkrafter som också bär lärandet: känslan av framsteg, ägandeskap över idén och växande mästerskap.

**Mått på en lyckad session:** en tydligare idé och djupare förståelse, aldrig tid i appen.

#### Player's Journey

Trappan följer spelens fyra etapper: Discovery, Onboarding, Scaffolding och Endgame. Stödet är störst i början och monteras ner i takt med att utvecklaren bemästrar momenten.

Etapperna motsvarar stegen i frågetrappan:

- **Discovery – försteg före steg 1, inte en egen nivå:** AI:n visar en kort exempeltrappa för en annan idé, en rad per steg. Exempeltrappan visas en gång, som ett mikroexempel, och ersätter inte utvecklarens eget arbete.
- **Onboarding – steg 1–2:** exempelsvar och mallar vid varje fråga.
- **Scaffolding – steg 3–6:** exempel och mallar tas bort steg för steg.
- **Endgame – steg 7–8:** utvecklaren leder och AI:n granskar. Rollbytet från lärare till granskare sker vid steg 7.

#### Lärande genom handling ("Show, Don't Tell")

1. **Ingen textguide.** Varje nytt moment visas med ett mikroexempel på några rader och provas direkt. Förklaringar ges först när utvecklaren efterfrågar dem. Syftesmeningen i början av varje steg är en orientering på en mening, inte en guide.
2. **Varje steg är en nivå.** Nivån låses upp när steget är bemästrat: svaret klarar AI:ns kontrollfrågor och sammanfattningen är godkänd.
3. **Säker miljö.** Inga svar är fel, bara utkast. Varje svar går att ändra, och ett tidigare steg går alltid att öppna igen utan förlust.
4. **En mekanik i taget.** Steg 1–2 tränar konkretion (en mening, utan lösning). Steg 3–4 tränar perspektiv. Steg 5–6 tränar avgränsning och skiss. Steg 7 tränar kritisk granskning och steg 8 mätbarhet.

#### Drivkrafter i varje steg

- **Framsteg:** en nivåkarta 1–8 på whiteboarden visar för varje steg status (låst, aktuell eller klar) och en sammanfattning på högst en mening. Kartan speglar godkända steg, aldrig uppblåsta procent.
- **Ägandeskap:** varje godkänt svar blir ett idékort på whiteboarden. Korten bygger tillsammans upp idén, synligt och påtagligt.
- **Mästerskap:** återkopplingen är specifik och kopplad till kvalitet, till exempel "problemet är mätbart och nämner ingen lösning", aldrig tomt beröm.
- **Kreativitet:** steg 6 börjar med utvecklarens egen skiss på whiteboarden; skissen kan vara en enkel lista i text. Därefter får AI:n föreslå alternativa skisser i textform, med boxar och pilar eller som Mermaid-diagram, som utvecklaren väljer från eller avvisar.
- **Mening:** varje steg börjar med en mening om *varför* steget finns och vad steget ger idén.
- **Bossnivå:** steg 7 är en utmaning där AI:n agerar granskare och söker svagheter i idén. Bossnivån är en övning, inte ett prov: varje svaghet som hittas leder till att idén revideras, och belöningen är en idé som håller. Granskningen avslutas när varje risk från steg 7 i frågetrappan är bedömd; hittas inga svagheter är steget klart.

#### Spelmekanik i frågetrappan

Mekanikerna nedan är hämtade från spel och gamifierade appar och anpassade för lärande. Varje mekanik har ett pedagogiskt syfte: att göra framsteg synliga, hålla flödet igång eller göra miljön trygg nog att pröva och ompröva. Nivåkartan stöder reflektion och är aldrig ett framgångsmått.

| Mekanik | Användning i frågetrappan |
| --- | --- |
| Nivåer och upplåsning | Åtta nivåer; en nivå låses upp när steget är bemästrat |
| Framstegsmätare | Nivåkarta som speglar godkända steg |
| Insiktskort | AI:n lyfter en oväntad koppling eller insikt när en sådan finns; insikten sparas i fasens leverabel |
| Ny vinkel | Alternativ följdfråga när ett svar kör fast |
| Föreslaget nästa steg | Nästa nivå föreslås och startar efter godkännande |
| Specifik återkoppling | Konkret bekräftelse på vad i svaret som håller |
| Anpassade följdfrågor | Svårighetsgraden följer svarens kvalitet |
| AI:n ger först | Exempel från en annan idé och sammanfattningar som stöd innan utvecklaren svarar |
| Egen utveckling | Jämförelse med egna tidigare idéer, inte med andra |
| Återupptagning | Statusfilen visar var arbetet slutade; AI:n sammanfattar läget vid nästa session |
| Tydligt slut | Trappan avslutas efter steg 8 med en färdig idé |
| Fri paus | Allt sparas löpande. Att hoppa över gäller en följdfråga, aldrig ett steg |
| Ärligt avslut | Att lägga ner idén efter steg 2 eller 7 är ett godkänt utfall; gaten passeras då inte och fas 2 påbörjas inte. Statusfilen sätts enligt Del 2, princip 2 |

### Grunder i utformning

Steg 6 ger en första skiss av appen, inte en färdig design. Skisserna räcker för att kraven i fas 2 och arkitekturen i fas 4 ska ha något konkret att utgå från:

- **Huvudvyer:** de 2–5 skärmar eller ytor appen består av
- **Huvudflöde:** de vanligaste momenten från start till mål, som en lista i text eller ritade som boxar och pilar
- **Interaktionsprincip:** hur appen främst används, till exempel dra och släpp, formulär eller tangentbord
- **Känsla:** några ord om tonen i UI:t, till exempel minimalistisk, lekfull eller tät och effektiv

**Leverabel:** Ett visionsdokument med svaren från alla åtta steg och sammanfattningen: idén i en mening, problem, primär användare, nuvarande lösning, kärnfunktioner, utformningsskisser som Mermaid-diagram, risker och framgångsmått. Idékort, sammanfattningar och insikter sparas i visionsdokumentet; nivåkartan och öppna följdfrågor sparas i statusfilen.

**Gate – klart när:**

- [ ] Samtliga åtta steg i frågetrappan är besvarade och sammanfattade
- [ ] Idén går att beskriva i en mening utan att nämna tekniken
- [ ] Kärnfunktionerna är avgränsade till den minsta version som ger värde
- [ ] Huvudvyer och huvudflöde är skissade
- [ ] De största riskerna är bedömda som hanterbara
- [ ] Minst ett mätbart framgångsmått är definierat
- [ ] Inga öppna följdfrågor återstår från AI:n

## 2. Funktionella krav (Functional Requirements)

**Huvudfråga:** Vad ska systemet göra?

**Syfte:** Översätta visionen till konkreta, testbara beteenden och bestämma exakt vad första versionen innehåller.

**Aktiviteter**

1. **User stories.** Format: *"[Roll] behöver [handling] för att [nytta]"*. Varje user story får ett ID, till exempel US-1. Exempel: "Användaren behöver kunna skapa en post-it-lapp för att snabbt fånga en idé."
2. **Acceptanskriterier.** 2–5 kriterier per user story som avgör när storyn är uppfylld, gärna i formatet *Givet / När / Så*. Kriterierna blir senare testfall i fas 6.
3. **Användarflöden (User Flows).** Beskrivning i ordningsföljd av de viktigaste flödena, inklusive felfall (till exempel tappad uppkoppling).
4. **Prioritering med MoSCoW.** Varje krav märks *Must*, *Should*, *Could* eller *Won't (nu)*.
5. **Avgränsning för MVP (Feature Scope).** MVP = samtliga *Must*-krav. Funktioner utanför MVP listas uttryckligen, för att hålla omfånget stabilt.

**Leverabel:** Ett kravdokument med user stories, acceptanskriterier, prioritering och en tydlig MVP-lista.

**Gate – klart när:**

- [ ] Samtliga Must-krav har testbara acceptanskriterier
- [ ] Huvudflödena är beskrivna, inklusive felfall
- [ ] MVP-gränsen är dragen och listan över funktioner utanför MVP är skriven
- [ ] Varje krav går att spåra tillbaka till problemet i fas 1

## 3. Icke-funktionella krav (Non-Functional Requirements)

**Huvudfråga:** Vilka kvaliteter och begränsningar gäller för systemet?

**Syfte:** Bestämma *hur väl* systemet ska fungera. Kvalitetskraven styr arkitekturvalen i fas 4 mer än de funktionella kraven, och behöver därför vara klara först.

**Utgångspunkt:** Ett icke-funktionellt krav ska vara mätbart. "Appen ska vara snabb" går inte att testa; "en ändring sparas inom 200 ms" går att testa.

**Aktiviteter:** Gå igenom varje kvalitet i listan och skriv minst ett mätbart krav, eller notera uttryckligen att kvaliteten saknar relevans för MVP. För en app i eget bruk räcker ofta enklare nivåer för skalbarhet och säkerhet; notera i så fall vad som måste skärpas om appen öppnas för fler.

- **Prestanda (Performance)** – Hur snabbt svarar systemet? *Exempel:* sidan laddas på under 2 s; ändringar synkas inom 200 ms.
- **Skalbarhet (Scalability)** – Hur mycket last ska systemet klara? *Exempel:* 10 000 objekt per tavla i eget bruk; 50 samtidiga användare om appen öppnas för fler.
- **Driftssäkerhet (Reliability)** – Hur ofta får systemet vara nere, och vad händer vid fel? *Exempel:* 99,5 % tillgänglighet; arbete går aldrig förlorat vid tappad uppkoppling.
- **Säkerhet (Security)** – Vilka behörigheter gäller, och hur skyddas data? *Exempel:* data krypteras i transit; inloggning och behörigheter krävs först när fler användare tillkommer.
- **Underhållbarhet (Maintainability)** – Hur lätt går koden att ändra och felsöka? *Exempel:* testtäckning över 70 % för kärnlogik; varje modul har en ansvarsbeskrivning och testa.py ger pass.
- **Portabilitet (Portability)** – På vilka plattformar ska systemet köras? *Exempel:* senaste två versionerna av Chrome, Safari, Firefox och Edge; fungerar på surfplatta.
- **Användbarhet och tillgänglighet (Usability)** – Vilka krav på användbarhet och tillgänglighet gäller? *Exempel:* alla funktioner nåbara med tangentbord; kontrast enligt WCAG 2.1 AA.

**Leverabel:** Ett dokument för icke-funktionella krav med ett mätbart krav per relevant kvalitet.

**Gate – klart när:**

- [ ] Varje kvalitet har ett mätbart krav eller en motivering till uppskjutning
- [ ] Kraven är realistiska givet tid och resurser från fas 1
- [ ] Krav med störst påverkan på arkitekturen är markerade

## 4. Systemarkitektur & design (System Architecture)

**Huvudfråga:** Hur ser modulerna och dataflödet ut?

**Syfte:** Bestämma systemets övergripande form innan koden skrivs: vilka delar som finns, vad varje del ansvarar för och hur data rör sig mellan delarna. Arkitekturen ska uppfylla kraven från fas 2 och 3.

**Aktiviteter**

1. **Gränsdragning (Boundary Definition).** Dela upp systemet i lagren enligt System design (domän, användningsfall, adaptrar, ramverk) och moduler (till exempel canvas, lagring, export). Varje modul får ett tydligt ansvar och ett definierat gränssnitt mot övriga moduler.
2. **Dataflöde och SSOT (Single Source of Truth).** För varje typ av data bestäms var datan *ägs*. All övrig kod läser därifrån och skriver via ägaren, aldrig direkt. Rita hur en ändring flödar: användarhandling → tillståndet uppdateras → ändringen sparas → resultatet visas.
3. **Datamodell.** De centrala objekten, objektens fält (till exempel `Board`, `Element`) och kopplingarna mellan objekten. Kan appen bli aktuell för fler användare senare: planera för ett `User`-begrepp redan nu, även med bara en användare.
4. **Teknikval (Technology Stack).** Välj språk och motivera valet mot kraven, inte mot vana. Databas, webbramverk och UI väljs först när ett verkligt behov kräver valet (System design, princip 6); fram till dess används minnesbaserade implementationer bakom gränssnitt.
5. **Arkitekturbeslut (ADR).** Varje viktigt val dokumenteras kort: sammanhang, beslut, bortvalda alternativ och konsekvenser.

**Leverabel:** Ett arkitekturdokument med moduldiagram, dataflöde, datamodell och teknikval, samt ett arkitekturbeslut (ADR) per fil. Båda ingår i leverabeln.

**Gate – klart när:**

- [ ] Varje modul har ett ansvar som går att beskriva i en mening
- [ ] Varje typ av data har exakt en ägare (SSOT)
- [ ] Dataflödet för de viktigaste user stories är ritat
- [ ] Fattade teknikval är motiverade mot kraven; uppskjutna val är listade med vad som utlöser beslutet
- [ ] Filstrukturen är bestämd, speglar lagren och är införd i strukturplanen som en ändring enligt Del 2

## 5. Implementation & moduldesign (Coding)

**Huvudfråga:** Hur skrivs koden inuti varje del?

**Syfte:** Bygga modulerna från fas 4 i små, granskningsbara ändringar, med kod som är lätt att förstå, testa och ändra.

**Aktiviteter**

1. **En story i taget.** User stories implementeras i prioritetsordning. Varje ändring är liten nog att granskas på några minuter och lämnar systemet i fungerande skick. Lagringsgränssnitt implementeras först minnesbaserat (System design, princip 6).
2. **Single Responsibility.** Varje modul, klass och funktion har ett ansvar. Kräver beskrivningen av en funktion ordet "och" är funktionen troligen för stor.
3. **Respektera gränserna.** Moduler anropas endast via definierade gränssnitt. Behov av en genväg är en signal att se över arkitekturen, inte att bryta gränsen.
4. **Ren kod (Code Craftsmanship).** Beskrivande namn, funktioner med ett ansvar, ingen duplicerad logik, inga "magiska" värden. Kommentarer förklarar *varför*; koden visar *vad*.
5. **Konsekvent stil.** Linter och formatterare körs automatiskt som grind 10 (stil) i testa.py, så att stilfrågor aldrig kräver eftertanke.
6. **Tester skrivs tillsammans med koden.** En story räknas som klar först när tillhörande enhetstester finns (se fas 6).

**Leverabel:** Fungerande kod i repot, där varje story består av en eller flera commits, samt uppdaterat arkitekturdokument eller en ny ADR vid avvikelser från arkitekturen. Varje commit är en ändring och bär storyns ID som referens. Fas 5 har inget eget projektdokument.

**Gate – klart när (varje MVP-story uppfyller):**

- [ ] Acceptanskriterierna från fas 2 är uppfyllda
- [ ] Enhetstester finns och passerar
- [ ] Varje commit för storyn följer formatet i arbetsflödet per ändring (Del 2, steg 8)
- [ ] testa.py ger pass i samtliga grindar, bland annat import_riktning (grind 4), publika_granssnitt (grind 6) och stil (grind 10)
- [ ] Dokumentationen är uppdaterad enligt tabellen i Del 2, steg 7

## 6. Testning & kvalitetssäkring (Verification)

**Huvudfråga:** Fungerar systemet enligt planen?

**Syfte:** Bevisa att systemet uppfyller både de funktionella kraven (fas 2) och de icke-funktionella kraven (fas 3), och fortsätter göra så vid kodändringar.

**Testnivåer** – många snabba tester längst ner, få långsamma högst upp. Endast enhetstesterna körs utan nätverk och filsystem:

- **Enhetstester (Unit)** – en funktion eller modul isolerat. *Exempel:* flytt av ett element uppdaterar rätt koordinater.
- **Integrationstester (Integration)** – samspelet mellan moduler. *Exempel:* en ändring sparas i databasen och går att läsa tillbaka.
- **End-to-end-tester (E2E)** – ett helt användarflöde i webbläsaren. *Exempel:* skapa tavla, lägg till lapp, ladda om, lappen finns kvar.
- **Icke-funktionella tester** – mätbara krav från fas 3. *Exempel:* prestandamätning med 10 000 objekt; tillgänglighetskontroll.

**Aktiviteter**

1. **Härled testfall från acceptanskriterierna.** Varje kriterium i fas 2 motsvaras av minst ett test.
2. **Automatisera.** Enhetstester körs i testa.py före varje commit; integrations-, E2E- och icke-funktionella tester körs i pipelinen vid varje push (System design, princip 9), så att fel upptäcks direkt och inte veckor senare.
3. **Testa felfallen.** Tappad uppkoppling, ogiltig indata, samtidiga ändringar och saknade behörigheter.
4. **Egen vardagsanvändning.** Inför varje release används appen i det egna arbetet under en period. Daglig användning avslöjar brister som automatiska tester missar.

**Leverabel:** Automatiserade tester i repot samt en teststrategi med vilka tester som körs på vilken nivå.

**Gate – klart när:**

- [ ] Samtliga tester passerar
- [ ] Varje Must-krav har minst ett test
- [ ] De icke-funktionella kraven är mätta och uppfyllda
- [ ] Inga kända allvarliga buggar återstår

## 7. Drift & förvaltning (Deployment & Maintenance)

**Huvudfråga:** Hur hålls systemet levande och stabilt över tid?

**Syfte:** Leverera systemet säkert och upprepbart, upptäcka problem tidigt och hålla koden frisk när kodbasen växer.

**Driftform styr omfattningen.** Fas 7 skalas efter hur appen körs, enligt kraven i fas 3 och besluten i fas 4:

- **Lokal app i eget bruk:** utrullning med ett kommando, backup av data och provad återställning. Rollback innebär återgång till föregående commit eller version och provas en gång. Övervakning, larm och separat testmiljö är ej tillämpliga.
- **Egen server:** därutöver automatisk utrullning, rollback som provas genom att köras en gång mot servern, loggning och larm.
- **Flera användare:** därutöver en separat testmiljö (staging) före produktion, där rollback provas.

Ett kriterium som är ej tillämpligt för driftformen stryks inte. Rutan kryssas och kriteriet får tillägget "ej tillämpligt – \<driftform>, se driftdokumentet", där motiveringen står.

**Aktiviteter**

1. **Utrullningspipeline (Deployment Pipeline).** Varje ändring går automatiskt genom bygge → testa.py → pipelinens tester → testmiljö (vid flera användare) → produktion. Ingen manuell kopiering av filer till servern.
2. **Miljöer och konfiguration.** Separata miljöer för utveckling och produktion, med en extra testmiljö när fler användare tillkommer. Hemligheter (lösenord, API-nycklar) ligger aldrig i koden.
3. **Övervakning och loggning (Monitoring & Logging).** Logga fel och viktiga händelser, mät svarstider och tillgänglighet mot kraven i fas 3, och larma vid avvikelser.
4. **Backup och återställning.** Automatisk säkerhetskopiering av data, med regelbundet testad återställning.
5. **Rollback.** Återgång till föregående version ska ta några minuter vid problem efter en release.
6. **Kontinuerlig förbättring (Refactoring).** Återkommande tid avsätts för att städa kod, uppdatera beroenden och betala av teknisk skuld, innan skulden gör nya funktioner dyra att bygga.
7. **Återkoppling till fas 1–2.** Erfarenheter från egen användning och felrapporter blir underlag för nästa omgång krav i fas 2. Fas 1 öppnas igen om problem, användare eller framgångsmått ändras.

**Leverabel:** Fungerande utrullning enligt driftformen, med pipeline och övervakning med larm där driftformen kräver det, samt ett driftdokument med instruktioner för utrullning, rollback och felsökning.

**Gate – klart när (inför första release, enligt driftformen):**

- [ ] Utrullning sker automatiskt med ett kommando eller en merge
- [ ] Rollback är provad enligt driftformen
- [ ] Övervakning och larm är aktiva
- [ ] Backup är aktiv och en återställning är provad
- [ ] Driftdokumentationen räcker för utrullning och felsökning efter flera månaders uppehåll

# Del 2: Best practice för AI-samarbete

AI:n leder processen aktivt och gör det tunga arbetet: håller reda på fas och steg, föreslår nästa moment, söker, läser, skriver och uppdaterar. Besluten fattas av utvecklaren. Att leda betyder att föreslå: när AI:n frågar presenterar AI:n alltid ett rekommenderat alternativ med motivering, så att utvecklaren kan svara med ett godkännande. En fråga med förslag är därför aldrig ett avsteg från att leda. Principerna för AI-samarbete bevarar rollfördelningen. Principerna är omdömesregler (kontroll: omdöme) och granskas vid varje fasbyte; i fas 0 förs de in i regelfilerna med ID i området PRO.

## Principer för AI-samarbete

**1. Inga manuella sökningar.** Radnummer, filnamn och mappstrukturer letas aldrig upp manuellt. AI:n inventerar och söker i repot och hänvisar till exakta filer och rader i förklaringar.

- *I praktiken:* Uppdraget beskrivs i klartext ("flytta valideringen till en egen modul"); AI:n hittar var koden finns.

**2. Portgång per fas (Gates).** Nästa fas påbörjas aldrig förrän föregående fas är godkänd. AI:n stämmer av mot gate-kriterierna i Del 1 och begär uttryckligt godkännande före fasbyte. Fasgates godkänns av utvecklaren; körbara grindar (testa.py) kontrollerar reglerna automatiskt. Båda krävs för att gå vidare. Vid fasbyte granskas även öppna varningar i statusfilen och omdömesreglerna (System design, princip 8–9).

- *I praktiken:* En fas avslutas med en avstämning i stil med "Gate för fas 3: alla tre kriterier uppfyllda – godkänt att gå vidare till fas 4?"
- *Undantag:* Kräver ny kunskap att en tidigare fas öppnas igen, flaggar AI:n behovet och föreslår vilken fas och vilket dokument som behöver ändras.

**Statusfilen vid gate, release och avslut.** Statusfilen sätts alltid på samma sätt:

| Händelse | Aktuell fas och senaste gate | Pågående ändring | Senaste ändring | Nästa mål | Varningar | Nivåkarta och följdfrågor |
| --- | --- | --- | --- | --- | --- | --- |
| Alla kriterier uppfyllda, avstämning begärd | "fas N – väntar på gate" | Ingen | Oförändrad | Första ändringen i fas N+1 | Oförändrade | Oförändrade |
| Utvecklaren godkänner gaten | "fas N+1 – pågår"; senaste gate: fas N, datum | Ingen | Gatebeslutet | Oförändrat | Oförändrade | "Ej aktuellt" när fas 1 lämnas |
| Ny release (gate för fas 7 godkänd) | "fas 2 – pågår"; senaste gate: fas 7, datum och release | Ingen | Releasen | Ur återkopplingen i fas 7, annars "Ej planerat" | Oförändrade, eftersom öppna varningar fortfarande gäller | "Ej aktuellt" |
| Ärligt avslut i fas 1 | "fas 1 – avslutad utan gate (steg N)"; senaste gate oförändrad | Ingen | Beslutet och skälet | "Ej planerat" | Oförändrade | Oförändrade, som underlag om idén tas upp igen |
| Fas öppnas igen | "fas N – pågår (öppnad igen)"; senaste gate oförändrad | Ingen | Beslutet att öppna fasen | Ändringen i fasens dokument | Oförändrade | Återställs ur versionshistoriken om fas 1 öppnas |

Statusfilen skrivs vid avstämning och vid godkännande, aldrig i förskott. Uppdateringen efter ett gatebeslut görs utan plan, eftersom beslutet redan är fattat, och sparas som en egen commit med referensen för den fas som godkänns, till exempel F0: godkänn gate. Vid ärligt avslut skrivs beslutet och skälet även in i visionsdokumentet.

**3. Plan först (Dry Run).** Innan kod skrivs eller ändras presenterar AI:n en plan för granskning och godkännande. Planen innehåller:

- filer som skapas, ändras eller tas bort
- ändringen i varje fil, en mening per fil
- krav, user stories och regel-ID:n som ändringen berör
- tester som läggs till eller påverkas
- risker och sidoeffekter

**4. Levande dokumentation.** Beslut, krav och strukturförändringar uppdateras i projektets dokumentation i samma ändring som koden – aldrig "senare". Dokumentationen beskriver alltid systemet i nuvarande skick.

**5. Små ändringar.** En ändring i taget: stor nog att vara meningsfull, liten nog att granskas snabbt. Större uppgifter delas upp i flera planer. Går målet inte att beskriva i en mening är ändringen för stor och delas upp; nästa ändrings mål i statusfilen är då målet för den första delen.

**6. Fråga hellre än gissa.** Vid otydliga eller motsägelsefulla krav stannar AI:n och frågar, i stället för att fatta beslutet på egen hand.

**7. Verifiera efteråt.** Efter varje ändring kör AI:n testa.py och redovisar resultatet. En ändring är klar först när testa.py ger pass.

## Arbetsregler

Arbetsreglerna kompletterar principerna med utvecklarens beslut om sessionens start och slut, filhantering, kontroll, gränser och språk. Arbetsreglerna är omdömesregler (kontroll: omdöme) och granskas vid varje fasbyte; i fas 0 förs de in i regelfilerna med ID i området PRO.

1. Sessionen startar med raden `Läs AGENTS.md och följ den. Projekt: <slug>.`, och `<slug>` i startfilens länkar är det angivna projektet. Anger startraden inget projekt gäller projektet i `AGENTS.local.md` i repots rot (git-ignorerad, en per dator). Saknas båda frågar AI:n efter projektet innan något annat läses.
2. Efter läsningen skriver AI:n ett startkvitto med projekt, aktuell fas, pågående ändring, nästa ändrings mål och öppna varningar, var och en med fil som källa. Det som saknas skrivs "saknas".
3. Innan sessionen lämnas, eller när den blir för lång, uppdaterar AI:n statusfilen, committar och pushar och skriver startraden för nästa session. Kan AI:n inte committa lämnas ändringarna till utvecklaren.
4. AI:n läser en fil från disk innan filen ändras och bygger ändringen på det lästa innehållet, aldrig på minnet.
5. En fil har en skrivare åt gången, och AI:n kontrollerar att inget annat jobb kör mot filen.
6. Varje avslutad ändring committas och pushas med det godkända commit-meddelandet ordagrant. Verktygets `Co-Authored-By`-rad får stå sist.
7. "Oförändrat" bevisas med en jämförelse mot ett sparat före-läge, aldrig mot HEAD.
8. Förväntat och uppmätt värde räknas på samma sätt.
9. En sökning som säger "saknas" visas med `repr()` innan något ändras.
10. Filer som ska finnas kvar mellan kommandon eller läsas av utvecklaren läggs i den git-ignorerade arbetsytan i repots rot som strukturplanen anger, aldrig i `/tmp`. Testkopior skapas i arbetsytan.
11. En projektmapp raderas, flyttas eller ersätts aldrig i sin helhet. Ändringar görs fil för fil enligt en godkänd plan.
12. AI:n ändrar aldrig utvecklarens arkiv. Materialet läses när utvecklaren hänvisar dit, och det som ska användas förs in i projektets filer.
13. AI:n bygger det som den godkända planen anger och inga funktioner som inte behövs nu.
14. Filerna vinner över chatten, och varje påstående om arbetet pekar på en fil eller en commit. Står svaret inte i filerna men mönstret är känt markerar AI:n förslaget som ej förankrat i filerna. Finns svaret ingenstans skriver AI:n "vet inte".
15. AI:n säger till när något är dåligt, osäkert eller okänt.
16. AI:n förklarar varför koden ser ut som den gör. Kod som är för svår för utvecklaren att läsa förenklas, kommenteras eller delas.
17. Chatten förs på svenska. Kod och tekniska termer får vara engelska.
18. AI:n skriver med mänsklig ton på vardaglig svenska, kort och i punktform, så att svaret är lätt att läsa. Rollerna benämns med utvecklarens initialer och "AI:n" när det gäller vem som beslutar eller utför.
19. Svaren är raka, konkreta och korta, i punktform som ryms på en skärm, med högst tre instruktioner till utvecklaren per svar. En granskning får vara längre och har rubrikerna Läst, Motsägelser, Fel, Best practice, Öppna frågor och Bedömning.
20. En ny regel bygger på ett fel som faktiskt har inträffat. AI:n föreslår ändringen med motivering och väntar på utvecklarens beslut.
21. När två regler, två filer eller en regel och ett källdokument säger emot varandra, eller när en pekare leder till något som inte finns, stannar AI:n, redovisar motsägelsen med fil och rad och frågar utvecklaren. Fram till beslutet gäller källdokumentens ordning: processdokumentet för faser och arbetsflöde, System design för struktur och regler.
22. Startfilen, regelfilerna, begreppslistan, strukturplanerna, mallarna och källdokumenten ändras endast när planen namnger filen och utvecklaren uttryckligen har godkänt just den ändringen. Övriga filer ändras enligt en godkänd plan (princip 3).

## Arbetsflöde per ändring

1. **Beskrivning:** målet med ändringen formuleras.
2. **Inventering:** AI:n läser relevanta filer och redovisar vilka regelfiler som lästs och vilka regel-ID:n som berörs, samt om ändringen påverkar kvalitetskraven (fas 3) eller arkitekturen (fas 4).
3. **Plan:** AI:n presenterar en plan enligt princip 3 i Del 2.
4. **Granskning:** planen godkänns, justeras eller avvisas.
5. **Genomförande:** ändringen görs enligt den godkända planen, inget utöver.
6. **Verifiering:** testa.py körs med samtliga grindar, inklusive stil (grind 10).
7. **Dokumentation:** berörd dokumentation uppdateras enligt tabellen nedan. Varje rad vars villkor stämmer gäller; filen som ska uppdateras listas redan i planen.

   | Om ändringen … | … uppdateras |
   | --- | --- |
   | gäller vad som helst | statusfilen (alltid) |
   | skapar, flyttar eller tar bort en fil | filregistret |
   | skapar, flyttar eller tar bort en mapp | strukturplanen |
   | skapar eller ändrar en modul eller funktion | docstring i berörd `.py`-fil |
   | ändrar en moduls ansvar, gränssnitt eller beroenden | arkitekturdokumentet |
   | avviker från arkitekturen eller fattar ett nytt teknikval | ny ADR och arkitekturdokumentet |
   | ändrar ett krav eller en user story | kravdokumentet eller dokumentet för icke-funktionella krav |
   | ändrar en regel | regelfilen och källdokumentet som källfältet pekar på |
   | ändrar ett begrepp | begreppslistan och båda källdokumenten, med ny version |
   | ändrar utrullning, backup eller rollback | driftdokumentet |
   | ändrar vilka tester som körs på vilken nivå | teststrategin |

8. **Sammanfattning:** vad som ändrades, berörda regel-ID:n och eventuella avvikelser från planen, varningar från testa.py samt vid en regeländring vilken källa som ändrades, angiven med källfältet. Sammanfattningen sparas i statusfilen som senaste ändring. Commit-meddelandet följer formatet \<referens>: \<vad som ändrades> [\<regel-ID:n>], där referensen är exakt en: storyns ID om ändringen hör till en story (US-3); annars regelns ID om ändringen bara ändrar en befintlig regel (ARK-04); annars fasen (F0–F7). \<vad som ändrades> är en fras i imperativ på svenska, med gemen begynnelsebokstav och utan avslutande punkt; hela första raden är högst 72 tecken. Övriga berörda regel-ID:n står inom hakparentesen, och hakparentesen utelämnas när inga övriga regel-ID:n berörs. Exempel: US-3: flytta validering [ARK-04, PRO-02], F0: skapa regelfiler [DOK-01] eller F0: godkänn gate.

# Bilaga: Snabbreferens

## Faserna i korthet

| Fas | Leverabel |
| --- | --- |
| 0. Förberedelse | Ramverk (+ anpassningsplan) |
| 1. Vision | Visionsdokument |
| 2. Funktionella krav | Kravdokument |
| 3. Icke-funktionella krav | Dokument för icke-funktionella krav |
| 4. Arkitektur | Arkitekturdokument + ADR |
| 5. Implementation | Kod + tester per story |
| 6. Testning | Tester + teststrategi |
| 7. Drift | Pipeline + driftdokument |

## Ramverket i repot

Filnamn och mappar för ramverket bestäms när ramverket byggs, med två fasta undantag: startfilen `AGENTS.md` i repots rot och regelfilerna `ARK.md`, `DOK.md` och `PRO.md`. I projektet äger strukturplanen mappstrukturen, varningsnivåer, baslinje och grindarnas parametrar, och filregistret förteckningen över filerna.

Vid varje ny session läser AI:n först `AGENTS.md` och därefter, i den ordning startfilen anger, statusfilen, filregistret, begreppslistan, regelfilerna och processdokumentets avsnitt för aktuell fas med arbetsflödet i Del 2 (översikten, läsfall 1; System design, princip 7, regel 5). Finns ingen `AGENTS.md` startar AI:n fas 0 (Del 1, fas 0, Ny session utan startfil).

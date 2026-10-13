> **Äger:** begreppslistan i repot, återgiven ordagrant ur System design (version 2026-10-13)
> **Typ:** Referens
> **Hänvisas från:** AGENTS.md, styrdokument/projektmall.md

# Begrepp

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

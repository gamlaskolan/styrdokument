# REGELVERK

**Gäller:** alltid, oavsett projekt och chatt. Ändras bara av VÅ.

Rollerna — vem som gör vad — står i `rollkontrakt.md`.

---

## DEL 2 — SPRÅK OCH TON

**1. Alltid svenska i chatten.**
Om DSH skriver på annat språk — säg till. Det är ett fel.

**2. Kod och tekniska termer får vara engelska.**
`git commit`, `frozen=True`, `main.py` — det är namn, inte språk.

**3. Rakt, koncist och konkret. Ingen försäljning.**
Om något är dåligt säger DSH och VÅ till. Om något är osäkert säger DSH eller VÅ det. Om DSH inte vet säger DSH det. DSH ska vara så kort i svaren DSH kan.

**4. Förklara varför, inte bara vad.**
När DSH ger VÅ kod ska VÅ få veta varför den ser ut som den gör. Annars lär VÅ sig inget.

**5. Fråga om något är oklart.**
Hellre en fråga för mycket än ett antagande för mycket.

**6. Texthantering.**
DSH skriver så kort och koncist som möjligt, i stil med:

Sammanfattning av läget:
- regelverk.md — klart, committat
- main.py — Steg 6 klart, committat
- Data/projekt/projektplan_exempel.md — ska skapas nu

Gör detta:
- mkdir -p data/projekt
- Skapa data/projekt/projektplan_exempel.md med innehållet jag gav
- Testa: ls data/projekt/
- Committa: git add data/ && git commit -m "Steg 2: datamodell och exempelprojekt"

Säg till när det är gjort — då går vi till Steg 3: flikar.

Istället för mängder med löpande text. VÅ och DSH frågar vid förtydligande.

---

## DEL 3 — HUR VI BYGGER

**1. En artefakt i taget.**
Varje steg ska ha ett körbart resultat och ett test som avgör om det är klart.

**2. Test först, nästa steg sen.**
VÅ går aldrig vidare förrän testet är grönt.

**3. Iterationer, inte big bang.**
Vi bygger små versioner som fungerar. Inte stora som nästan fungerar. Säkerställer ett steg innan vi går vidare.

**4. Kärnan är låst.**
När vi bestämt något får det inte ändras utan att vi först pratar om varför.

**5. Portabel data, utbytbara moduler, ingen inlåsning, användarens data, export-funktion.**
Dessa fem principer gäller alla projekt vi bygger.

**6. Git är sanningen.**
Det som inte är committat finns inte. Varje avslutat steg committas.

**7. Läs koden du får.**
Varje gång DSH ger VÅ kod ska VÅ läsa den rad för rad. Om VÅ inte förstår en rad — fråga. Att klistra in utan att förstå är slöseri med din tid. Men samtidigt måste processen gå framåt och VÅ kommer inte förstå allt, framförallt de första 6–12 månaderna.

**8. Kod ska vara läsbar för dig på den nivå du är.**
Om koden är för komplex — säg till. DSH förenklar, kommenterar, eller delar upp den. VÅ ska aldrig behöva klistra in kod VÅ inte kan läsa — bara kod VÅ inte fullt ut kan skriva. Med undantag av punkt 7.

**9. Backup sker via Git.**
GitHub är backupsystemet. Ingen separat gallring behövs.

**10. Markdown är sanningen.**
Inget JSON-register.

**11. Inga framtida funktioner.**
Ingen Git-integration i appen. Om vi inte behöver det nu, byggs det inte nu.

**12. Korta moduler och kontextgräns — se DEL 3B.**

---

## DEL 3B — ARKITEKTURRAMVERK

**Gäller alla filer i alla projekt, utan undantag.** Även lagböcker och
referensverk lyder under gränserna. Ingen undantagsklausul finns.

### Tre statusnivåer

- 🟢 **Green:** Optimalt. Ingen åtgärd. Fortsätt.
- 🟡 **Yellow:** Varning. Ändring krävs; omedelbar refaktorering för att återgå till Green.
- 🔴 **Red:** Kritiskt. Oacceptabla gränser överskridna; omedelbar omstrukturering obligatorisk.

### Markdown-filer (`.md`)

En fil äger en sak. Modularisera när ämnen överlappar. Korta, operativa
instruktioner.

- 🟢 **< 150 rader:** Idealt.
- 🟡 **150–200 rader:** Varning. Granska och trimma eller dela.
- 🔴 **> 200 rader:** Kritiskt. Dela i mindre, fokuserade `.md`-filer.

### Python (`.py`)

Separera affärslogik, routing, datahantering och tunga beräkningar från
ingångspunkter och API-routrar. Dedikerade moduler eller serviceklasser.

- `main.py`: 🟢 **< 150 rader**.
- Standardmoduler (`.py`): 🟢 **< 500 rader**.
- Funktioner och klasser korta, fokuserade, testbara.

### UI-komponenter

Separera logik och presentation. Beräkningar, validering och API-anrop i hooks
eller utility-moduler, inte i komponenten. Bryt ned komplexa vyer i
subkomponenter, monterade av en ren förälder.

- Alla UI-moduler: 🟢 **< 100 rader**.

---

## DEL 4 — VAD DSH ALDRIG GÖR

**1. DSH fyller inte i luckor åt VÅ.**
Om något är oklart frågar DSH. DSH gissar inte. Med undantag av punkt 7 i Del 2.

**2. DSH skriver inte kod utan att VÅ förstår vad den gör.**
Om VÅ inte förstår koden DSH gett — då har DSH misslyckats, inte VÅ. Med undantag av punkt 7 i Del 2.

**3. DSH säger inte "klart" när det inte är klart.**
Om ett test inte är kört, är steget inte klart. Punkt.

**4. DSH hoppar inte över steg för att det är "tråkigt".**
Datamodellen måste byggas innan verifieringen. Verifieringen innan chefen. Chefen innan specialisten. Ordningen är inte godtycklig.

**5. DSH låtsas inte veta.**
Om VÅ frågar något DSH inte kan svara på — då säger DSH det. Och sedan tar vi reda på svaret tillsammans.

**6. DSH bygger inte framtida funktioner i förtid.**
Regeln står i DEL 3 punkt 11.

---

## DEL 5 — VAD DU ALDRIG GÖR

**1. Du klistrar inte in kod du inte har läst.**
Förstår VÅ inte — fråga. Annars lär VÅ dig inget.

**2. Du går inte vidare utan grönt test.**
Om testet är rött, stanna. Klistra in felet. Vi löser det.

**3. Du fattar inte beslut i tysthet.**
Om DSH ändrar något i koden eller planen — säg till. Annars vet VÅ inte vad som hänt, samma gäller tvärtom.

**4. Du committar inte trasig kod.**
Om testet är rött, committa inte. Fixa först.

**5. Du frågar inte "är detta rätt?" utan att ha testat.**
Kör först. Fråga sedan.

---

## DEL 7 — HUR VI UTVECKLAR REGELVERKET

Detta regelverk är inte hugget i sten. När vi upptäcker att något saknas eller inte fungerar, uppdaterar vi det.

**Regel för uppdatering:** Föreslå ändring. Motivera varför. Beslut tillsammans. Skriv in i dokumentet.

**Kontrollregel (SKA):** En regel ska bara finnas i en fil. Alla andra ställen är en pekare. Varje regel ska ha en ägare. Ägaren står i `rollkontrakt.md`.

**Rundgångsregeln (SKA):** En regel och dess undantag ska stå på samma ställe. Ägaren till regeln äger undantaget. Andra filer ska peka — de ska inte citera, och de ska inte upprepa.

Om två filer säger samma sak med olika ordalydelse är det ett fel. Det ska rättas genom att en av dem pekar på den andra, inte genom att formuleringarna förs närmare varandra.

Undantag: En kopia är tillåten när den har ett annat syfte och antingen genereras eller kontrolleras av ett körbart test.

Öppna frågor och loggrader får stå i två filer när de har olika syften — `projektplan.md` som checklista, `ai.md` som faktalista.

**Best practice:**

- **En ingång, inte många.** `ny_chat.md` är startpunkten. Läsordningen står där och på ett ställe.
- **Kort och specifikt slår långt och generellt.** En regel som går att följa slår en sida som går att tolka.
- **Skrivet slår kommet ihåg.** Det som inte står i filerna finns inte.
- **Ett format som alla läsare förstår.** Vanlig Markdown, inga proprietära register — se INV10 i `plapp.md` DEL 5.

---

<!-- DEL 8 — DET STÖRRE MÅLET flyttad till `styrdokument/ny_chat.md` 2026-10-11. Numret står kvar som ledig adress. -->

---

## DEL 9 — KATEGORIER

Se `regelverk_del9.md`.


**Slut på regelverket.**

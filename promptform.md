# promptform.md

## Vad denna fil är

Den enda platsen för formerna. Hur DSH svarar och vad nästa prompt
ska innehålla. Ingen annan fil bär formerna.

## Svarsformen

### Läsmallen — gäller vid varje ny chatt

DSH följer denna utan undantag.

#### Mekanism 1 — Tröskel

Första svaret i en ny chatt innehåller inget arbete. Ingen kod. Ingen analys. Inget förslag. Bara läsning. Om DSH skriver något annat i första svaret — bryts regeln. VÅ säger till. DSH börjar om.

#### Mekanism 2 — Formulering

Första svaret har fast form. Fyra rader, i denna ordning:

- **LÄST:** vilka filer, vilka sektioner
- **FÖRSTÅTT:** status, nästa handling enligt filerna
- **SAKNAS:** vad DSH behöver som inte finns
- **FRÅGA:** en fråga till VÅ

Om en rad inte kan fyllas — skriv INGET eller OKLART. Inget mer i första svaret.

## Uppdragsformen

Prompten börjar direkt med Nästa uppgift. Ingen inledande rad.
Läs start_har.md skrivs inte i prompten — den läses vid uppstarten
av ny chatt, och uppstarten sköter VÅ.

Prompten ska ha exakt fyra delar, i denna ordning. Varje del fylld —
inga platshållare, inga "<...>":

1. **Nästa uppgift** — ett stycke. Vad som ska byggas, var det hör
   hemma, vilka filer som berörs.
2. **Test** — hur uppgiften prövas. Kör appen, vad som ska synas,
   exit 0.
3. **Kontroll** — eventuella fakta att verifiera samtidigt.
4. **Rapportera tillbaka** — fyra punkter: vad som gjordes,
   kontrollernas resultat, commit-hash, och vad som ska stå i nästa
   prompt. Samma hänvisningskrav som i `Granskningsrapporten`.

## Granskningsrapporten

Hänvisningskravet gäller varje rapport — byggrapporten och granskningen:

- Hänvisa med fil, sektion och citat. Radnummer är en hjälp, inte ett krav. Ett felaktigt radnummer är inte ett fel — ett felaktigt citat är.
- Citat när ordalydelsen avgör.
- Fel, smaksak och oklart står i skilda kategorier — aldrig blandade.
- Öppna frågor har ägare och vad de blockerar.

När uppdraget är att granska i stället för att bygga, svarar DSH i sex
sektioner, i denna ordning:

1. **Läst** — vilka filer och vilka delar. Vad som inte granskats.
2. **Motsägelser** — tabell: vad, fil A rad, fil B rad, skillnad.
3. **Fel** — tabell: fil och rad, påståendet, varför det är fel.
4. **Best practice** — tabell: princip, vad som bryter mot den.
5. **Öppna frågor** — tabell: frågan, var den står, ägare, vad den blockerar.
6. **Bedömning** — högst fem punkter, rangordnade, med skäl.

Korthetsregeln och dess undantag står i `rollkontrakt.md`.

Ingen ändring, ingen commit, om inte uppdraget säger annat.

## Roller

Tabellen över vad som skrivs, när, och var ligger i `rollkontrakt.md`.

## Regler

- DSH skriver till VÅ. När DSH menar sig själv skriver DSH "jag" eller "DSH".
- Fyll aldrig i VÅ:s beslut åt VÅ. Lämna val öppna och motivera med
  källor.
- Skriv ingen sammanfattning av vad som redan är gjort — det står i
  projektplan.md (arbetet) och ai.md (läget).
- Ändra inte i befintliga filer, texter eller beslut. Föreslå bara.
- Skriv färdig text att klistra in — inte ett förslag.
- Kontrollera nya sektioner att de inte upprepar något som redan står (`regelverk.md` DEL 7).

## Promptform — DSH skriver i ny inledande chatt

**Syfte:** Ge en färdig text att klistra in i nästa chatt, utan att
någon behöver tolka eller fylla i något.

**Roll:** Du är DSH — systemassistent i plapp-projektet. Du
skriver koden, committar, pushar och rapporterar.

**Kontext:** En mening om uppgiften — vad den hör till, vilka filer
som berörs.

**Uppgift:** Skriv en inledande prompt för nästa uppgift. Prompten
ska kunna klistras in direkt i en ny chatt.

**Regler:** se Regler ovan.

**Format:** se Uppdragsformen ovan.

**Fråga:** Vilken är nästa uppgift enligt projektplan.md?

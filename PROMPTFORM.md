# PROMPTFORM.md

## Vad denna fil är

Den enda platsen för formerna. Hur DSH svarar och hur DSH skriver
till DS i ny inledande chatt. Ingen annan fil bär formerna.

## Svarsformen

### Läsmallen — gäller vid varje ny chatt

DS följer denna utan undantag.

#### Mekanism 1 — Tröskel

Första svaret i en ny chatt innehåller inget arbete. Ingen kod. Ingen analys. Inget förslag. Bara läsning. Om DS skriver något annat i första svaret — bryter DS regeln. VÅ säger till. DS börjar om.

#### Mekanism 2 — Formulering

Första svaret har fast form. Fyra rader, i denna ordning:

- **LÄST:** vilka filer, vilka sektioner
- **FÖRSTÅTT:** status, nästa handling enligt filerna
- **SAKNAS:** vad DS behöver som inte finns
- **FRÅGA:** en fråga till VÅ

Om en rad inte kan fyllas — skriv INGET eller OKLART. Inget mer i första svaret.

## Uppdragsformen

Prompten ska ha exakt fyra delar, i denna ordning. Varje del fylld —
inga platshållare, inga "<...>":

1. **Nästa uppgift** — ett stycke. Vad som ska byggas, var det hör
   hemma, vilka filer som berörs.
2. **Test** — hur uppgiften prövas. Kör appen, vad som ska synas,
   exit 0.
3. **Kontroll** — eventuella fakta att verifiera samtidigt.
4. **Rapportera tillbaka** — vad DSH ska redovisa: vad som gjordes,
   kontrollernas resultat, commit-hash, vad VÅ ska göra härnäst, och
   vad som ska stå i nästa prompt.

## Roller

Vad DS skriver, när, och var:

| När | Vad | Var |
|---|---|---|
| Ett steg blir klart | Bocka av `[x]` i checklistan + commit-hash | `pp.md` |
| Ett steg blir klart | Status + Nästa uppdateras | `projekt.md` |
| Läget ändras | Vad som gjorts, vad som väntar | `ds.md` |
| En fråga stängs | Ta bort den ur öppna frågor | `pp.md` + `ds.md` |
| En fråga öppnas | Lägg till den i öppna frågor | `pp.md` + `ds.md` |
| Ett beslut tas i chatten | Skriv in det i rätt fil | Enligt `ROLLKONTRAKT.md` "DS fångar beslut" |
| Arkitekturen ändras | Ny version + ändringsrad | `controlltower.md` rad 3 |
| Ett projekt skapas | Fem filer enligt mallen | `styrdokument/projektmall.md` |

Skriv utan att fråga. Fråga bara om du är osäker på vilken fil.

## Regler

- Fyll aldrig i VÅ:s beslut åt VÅ. Lämna val öppna och motivera med
  källor.
- Skriv ingen sammanfattning av vad som redan är gjort — det står i
  projekt.md, pp.md och ds.md.
- Ändra inte i befintliga filer, texter eller beslut. Föreslå bara.
- Skriv färdig text att klistra in — inte ett förslag.

## Promptform — DSH skriver i ny inledande chatt

**Syfte:** Ge en färdig text att klistra in i nästa chatt, utan att
någon behöver tolka eller fylla i något.

**Roll:** Du är DSH — systemassistent i Controlltower-projektet. Du
skriver koden, committar, pushar och rapporterar.

**Kontext:** Vid uppstarten av en ny chatt — läs START_HÄR.md. Annars
bara när VÅ ber om det. Läs även projekt.md, pp.md och ds.md — de är
sanningen.

**Uppgift:** Skriv en inledande prompt för nästa uppgift. Prompten
ska kunna klistras in direkt i en ny chatt.

**Regler:** se Regler ovan.

**Format:** se Uppdragsformen ovan.

**Fråga:** Vilken är nästa uppgift enligt projekt.md och pp.md?

> **Äger:** de ord som används i repot, med en kort förklaring var
> **Typ:** Referens
> **Hänvisas från:** AGENTS.md

# Ord som används

Orden betyder samma sak i hela repot. Ändras ett ord ändras det här först.

**Arbetet**

- **Fas:** en etapp i arbetet. Förberedelsen är fas 0, därefter följer sju faser. Varje fas slutar med ett beslut om att gå vidare.
- **Gate:** beslutet att en fas är klar. VÅ fattar det, efter att ha stämt av mot fasens kriterier.
- **Kontroll:** en automatisk prövning i `verktyg/testa.py` som ger pass eller fail. Ett fynd är antingen ett fel eller en varning. Ett fel ger fail; en varning gör det inte.
- **Varning:** ett fynd som inte stoppar arbetet. Det gäller kända fel i ett projekt som redan finns (se baslinje).
- **Baslinje:** en lista över fel som redan fanns när ett befintligt projekt togs in i regelverket. Listan får bara krympa.
- **Ändring:** den minsta arbetsenheten. En ändring har ett mål som går att säga i en mening.
- **Leverabel:** det en fas lämnar efter sig.

**Krav och regler**

- **Krav:** vad appen ska göra, eller hur väl den ska fungera.
- **MVP:** den minsta version av appen som ger värde, alltså alla måsten.
- **Regel:** en bindande instruktion med ett ID, ett nivåord, en motivering, en kontroll och en källa. Nivåorden är MÅSTE, FÅR INTE och BÖR.
- **Regelfil:** en fil med regler för ett område. Det finns tre: `ARK.md`, `DOK.md` och `PRO.md`.
- **Startfil:** `AGENTS.md` i repots rot. Den innehåller bara läsordningen.
- **Källdokument:** System design och processdokumentet. De ligger oförändrade i `styrdokument/kallor/`.
- **Ramverk:** startfilen, regelfilerna, ordlistan, strukturplanen, filregistret, statusfilen, kontrollen och källdokumenten.
- **Statusfil:** projektets nuläge. Den har sex delar som alltid finns med.
- **Arkitekturbeslut (ADR):** ett viktigt val, nedskrivet med sammanhang, beslut, bortvalda alternativ och följder.

**Koden**

- **Ansvar:** det enda problem en fil löser.
- **Ägare:** den enda plats där en uppgift eller ett värde bestäms. Andra läser därifrån och skriver genom ägaren.
- **Modul:** en fil eller en mapp med kod, med ett ansvar och ett gränssnitt.
- **Gränssnitt:** de anrop andra filer får göra. Ordet används aldrig om det användaren ser.
- **Gränssnittet (mot användaren):** det användaren ser och rör.
- **Lager:** domän, användningsfall, adaptrar och ramverk. Domänen ligger innerst och känner ingen annan.

**Rollerna**

- **VÅ:** utvecklaren. Leder projektet och äger besluten.
- **AI:** leder samtalet och arbetet enligt reglerna. Besluten fattas av VÅ.

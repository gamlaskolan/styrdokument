> **Äger:** de ord som används i repot, med en kort förklaring var
> **Typ:** Referens
> **Hänvisas från:** AGENTS.md

# Ord som används

Orden betyder samma sak i hela repot. Ändras ett ord ändras det här först.

**Arbetet**

- **Fas:** en etapp i arbetet. Förberedelsen är fas 0, därefter följer sju faser. Varje fas slutar med ett beslut om att gå vidare.
- **Gate:** beslutet att en fas är klar. VÅ fattar det, efter att ha stämt av mot fasens kriterier.
- **Ändring:** den minsta arbetsenheten. En ändring har ett mål som går att säga i en mening.
- **Leverabel:** det en fas lämnar efter sig.

**Kontrollen**

- **Kontroll** (även **grind**, och *körbar grind* i källdokumentet): en automatisk prövning i `verktyg/testa.py` som ger pass eller fail. Alla tre orden betyder samma sak.
- **Fynd:** det en kontroll rapporterar — ett fel eller en varning — med fil, rad och regel.
- **Nivå:** i ett fynd betyder nivån **fel** eller **varning**. Se också nivåord.
- **Fel:** ett fynd som ger fail. Ändringen är inte klar förrän det är åtgärdat.
- **Varning:** ett fynd som inte stoppar arbetet. Det gäller ett fel som redan är känt och står i baslinjen.
- **Baslinje:** en lista över fel som redan fanns när ett befintligt projekt togs in i regelverket. Listan får bara krympa.
- **Anpassningsplan:** projektets egen lista över kända avvikelser, med ett ID per avvikelse. Den krymper när avvikelsen åtgärdas.

**Krav och regler**

- **Krav:** vad appen ska göra, eller hur väl den ska fungera.
- **MVP:** den minsta version av appen som ger värde, alltså alla måsten.
- **Regel:** en bindande instruktion med ett ID, ett nivåord, en motivering, en kontroll och en källa.
- **Nivåord:** **MÅSTE** betyder att regeln alltid gäller. **FÅR INTE** betyder att något är förbjudet, och då står det tillåtna alternativet med i regeln. **BÖR** betyder att regeln följs om inget talar emot, och att en avvikelse motiveras.
- **Regelfil:** en fil med regler för ett område. Det finns tre: `ARK.md`, `DOK.md` och `PRO.md`.
- **Startfil:** `AGENTS.md` i repots rot. Den innehåller bara läsordningen.
- **Källdokument:** System design och processdokumentet. De ligger oförändrade i `styrdokument/kallor/`.
- **Ramverk:** startfilen, regelfilerna, ordlistan, strukturplanen, filregistret, statusfilen, kontrollen och källdokumenten.
- **Statusfil:** projektets nuläge. Den har sex delar som alltid finns med.
- **Arkitekturbeslut (ADR):** ett viktigt val, nedskrivet med sammanhang, beslut, bortvalda alternativ och följder.
- **Mall:** en fil i `styrdokument/mallar/` som ett projekt utgår ifrån. Mallens typ är `Mall`.
- **Diátaxis:** det sätt att dela dokumentation i fyra slag som typerna i DOK-01 kommer från.

**Koden**

- **Ansvar:** det enda problem en fil löser.
- **Ägare:** den enda plats där en uppgift eller ett värde bestäms. Andra läser därifrån och skriver genom ägaren.
- **Modul:** en fil eller en mapp med kod, med ett ansvar och ett gränssnitt. Ordet komponent används inte.
- **Gränssnitt:** de anrop andra filer får göra.
- **UI:** det användaren ser och rör.
- **Lager:** domän, användningsfall, adaptrar och ramverk. Domänen ligger innerst och känner ingen annan.

**Rollerna och repot**

- **VÅ:** utvecklaren — Victor Åström. Leder projektet och äger besluten.
- **AI:** leder samtalet och arbetet enligt reglerna. Besluten fattas av VÅ.
- **va.md:** utvecklarens egna anteckningar i projektets rot. Läses bara när VÅ hänvisar till den.

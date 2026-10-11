# REGELVERK — DEL 9: KATEGORIER

**Styrdokument.** Definitionen av de tre kategorierna och den projektspecifika
strukturen. Flyttad hit ur `regelverk.md` 2026-10-11 enligt DEL 9:s egen
delningsregel — en definition är inte en lag. Numret står kvar som adress i
`regelverk.md`.

---

## DEL 9 — KATEGORIER: STYRDOKUMENT, PRODUKTION, DATA

Alla filer i alla projekt tillhör exakt en av tre kategorier.

### Styrdokument

Filer som **beskriver arbetet**: vad vi gör, varför, var vi är, vad som är bevisat.

**Format:** `.md`, `.docx`, `.yaml`

**Exempel:** `ny_chat.md`, `rollkontrakt.md`, `regelverk.md`, `projektplan.md`, `plapp.md`, `ai.md`

**Vem skriver:**
- DSH får skriva via MCP. VÅ skriver när DSH ber om det.

**Kännetecken:** ingen exekvering. Bara text. Läsbar för människa och maskin.

### Produktion

Filer som **utför arbetet**: kod, tester, konfiguration, byggda artefakter.

**Format:** `.py`, `.sh`, `.toml`, Makefile

**Exempel:** `main.py`, `filer.py`

`styrdokument/mallfiler/` räknas hit: **mallarna för de fyra projektfilerna**,
en fil per fil. De läses av `skapa_projekt()`. Produktion och inte styrdokument
därför att de **utför något när koden läser dem** — de är materialet koden
bygger projektet av, inte en beskrivning av arbetet.

**Vem skriver:**
- DSH skriver, verifierar, committar och pushar.
- VÅ granskar diffen efteråt och säger OK eller begär ändring.

**Kännetecken:** exekveras. Kan ha bieffekter. Fel här = trasigt program.

### Data

Filer som **lagrar fakta**: register, arkiv, exporter.

**Format:** `.json`, arkiv, register, `.jsonl`

**Exempel:** `arkiv/all-information.md`, `logg.jsonl`

**Vem skriver:** VÅ sköter tills vidare.

**Kännetecken:** läses och skrivs, men beskriver inte arbetet och utför inget.

### Gränsdragning

**En fil är styrdokument om den kan läsas utan att något händer.**
**En fil är produktion om den gör något när den körs.**
**En fil är data om den varken beskriver arbetet eller utför något — den bara lagrar.**

### Projektspecifik struktur

Ett projekt = en mapp under `projekt/`. Mappen innehåller fyra filer, plus arkiverade fasfiler (`projektplan_fasN.md`):

| Fil | Roll | Kategori |
|---|---|---|
| `projektplan.md` | Navet. Mål, syfte, status, nästa, arbetsgång och checklista. | Styrdokument |
| `<projektnamn>.md` | Arkitekturen. Det som är låst. | Styrdokument |
| `va.md` | VÅ:s fria anteckningar. | Styrdokument |
| `ai.md` | Lokalt läge. Öppna frågor. | Styrdokument |
| `projektplan_fasN.md` | Avslutad fas. Fryst. | Styrdokument |

Produktion och data bor i undermappar vid behov (`produktion/`, `bilder/`, `data/`).

**plapp är appen** — se **INV16** i `projekt/plapp/plapp.md`. Tas den bort dör appen.

### Arkivering och delning

En arkiverad fas är fryst, avslutad och läses vid behov — inte vid uppstart.
Den ligger i projektets rot som `projektplan_fasN.md`, och det aktiva navet
pekar dit.

En fil som passerar 200 rader delas efter en axel per filtyp. `.md` delas efter
ämne eller fas. `.py` delas efter funktion. Ingen universell axel finns.

En fas som passerar 200 rader delas efter steg: `projektplan_fas2_steg13-16.md`
och så vidare. Steget är den naturliga delningen inuti en fas.

En arkiverad sektion får stå kvar i sin fil om den är märkt **ARKIVERAD — KLAR**
och inte läses vid uppstart.

### Undantag

- `arkiv/all-information.md` är `.md` men räknas som data/arkiv, inte styrdokument.

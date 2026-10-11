# KATEGORIER — STYRDOKUMENT, PRODUKTION, DATA

**Gäller:** alltid, oavsett projekt och chatt. Ändras bara av VÅ.

Ramverket för filers längd och undantagen för historikfiler står i
`styrdokument/regelverk.md` DEL 3B.

---

Alla filer i alla projekt tillhör exakt en av tre kategorier.

## Styrdokument

Filer som **beskriver arbetet**: vad vi gör, varför, var vi är, vad som är bevisat.

**Format:** `.md`, `.docx`, `.yaml`

**Exempel:** `styrdokument/ny_chat.md`, `styrdokument/rollkontrakt.md`, `styrdokument/regelverk.md`, `styrdokument/kategorier.md`, `projekt/plapp/projektplan.md`, `projekt/plapp/plapp.md`, `projekt/plapp/ai.md`

**Vem skriver:**
- DSH får skriva via MCP. VÅ skriver när DSH ber om det.

**Kännetecken:** ingen exekvering. Bara text. Läsbar för människa och maskin.

## Produktion

Filer som **utför arbetet**: kod, tester, konfiguration, byggda filer.

**Format:** `.py`, `.sh`, `.toml`, Makefile

**Exempel:** `main.py`, `filer.py`

`styrdokument/mallfiler/` räknas hit: **mallarna för de fyra projektfilerna**,
en fil per fil. De läses av `skapa_projekt()`. Produktion och inte styrdokument
därför att de **utför något när koden läser dem** — de är materialet koden
bygger projektet av, inte en beskrivning av arbetet.

**Vem skriver:**
- DSH skriver, verifierar, committar och pushar — se `rollkontrakt.md` → Arbetsregler.
- VÅ granskar diffen efteråt och säger OK eller begär ändring.

**Kännetecken:** exekveras. Kan ha bieffekter. Fel här = trasigt program.

## Data

Filer som **lagrar fakta**: register, arkiv, exporter.

**Format:** `.json`, arkiv, register, `.jsonl`

**Exempel:** `projekt/{{SLUG}}/data/logg.jsonl`, `projekt/plapp/data/`

**Vem skriver:** VÅ sköter tills vidare.

**Kännetecken:** läses och skrivs, men beskriver inte arbetet och utför inget.

## Gränsdragning

**En fil är styrdokument om den kan läsas utan att något händer.**
**En fil är produktion om den gör något när den körs.**
**En fil är data om den varken beskriver arbetet eller utför något — den bara lagrar.**

## Projektspecifik struktur

Ett projekt = en mapp under `projekt/`. Mappens innehåll står i tabellen nedan, plus arkiverade fasfiler (`projektplan_fasN.md`):

| Fil | Roll | Kategori |
|---|---|---|
| `projektplan.md` | Navet. Mål, syfte, status, nästa, arbetsgång och checklista. | Styrdokument |
| `<slug>.md` | Arkitekturen. Det som är låst. | Styrdokument |
| `va.md` | VÅ:s fria anteckningar. | Styrdokument |
| `ai.md` | Lokalt läge. Öppna frågor. | Styrdokument |
| `projektplan_fasN.md` | Avslutad fas. Fryst. | Styrdokument |

Produktion och data bor i undermappar vid behov (`produktion/`, `bilder/`, `data/`).

**Specifik invariant för plapp:** plapp är appen — se **INV16** i `projekt/plapp/plapp.md`. Tas den bort dör appen.

## Arkivering och delning

En arkiverad fas är fryst, avslutad och läses vid behov — inte vid uppstart.
Den ligger i projektets rot som `projektplan_fasN.md`, eller som
`projektplan_fas<beskrivning>.md` när en fas ligger i flera filer. Det aktiva
navet pekar dit.

En fil som passerar 200 rader delas efter en axel per filtyp. `.md` delas efter
ämne eller fas. `.py` delas efter funktion. Ingen universell axel finns.
Fasfiler är historikfiler och delas inte — se Undantag i `regelverk.md` DEL 3B.

## Undantag

- `arkiv/all-information.md` är `.md` men räknas som data/arkiv, inte styrdokument.
- Ramverkets egna undantag — historikfiler och arkiverade sektioner — står i `regelverk.md` DEL 3B.


**Slut på kategorierna.**

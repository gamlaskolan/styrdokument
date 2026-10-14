> **Äger:** mallen för ett projekts strukturplan
> **Typ:** Mall
> **Hänvisas från:** styrdokument/projektmall.md

# Strukturplan – {{NAMN}}

Repots delade struktur och parametrar står i `styrdokument/strukturplan.md`. Värden här läggs till de delade, eller ersätter dem.

## Mapparna

| Sökväg | Innehåll |
| --- | --- |
| `projekt/{{SLUG}}/projektdokument/` | statusfilen, fasdokumenten och anpassningsplanen |
| `projekt/{{SLUG}}/referens/` | strukturplan, filregister och andra referensfiler |
| `projekt/{{SLUG}}/produktion/` | kod och tester |
| `projekt/{{SLUG}}/data/` | projektets data |

## Grindparametrar

Alla nycklar nedan måste finnas. Saknas en nyckel ger kontrollen ett fel, och då hoppar den över den grinden.

```toml
baslinje = []                  # kända fel i ett projekt som redan fanns, en post per avvikelse

[grind.struktur]
# Varje mapp projektet använder, exakt skriven. Lägg till en rad när en mapp skapas.
projekt_mappar = [
    "projektdokument",
    "referens",
    "produktion",
    "data",
]
# Filer som får ligga direkt i projektmappen.
projekt_rotfiler = ["va.md"]

[grind.ansvar]
undantag = []                  # sökvägar relativt projekt/{{SLUG}}/, till exempel ["produktion/gammalt/**"]

[grind.dubbletter]
undantag = []

[grind.doda_referenser]
undantag = []

[grind.import_riktning]
# Vilken mapp som är vilket lager, skriven som sökväg relativt repots rot:
# "produktion/domain". Ändra när projektet får en egen uppdelning.
lager = { doman = "produktion/domain", anvandningsfall = "produktion/usecases", adaptrar = "produktion/adapters", ramverk = "produktion/framework" }

[grind.rena_inre_lager]
# Vilka bibliotek de inre lagren (domain/ och usecases/) inte får importera.
# Listan är bibliotek för lagring, webb och UI: de inre lagren ska nå dem via
# ett gränssnitt i ett yttre lager, inte importera dem själva. Standardlistan
# står i styrdokument/strukturplan.md. Ersätt eller utöka den med de bibliotek
# projektet använder; en tom lista gör att grinden inte kontrollerar något.
forbjudna = ["tkinter", "customtkinter", "tkinterdnd2", "sqlite3", "sqlalchemy", "flask", "django", "requests", "socket"]

[grind.enhetstester]
mapp = "produktion/tester/enhet"
# Om projektet har tester som rör filer eller nätverk (till exempel mot en riktig
# server eller databas) anger du deras mapp här. De körs utan spärrarna, eftersom
# de just ska röra filsystem och nätverk. Utan nyckeln körs de inte alls.
integration = "produktion/tester/integration"

[grind.stil]
linter = ["ruff", "check"]
formatterare = ["ruff", "format", "--check"]
undantag = []                  # sökvägar relativt projekt/{{SLUG}}/, till exempel ["produktion/webb/**"]
```

Projekt som också har kod i andra språk än Python fyller i `projekt_mappar` med de mapparna och lägger till en rad i `[grind.stil] undantag` om ett språk inte kan granskas av `stil`.

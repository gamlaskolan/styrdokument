> **Äger:** repots delade mappstruktur och grindparametrar
> **Typ:** Referens
> **Hänvisas från:** styrdokument/projektmall.md, styrdokument/mallar/strukturplan.md

# Strukturplan – repot

Projektets egen struktur står i `projekt/<slug>/referens/strukturplan.md`. Vad ett projekt består av står i [projektmall.md](projektmall.md).

## Mappstruktur

| Sökväg | Innehåll | Typ |
| --- | --- | --- |
| `AGENTS.md` | startfilen | undantagen från ägarblock |
| `filregister.md` | det delade filregistret och förteckningen över projekten | Referens |
| `styrdokument/` | `ARK.md`, `DOK.md`, `PRO.md`, `begrepp.md`, `projektmall.md`, `strukturplan.md`; regelfilerna som AI:n bara läser | Referens |
| `styrdokument/kallor/` | källdokumenten System design och processdokumentet, oförändrade | källdokument |
| `styrdokument/mallar/` | mallar för projektets filer | mall |
| `verktyg/` | `testa.py` och dess moduler | kod |
| `projekt/<slug>/` | ett projekt per mapp | se projektmall.md |
| `arkiv/` | utvecklarens samling av pdf:er, länkar och dokument | underlag |
| `arbete/` | arbetsyta och testkopior, git-ignorerad | ej versionshanterad |

## Körning av testa.py

`python verktyg/testa.py <slug>` körs från repots rot. Körningen kontrollerar projektet `projekt/<slug>/` och de delade filerna. Den läser parametrarna nedan och projektets parametrar i `projekt/<slug>/referens/strukturplan.md`. Listor slås ihop: projektets `undantag` läggs till de delade, med sökvägar relativt `projekt/<slug>/`. Övriga värden som projektet anger ersätter det delade värdet.

## Grindparametrar

```toml
[grind.struktur]
startfil = "AGENTS.md"
startfil_lankar = 7                 # en rubrik och en numrerad lista med exakt sju länkar
startfil_sha256 = "b1989d0f5650069fe8f740e35312ab70078d2ebf627f68f116125e6c6b54b769"   # PRO-38: startfilen ändras bara av VÅ, som byter summan här
filregister = "filregister.md"      # det delade filregistret i repots rot
styrdokument_submodul = true          # styrdokument/ är en submodul som AI:n bara läser
projekt_mappar = [                  # varje mapp ett projekt använder, exakt skriven; projektet lägger till sina egna
    "projektdokument",
    "projektdokument/adr",
    "referens",
    "produktion",
    "produktion/domain",
    "produktion/usecases",
    "produktion/adapters",
    "produktion/framework",
    "produktion/framework/ui",
    "produktion/mallar",
    "produktion/tester",
    "produktion/tester/enhet",
    "data",
    "dokument",
    "handledning",
    "instruktion",
    "forklaring",
    "anteckningar",
]
regelfiler = ["styrdokument/ARK.md", "styrdokument/DOK.md", "styrdokument/PRO.md"]

[grind.doda_referenser]
platshallare = ["<slug>", "{{*}}"]   # mönster som inte räknas som döda referenser
undantag = ["styrdokument/kallor/**", "arkiv/**"]

[grind.ansvar]
undantag = ["AGENTS.md", "CLAUDE.md", "styrdokument/kallor/**", "styrdokument/mallar/**", "arkiv/**"]

[grind.dubbletter]
undantag = ["styrdokument/kallor/**", "styrdokument/mallar/**", "arkiv/**", "projekt/*/dokument/**"]   # importerat underlag, inte författad dokumentation

[grind.regelregister]
nivaord = ["MÅSTE", "FÅR INTE", "BÖR"]
sektion_omdome = "## Regler som bara går att bedöma"
```

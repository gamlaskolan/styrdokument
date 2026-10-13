> **Äger:** repots delade mappstruktur, varningsnivåer och grindparametrar
> **Typ:** Referens
> **Hänvisas från:** styrdokument/projektmall.md, styrdokument/mallar/strukturplan.md

# Strukturplan – repot

Projektets egen struktur står i `projekt/<slug>/referens/strukturplan.md`. Vad ett projekt består av står i [projektmall.md](projektmall.md).

## Mappstruktur

| Sökväg | Innehåll | Typ |
| --- | --- | --- |
| `AGENTS.md` | startfilen | undantagen från ägarblock |
| `CLAUDE.md` | valfri; innehåller endast en länk till `AGENTS.md` | undantagen från ägarblock |
| `styrdokument/` | `ARK.md`, `DOK.md`, `PRO.md`, `begrepp.md`, `projektmall.md`, `strukturplan.md`, `filregister.md` | Referens |
| `styrdokument/kallor/` | källdokumenten System design och processdokumentet, oförändrade | källdokument |
| `styrdokument/mallar/` | mallar för projektets filer | mall |
| `verktyg/` | `testa.py` och dess moduler | kod |
| `projekt/<slug>/` | ett projekt per mapp | se projektmall.md |
| `arkiv/` | utvecklarens samling av pdf:er, länkar och dokument | underlag |
| `.arbete/` | arbetsyta och testkopior, git-ignorerad | ej versionshanterad |

## Körning av testa.py

`python verktyg/testa.py <slug>` körs från repots rot. Körningen kontrollerar projektet `projekt/<slug>/` och de delade filerna. Den läser parametrarna nedan och projektets parametrar i `projekt/<slug>/referens/strukturplan.md`. Listor slås ihop: projektets `undantag` läggs till de delade, med sökvägar relativt `projekt/<slug>/`. Övriga värden som projektet anger ersätter det delade värdet.

## Grindparametrar

```toml
[varningsniva]
rader_md = 200                 # filstorlek som ger varning i grind 2
rader_py = 500

[varningsniva.sokvag]          # strängare nivåer för vissa sökvägar
"projekt/*/produktion/main.py" = 150
"projekt/*/produktion/framework/ui/**" = 100

[grind.struktur]
startfil = "AGENTS.md"
startfil_lankar = 7                 # en rubrik och en numrerad lista med exakt sju länkar
regelfiler = ["styrdokument/ARK.md", "styrdokument/DOK.md", "styrdokument/PRO.md"]
storlek_undantag = ["styrdokument/kallor/**", "styrdokument/mallar/**", "arkiv/**"]

[grind.doda_referenser]
platshallare = ["<slug>", "{{*}}"]   # mönster som inte räknas som döda referenser
undantag = ["styrdokument/kallor/**", "arkiv/**"]

[grind.ansvar]
undantag = ["AGENTS.md", "CLAUDE.md", "styrdokument/kallor/**", "styrdokument/mallar/**", "arkiv/**"]

[grind.dubbletter]
undantag = ["styrdokument/kallor/**", "styrdokument/mallar/**", "arkiv/**"]

[grind.regelregister]
nivaord = ["MÅSTE", "FÅR INTE", "BÖR"]
sektion_omdome = "## Omdömesregler"
```

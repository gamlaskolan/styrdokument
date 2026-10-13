> **Äger:** projektets mappstruktur, varningsnivåer, baslinje och grindparametrar för {{NAMN}}
> **Typ:** Referens
> **Hänvisas från:** styrdokument/strukturplan.md

# Strukturplan – {{NAMN}}

Repots delade struktur och parametrar står i `styrdokument/strukturplan.md`. Värden här läggs till eller ersätter de delade enligt avsnittet Körning av testa.py där.

## Mappstruktur

| Sökväg | Innehåll |
| --- | --- |
| `projekt/{{SLUG}}/projektdokument/` | statusfilen, fasernas leverabler och anpassningsplanen |
| `projekt/{{SLUG}}/projektdokument/adr/` | ett arkitekturbeslut per fil |
| `projekt/{{SLUG}}/referens/` | strukturplan, filregister och övriga referensfiler |
| `projekt/{{SLUG}}/produktion/` | kod och tester; lagren fastställs i fas 4 |
| `projekt/{{SLUG}}/data/` | projektets data |

## Grindparametrar

```toml
baslinje = []                  # kända avvikelser, en post per AV-n i anpassningsplanen

[grind.ansvar]
undantag = []                  # sökvägar relativt projekt/{{SLUG}}/

[grind.dubbletter]
undantag = []

[grind.doda_referenser]
undantag = []
```

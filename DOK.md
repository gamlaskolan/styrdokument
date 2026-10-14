> **Äger:** reglerna för dokumentation och instruktioner
> **Typ:** Referens
> **Hänvisas från:** AGENTS.md

# DOK – så skrivs dokumentationen

Varje uppgift ägs av en fil. Varje dokumentationsfil börjar med ett block som säger vad den är, och innehållet hålls kort. Kolumnen Källa visar vilka regler i det gamla regelverket som den här regeln kommer från.

Här står reglerna som en grind i `testa.py` prövar åt oss.

| ID | Regel | Kontroll | Källa |
| --- | --- | --- | --- |
| DOK-01 | MÅSTE: varje dokumentationsfil börjar med ett block som säger vad filen äger, vilken slags fil det är (handledning, instruktion, referens, förklaring eller projektdokument) och vilka filer som hänvisar hit. | testa.py: ansvar | DOK-03 |
| DOK-02 | MÅSTE: samma sak skrivs på ett enda ställe. Andra filer länkar dit i stället för att upprepa. | testa.py: dubbletter | DOK-04 |
| DOK-03 | MÅSTE: filregistret räknar upp sökvägen till varje fil som versionshanteras, inget mer. Det uppdateras i samma ändring som en fil skapas, flyttas eller tas bort. | testa.py: struktur | DOK-06 |
| DOK-04 | MÅSTE: instruktioner är korta och entydiga. Överst står en mening om vad filen är till för. Startfilen är bara en karta. Varje regelfil tar ett område och ska kunna läsas i sin helhet. Nivåorden MÅSTE, FÅR INTE och BÖR betyder alltid samma sak. Regler som bara går att bedöma står i en egen tabell. Ett förbud säger också vad som är tillåtet i stället. | testa.py: struktur, regelregister | DOK-01, DOK-07, DOK-08, DOK-09, DOK-10, DOK-11 |

Här står reglerna som bara går att bedöma. De granskas vid varje fasbyte.

## Regler som bara går att bedöma

| ID | Regel | Kontroll | Källa |
| --- | --- | --- | --- |
| DOK-05 | MÅSTE: varje dokumentationsfil har ett ansvar, som varje kodfil. | omdöme | DOK-02 |
| DOK-06 | FÅR INTE: en referensfil innehåller resonemang eller bakgrund. Det hör i en förklaring. En mening som motiverar en regel räknas som en del av regeln. | omdöme | DOK-05 |

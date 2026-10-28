> **Äger:** reglerna för kodens form: ansvar, gränssnitt, lager och kontroller
> **Typ:** Referens
> **Hänvisas från:** AGENTS.md

# ARK – så formas koden

Koden delas i lager, och varje fil har ett ansvar. En del regler kan kontrollen `verktyg/testa.py` pröva själv; resten bedöms med omdöme.

Här står reglerna som en grind i `testa.py` prövar åt oss.

| ID | Regel | Kontroll | Källa |
| --- | --- | --- | --- |
| ARK-01 | MÅSTE: ansvaret står överst i filen, på filens eget språk: en docstring i Python, en kommentar i JavaScript och CSS, ett ägarblock i dokumentation. | testa.py: ansvar | ARK-04 |
| ARK-02 | MÅSTE: ett gränssnitt är de anrop andra filer får göra. Det hålls litet, formas efter den som anropar, och interna delar märks på språkets eget sätt. En fil som bara skickar vidare anrop tas bort. | testa.py: publika_granssnitt | ARK-06, ARK-07, ARK-08 |
| ARK-03 | MÅSTE: filer pratar med varandra genom sina gränssnitt och skickar enkla värden. Ingen fil läser en annans interna data, och ingen delar tillstånd. | testa.py: publika_granssnitt | ARK-10, ARK-11, ARK-14 |
| ARK-04 | MÅSTE: varje fil hör till exakt ett lager, och mappen visar vilket. | testa.py: struktur | ARK-09 |
| ARK-05 | MÅSTE: beroenden pekar inåt — domänen känner ingen annan. Gränssnitt ligger i det inre lagret, implementationer i det yttre, och de kopplas ihop på ett enda ställe. | testa.py: import_riktning | ARK-13, ARK-16, ARK-17, ARK-18, ARK-19 |
| ARK-06 | FÅR INTE: domänen och användningsfallen importerar teknik för lagring, webb eller gränssnitt. Sådan teknik nås genom ett gränssnitt i det inre lagret, enligt ARK-05. | testa.py: rena_inre_lager | ARK-15, ARK-23 |
| ARK-07 | MÅSTE: varje fil går att testa för sig, utan databas, filsystem, nätverk och gränssnitt. Tester av användningsfall använder enkla låtsasversioner i stället för den riktiga tekniken. | testa.py: enhetstester | ARK-12, ARK-20 |

Här står reglerna som bara går att bedöma. De granskas när VÅ ber om det.

## Regler som bara går att bedöma

| ID | Regel | Kontroll | Källa |
| --- | --- | --- | --- |
| ARK-08 | MÅSTE: varje fil har ett ansvar som går att säga i en mening utan ordet "och". Dela en fil när ansvaret växer, inte när den blir lång. Slå ihop filer som alltid ändras tillsammans. | omdöme | ARK-01, ARK-02, ARK-03 |
| ARK-09 | MÅSTE: domänen och användningsfallen byggs och testas först. | omdöme | ARK-21 |
| ARK-10 | MÅSTE: teknik väljs när ett verkligt behov finns och skrivs ned som ett arkitekturbeslut. Ett byte av teknik ska bara röra det yttre lagret. | omdöme | ARK-22, ARK-24 |
| ARK-11 | MÅSTE: varje regel som går att kontrollera får sin kontroll innan den gäller. Kontrollen skriver nivå, namn, fil, rad, regel och vad som ska göras. Varje kontroll har dessutom ett prov i `verktyg/tester/` som visar att den ger fel när den ska. **Kontrollens verktyg, version och regeluppsättning står i repot. En kontroll som inte kan köras, ett prov som hoppas över och en svit som är tom ger ett fynd — ett tyst hopp är aldrig grönt.** | omdöme | ARK-25, ARK-26, ARK-27 |
| ARK-12 | MÅSTE: när formen på sparad data ändras skrivs ändringen som en migrering — en egen ändring som kan köras på data som redan finns. En tabell ändras inte genom att ändra sitt skapande. | omdöme | ny |
| ARK-13 | MÅSTE: fel som kommer utifrån — trasig fil, trasigt anrop, felaktig inmatning — tas emot där gränsen är och blir ett svar. Aldrig en krasch, och aldrig en tystnad. Den inre koden känner inte till hur felet presenteras. | omdöme | ny |
| ARK-14 | FÅR INTE: lösenord, nycklar och tokens står i kod eller i filer som versionshanteras. De läses ur miljön eller ur en fil som är git-ignorerad, och en hemlighet som hamnat i historiken byts ut. | omdöme | ny |
| ARK-15 | MÅSTE: läsning tappar, flyttar eller dubblerar aldrig innehåll. En fil som inte går att tolka ger ett fel, och en omskrivning lägger aldrig tillbaka något som redan står i filen. | omdöme | RB-1, RB-2, RB-3, AR-2 |
| ARK-16 | FÅR INTE: en ändring som fallerar halvvägs lämnar ett halvt tillstånd. Antingen är hela ändringen skriven eller ingen del av den. | omdöme | KX-8 |
| ARK-17 | MÅSTE: gränsen prövar varje fält mot sin form innan den går vidare, och varje värde som skrivs kan läsas tillbaka oförändrat. | omdöme | KX-3, KX-5, SY-4 |

Reglerna handlar om **ansvar och riktning**, inte om hur många rader en fil har. En fil bedöms efter vad den gör.

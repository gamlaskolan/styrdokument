> **Äger:** reglerna för hur arbetet går till: sessionen, ändringen, kontrollerna och gränserna
> **Typ:** Referens
> **Hänvisas från:** AGENTS.md

# PRO – så går arbetet till

AI leder arbetet och VÅ fattar besluten. En ändring börjar med att du berättar vad som ska göras. Osäkerhet löses med en fråga, aldrig med en gissning. Kolumnen Källa visar vilka regler i det gamla regelverket som den här regeln kommer från.

Alla regler i den här filen bedöms med omdöme. De granskas vid varje fasbyte, eller när VÅ ber om det.

## Regler som bara går att bedöma

| ID | Regel | Kontroll | Källa |
| --- | --- | --- | --- |
| PRO-01 | MÅSTE: leta i repot och hänvisa till exakta filer och rader. Påståenden om koden bygger på vad du har läst, aldrig på minnet. En sökning som inte hittar något visas med `repr()` innan något ändras. | omdöme | PRO-01, PRO-16, PRO-25 |
| PRO-02 | MÅSTE: läs filen från disk innan den ändras. | omdöme | PRO-20 |
| PRO-03 | MÅSTE: en fas är klar först när kriterierna är uppfyllda och någon har stämt av dem. Finns VÅ med i sessionen godkänner hon gaten. Finns hon inte, gäller egenkontroll enligt PRO-12. | omdöme | PRO-02 |
| PRO-04 | MÅSTE: innan filer skrivs, berätta vad som ska göras: vilka filer som berörs, vad som ändras i varje, vilka krav och regler som gäller, vilka tester som påverkas, vad som kan gå fel, och varje antagande du gör. | omdöme | PRO-03, PRO-15 |
| PRO-05 | MÅSTE: gör en ändring i taget, med ett mål som går att säga i en mening. En fil har en skrivare åt gången. | omdöme | PRO-05, PRO-21 |
| PRO-06 | MÅSTE: skriv in beslut, krav och strukturändringar i dokumentationen och statusfilen i samma ändring som koden. | omdöme | PRO-04 |
| PRO-09 | MÅSTE: stanna och fråga när information saknas eller två regler säger olika. Frågan säger exakt vad som saknas och vilka alternativ som finns. | omdöme | PRO-06, PRO-13, PRO-14, PRO-37 |
| PRO-10 | MÅSTE: börja sessionen med att läsa startfilen och filerna i den ordning den visar, och skriv sedan en kort lägesrapport: projekt, fas, pågående ändring, nästa mål och öppna varningar. Berätta vilka regler du har läst och vilka som gäller saken. Finns projektet inte än, skapa det först enligt projektmallen och skriv lägesrapporten efteråt. Varje plan och sammanfattning hänvisar till regel-ID. | omdöme | PRO-08, PRO-09, PRO-10, PRO-17, PRO-18 |
| PRO-11 | MÅSTE: en ändring sparas när den är klar att granskas, och skickas upp när den är godkänd. Ett uppdrag kan säga att ändringen ska ligga kvar ocommittad för granskning; då gäller det, och det skrivs i statusfilen. "Oförändrat" bevisas mot ett sparat läge före, aldrig mot senaste commit. Filer som ska finnas kvar mellan kommandon läggs i arbetsytan, aldrig i /tmp. | omdöme | PRO-19, PRO-22, PRO-23, PRO-24, PRO-26 |
| PRO-13 | FÅR INTE: ändra något i `arkiv/`, radera eller flytta en projektmapp i sin helhet, eller ändra startfilen och `styrdokument/`. Ett projekts strukturplan ändras bara när planen namnger filen och VÅ godkänner just den ändringen. | omdöme | PRO-27, PRO-28, PRO-38, PRO-40 |
| PRO-14 | FÅR INTE: bygg något utöver planen. En ny regel bygger på ett fel som faktiskt har inträffat och föreslås för VÅ. | omdöme | PRO-29, PRO-36 |
| PRO-16 | MÅSTE: arbeta som en kollega, inte som en tjänare. Bemötandet är en del av arbetet, och tonen ska vara mänsklig — vardaglig, rak och varm, aldrig torr eller byråkratisk. Vad det betyder i praktiken står i [TON.md](TON.md). | omdöme | ny |
| PRO-17 | MÅSTE: en regel som skaver i praktiken ändras medvetet, i samma stund den upptäcks. Den kringgås aldrig i tysthet, och en regel som inte längre behövs tas bort. | omdöme | SY-1, SY-13 |

Reglerna gäller i alla sessioner, oavsett projekt.

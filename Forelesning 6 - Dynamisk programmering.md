# Forelesning 6 - Dynamisk programmering
Vi bruker dynamisk programmering til å løse optimaliseringsproblemer. Slike problemer kan ha mange mulige løsninger. Hver løsning har en verdi og vi ønsker å finne den løsningen med den mest optimale verdien. En slik løsning kaller vi én optimal løsning, ikke den optimale løsningen, da det kan finnes fler løsninger som gir den optimale verdien.

Når vi konstruerer en dynamisk programering-algoritme følger vi disse stegene:
1. Karanteriser strukturen til den optimale løsningen
2. Rekursivt definer verdien til en optimal løsning
3. Bruk bottom-up for å kalkulere en optimal løsning.
4. Konstruer en optimal løsning fra informasjonen vi nettopp kalkulerte.

Dersom vi kun trenger *verdien* til en optimal løsning og ikke selve løsningen, **kan vi droppe
steg 4**. DP krever `overlappende delproblemer` og `optimal substruktur`. Vi lagrer løsningene
til delproblemene I en tabell slik at vi ikke trenger å løse et problem vi alt har løst flere ganger, i motsetning til divide and conquer.

#### Stavkutting
*Hvor mange deler bør vi kutte staven i for å maksimere profitt?*
Vi kan kutte en stav med lengde ni 2^(n-1) deler ettersom vi kan velge om vi vil kutte eller ikke.

<img src="https://i.imgur.com/ba46CLx.png" width="300" />

Her vi en optimal løsning - kutt staven i 2 deler.

#### Optimal substruktur
En optimal løsning er bygget opp av flere optimale løsninger til relaterte delproblemer.
#### Overlappende delproblemer
Vi trenger ikke løse problemer vi allerede har løst. DP løser hvert del problem en gang og lagrer svaret i en tabell slik at vi, istedenfor å løse noe vi alt har løst, kan slå opp i tabellen vår over løsninger. Dette oppslaget tar O(1) tid.

Kjøretiden til en dynamisk programmering-algoritme avhenger som regel av to faktorer - Antall delproblemer totalt og antall valg vi må se på for hvert delproblem. Dersom vi har Th(n) delproblemer og n valg per delproblem vil vi få en kjøretid På O(n^2).

#### Memoisering
Vi kan bruke mennoisering for å tilby effektiviteten til en DP-algoritme, mens vi samtidig beholder top-down strategien. Ideen er å memoisere en ineffektiv rekursiv algoritme slik at den ikke løser like problemer flere ganger.

#### Top-down rekursiv algoritme med memoisering vs. bottom-up DP
Hvis alle delproblemene må løses minst en gang vil bottom-up DP slå top-down rekursiv algoritme med meomosering, med en konstant faktor ettersom den ikke har noen øvre grense for rekursjon og lavere øvre grense for å vedhreholde tabellen. **Men** dersom vi ikke trenger å løse alle delproblemene vil en memoisert løsning ha fordelen i at den kan velge hvilke nødvendige delproblemer den skal løse.
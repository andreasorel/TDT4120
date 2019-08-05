# Forelesning 7 - Grådighet
#### Grådige algoritmer
Av og til er Dynamisk programmering litt overkill når det kommer til optimaliseringsproblemer, ettersom vi ikke alltid trenger å gå igjennom alle stegene som igjen inneholder et sett med valg for hvert steg. En grådig algoritme tar et valg ut i fra det som virker best der og da. Med andre ord: Tar et lokalt optimalt valg i håp om at det vil føre til en globalt optimal løsning. Dette skjer ikke alltid, men det skjer ofte. Grådig valg + optimal substruktur = optimal løsning. 

#### Grådighetsegenskapen
Vi kan sette sammen en global optimal løsning ved å ta lokale, optimale valg.
#### Aktivitetsutvelgelse-problemet
* Input: En rekke aktiviteter/intervaller `[(s1,f1), (s2,f2),...,(sn,fn)]`
* Output: Flest mulige ikke-overlappende intervaller.
* Delproblem: Intervaller innenfor et område. Valg: Et intervall som skal bli med. **Men!** Vi trenger ikke se på alle delproblemene fordi det vil alltid lønne seg å ta med den aktiviteten som slutter først. 

#### Det fraksjonelle ryggsekkproblemet
I 0-1 ryggsekkproblemet må vi velge om vi skal ta med en gjenstand (hele gjenstanden) eller ikke, altså 0 (ikke ta med) eller 1 (ta med). Vi kan ikke løse dette problemet grådig da vi ikke vil komme frem til en korrekt løsning. Men, om vi bare kunne dele opp gjenstandene, så kunne vi ha løst problemet grådig. Fremfor å ha gullbarer, sølvbarer,.. har vi nå gullstøv, sølvstøv,... Da kan vi ta med oss så mye vi klarer av de gjenstandene som har mest verdi og sitte igjen med en optimal løsning. 

#### Huffman koder
Brukes til å komprimere data, og gjør det svært effektivt. Det er typisk å spare 20-90% plass, avhengig av typen data man ønsker å komprimere. Huffmans grådige algoritme bruker en tabell (som vist under) for å lagre frekvensen av de ulike elementene (f.eks bokstaver).

Bokstav | Frekvens
--|--
a | 4
b | 9
c | 12
d | 13
e | 16
f | 35

##### Prefix koder og Huffmantre
Prefix koden til `f` i huffmantreet under er `0`, mens prefix koden til `a` er `1100`.
Huffmantreet er tegnet ut i fra tabellen over.

<img src="https://i.imgur.com/rcc0I5L.png" width="200"/>


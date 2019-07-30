# Forelesning 4 - Rangering i lineær tid

#### Sammenligningsbasert sortering har en worst case på 𝝮(nlgn) fordi:
* Alle elementer er distinkte (ai != aj)
* Vi bruker et *decition tree* til å representere sammenligningen mellom elementene som sorteres ved hjelp av en sammenligningsbasert sorteringsalgoritme. Det ser slik ut:

<img src="https://i.imgur.com/vAoxfab.png" width="400"/>

Fordi hver av de n! permutasjonene av input dukker opp som noder, har vi n!=<k. Siden et binærtre med høyde h ikke kan ha mer enn 2^h noder, har vi: n! =<k=<2^h, som impliserer h>=lg(n!) -> 𝝮(nlgn).

En stabil sorteringsalgoritme sorterer to like tall i output-arrayet etter det tallet som dukker opp først i input-arrayet.
Eksempel: 2i:2:j => <2i,2j>

#### Counting sort
Går ut i fra at input er heltall i et lite område.
* Stabil
* Worst case: O(n+k) Average case: Th(n+k) Best case: 𝝮(n+k) 
    * Hvis k=O(n) får vi kjøretid O(k)
###### Virkemåte
Counting sort bruker i tillegg til input-array A, output-array B og arbeidslager C. A[1...n], A.length = n, B[1...n] og C[0...k]. Arbeidslageret teller antall forekomster av de ulike verdiene og plasserer de direkte på plass i output-arrayet.

#### Radix sort
* Worst case: O(d(k+n)) AC: Th(d(k+n)) BC:Om(d(k+n))
    * Hvis k=O(n) får vi kjøretid O(k), ettersom vi bruker en subrutine som f.eks Counting sort som kan ha dette spesialtifellet.
###### Virkemåte
Radix sort sorterer tall med d-siffer, fra minst signifikante til mest signifikante. Subrutinen som sorterer sifferene **må** være stabil. Vi kan ikke endre rekkefølgen på tallene når de kommer ut av en subrutine selv om alle verdiene har samme siffer i den gjeldende kolonnen.

#### Bucket sort
* Worst case: O(n^2) Average case/best case: Th(n) (Når k = n)
###### Virkemåte
Her kan vi faktisk oppnå lineær kjøretid som average case, om vi går ut i fra at input er trukket fra en uniform distribusjon. Algoritmen distribuerer input over bøtter (Implementeres som lenkede lister) og kjører deretter (f.eks.) Insertion sort på hver av bøttene. Etter dette blir alle bøttene slått sammen og vi får en sortert output. 

### Selektering i lineær tid
#### Randomized SELECT
Som Randomized-Quicksort bruker algoritmen Randomized-partition, men i motsetning til Randomized-Quicksort som prosesserer begge sider av pivot, jobber Randomized-SELECT kun på en side. Denne forskjellen spiller en rolle på kjøretiden (QC AC: Th(nlgn)). Randomized-SELECT har en lineær kjøretid om vi har distinkte elementer. Worst case er Th(n^2) og vi oppnår dette om vi er uheldig med pivot-elementet vi partisjonerer rundt.
#### SELECT
Her tar vi inn pivot som input og kan dermed garanterere en god partisjonering. Worst case O(n). 

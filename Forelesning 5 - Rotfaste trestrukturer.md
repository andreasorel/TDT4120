# Forelesning 5 - Rotfaste trestrukturer
<img src="https://i.imgur.com/BSN9Q9R.png" width="150"/>

#### Heaps
Heaps/hauger er en datastruktur som brukes primært av Heapsort algoritmen. En haug er et listeobjekt som vi kan se på som et nesten-komplett binærtre. Treet er fylt på alle nivå bortsett fra muligens det laveste.  En liste A som representerer en haug er et objekt med to egenskaper: `A.length` som gir oss antall elementer i lista og `A.heap-size` som gir oss antall elementer i heapet som er lagret i lista.

I en heap med høyde h kan vi ha minimum 2^h elementer og maksimum (2^(h+1)) -1.

Eksempel:

<img src="https://i.imgur.com/QEQ3CK6.png" width="200"/>

##### MAX-HEAP / MIN-HEAP egenskapen

<img src="https://i.imgur.com/TkGIA8T.png" width="300" />

Ettersom høyden til et binærtre er Th(lgn) vil enkle operasjoner/prosedyrer aldri ta lenger enn  O(lgn) tid. 
##### BUILD-MAX-HEAP
Tar O(n) tid og produserer et MAX-HEAP fra en usortert input.
##### MAX-HEAPIFY
Tar O(lgn) tid og har som oppgave å opprettholde max-heap egenskapen.

##### Flere operasjoner som bruker O(lgn) tid
Disse operasjonene gjør det mulig for heapen å implementere en prioritetskø.
* MAX-HEAP-INSERT
* HEAP-EXTRACT-MAX
* HEAP-INCREASE-KEY
* HEAP-MAXIMUM

#### Heapsort
Sorterer elementer `in-place` ved bruk av `BUILD-MAX-HEAP` og `MAX-HEAPIFY`. Kjøretiden til disse to prosedyrene er henholdsvis O(n) og O(lgn) og dermed har Heapsort en kjøretid på O(nlogn). 

1. Kjør `BULD-MAX-HEAP`
    * Første/øverste element er nå det største elementet og kan legges sist i den sorterte listen.
2. Kjør `MAX-HEAPIFY` n-1 ganger
    * Hver gang fjerner vi det første elementet og legger det på sin plass i listen.
    
#### Prioritetskøer
En prioritetskø er en datastruktur vi bruker for å vedlikeholde en mengde S med elementer, hvorav hvert element har attributten `key`.
###### MAX-PRIORITY- og MIN-PRIORITY QUEUE
Støtter følgende operasjoner:
* `INSERT(S,x)` - Sett inn x i S
* `MAXIMUM(S)`/`MINIMUM(S)` - Returnerer det elementet i S med størst/minst key.
* `EXTRACT-MAX(S)`/`EXTRACT-MIN(S)` - Fjerner og returnerer det elementet med størst/minst key.
* `INCREASE(S,x,k)`/`DECREASE(S,x,k)` - Øker/minker verdien key i elementet x i mengden S med verdien k.

#### Rotfaste trestrukturer
Kan implementeres som en lenket liste med pekere, hver node inneholder `key`.
##### Rotfaste trestrukturer med ubegrenset forgreining
Left-child, right-sibling-representation bruker O(n) plass for ethvert n-rotet tre.
* x.left-child peker til venstre nærmeste barn
* x.right-sibling peker til det elementet direkte til høyre for elementet.

<img src="https://i.imgur.com/utJ4dvd.png" width="300"/>

###### Binærtre
Hver node inneholder x.right og x.left som representerer det høyre og venstre barnet til noden. Hver node inneholder og x.p som referer til foreldrenoden. Hvis x = T.root => x.p = NIL

<img src="https://i.imgur.com/BDRl9om.png" width="280"/>

###### Binært søketre
* Binary-search-tree property
    * La x være en node i et binært søketre
        * Hvis y er en node i det venstre subtreet til x så er y.key =< x.key
        * Hvis y er en node i det høyre subtreet til x så er y.key >= x.key

<img src="https://i.imgur.com/Cy2aWg8.png" width="600"/>

#### Traversering av trær
##### In-order tree walk
Dersom x er rotnode i et n-doe subtre tar traverseringen Th(n) tid. Går igjennom tree og printer ut key verdiene til roten av et subtre mellom å printe verdiene i rotens venstre og høyre subtre.

<img src="https://i.imgur.com/MOHO0fP.png" width="500"/>

##### Pre-order tree walk
Skriver ut key-verdien til roten før key-verdiene i subtrærne

<img src="https://i.imgur.com/kKLGFcm.png" width="500"/>

##### Post-order tree walk
Skriver ut key-verdien til subtrærne før key-verdien til rotnoden.

<img src="https://i.imgur.com/CkSwk1D.png" width="500"/>


#### Søk i binærtre
Tar O(h) tid der h=høyden på treet.

#### Insetting og sletting
* TREE-INSERT
* TREE-DELETE
    * 3 alternativer
        * Hvis z ikke har noen barn så fjerner vi noden ved å endre foreldrenoden til å erstatte z med NIL som sitt barn.
        * Hvis z har kun ett barn så løfter vi barnet slik at det tar z's posisjon i treet ved å endre z's foreldrenode til å erstatte z med barnet til z.
        * Hvis z har to barn så finner vi z's etterkommer y som må være i z's høyre subtre. Vi lar så y ta z's posisjon i treet. Resten av z's venstre subtre blir y's nye venstre subtre.
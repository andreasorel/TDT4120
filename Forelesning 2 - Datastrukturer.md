# Datastrukturer
**En måte å lagre data på for å legge til rette for tilgang og endringer**
## Stakker
* Kun adgang øverst/sist i stakken
* LIFO - Last In First Out
* POP - Fjern siste element
* Push - Leff til element på slutten
## Køer
* FIFO
* `ENQUEUE` Legg til element bakerst
    * `Q[Q.tail] = x`
* `DEQUEUE` Fjern første element
    * `x = Q[Q.head], Q.head = x - 1`
## Lenkede lister
* Består av noder som inneholder pekere til forrige og neste element i listen.
* Tar **Linær** tid å slå opp på en gitt posisjon `LIST_SEARCH = O(n)`
* Tar **Konstant** tid å **sette inn** eller **slette** elementer `LIST_INSERT eller LIST_DELETE = O(1)`
##### LIST_INSERT Illustrasjon
<img src="https://i.imgur.com/5UYw4Fn.jpg" width="400"/>

## Hashtabeller
* Direkte addressering
    * Nøkkel = indeks
* Hashtabeller
    * Modifisert nøkkel er indeks
    * Putter objektene inn i en hashfunksjon og får ut en gyldig indeks.
        * Eksempel på hashfunksjon: `h(k) = k mod n`
    * Hashing
        * Regn ut indeks fra nøkkelverdien
    * Chaining
        * Hver posisjon har en liste
        * Om to verdier hasher til samme posisjon får vi en **kollisjon**. For å ta vare på begge verdiene kan vi for eksempel ha en lenket liste i hver celle i tabellen.
        * `Mange kollisjoner = Lineært lange liste`
    * Søk tar lineær tid `O(n)`
    ```
      Anta lineært stor tabell
    + Anta jevn, tilfeldig fordeling
    = Konstant forventet kjøretid 
    ```
## Amortisert arbeid
Om en hashtabell/stakk/kø blir full ønsker vi å allokere mye minne om gangen, ettersom det tar linær tid.
#### Formel
<img src="https://imgur.com/pvuxXVt.jpg" width="200"/>

Ekstra arbeid per insetting: θ(`1`)

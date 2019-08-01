# Forelesning 8  - Traversering av grafer
Vi søker gjennom en graf ved å systematisk følge kantene (E) til grafen for å besøke nodene (V) i grafen. 
#### Grafrepresentasjon og implementasjon
Grafen G = (G,V) kan representeres på to ulike måter:
1. Som en samling av nabolister
2. Som en nabomatrise

Disse to representasjonene er gyldige for både retta og uretta grafer. Nabolister er vanligst ettersom det gir en kompakt måte å vise glisne grafer (glisn = eng: sparse, når |E| er mye mindre enn |V|^2). Dersom grafen er tett (eng: dense) vil nabomatrise være å foretrekke. 

<img src="https://i.imgur.com/OfoZtg3.png"/>

* Nabolisten og nabomatrisen vil se relativt lik ut for retta grafer, men kantene vil ikke nødvendigvis gå begge veier.

* I retta grafer vil summen av alle nabolistene være |E| mens i uretta grafer vil summen være 2|E| fordi hvis (u,v) er i en naboliste vil (v,u) være i en annen naboliste.
* I glisne grafer vil nabolister ta mindre plass enn nabomatriser, men ikke ellers. Det tar lengre tid å søke opp en kant i nabolister. Nabomatriser bruker kortere tid på å søke opp en kant men bruker mer asymptotisk mer minne dersom grafen er glisn. 

#### BFS
Kjøretid: WC/AC: `Θ(V+E)`, O(V) kø operasjoner og O(E) tid å skanne alle nabolister. BC: `Θ(V)` siden vi må initialisere alle nodene.

Gitt grafen G = (V,E) og en kildenode s, utforsker BFS systematisk kantene
i grafen for å finne hver node man kan nå fra s. Den kalkulerer dermed avstanden fra s til
hver node man kan nå. Fungerer på både retta og uretta grater. Bruker farger til å karakterisere om en node er besøkt. 

<img src="https://i.imgur.com/LfYRIfw.png" width="300"/>

Algoritmen konstruerer et bredde-først-tre. Hver gang søket finner en hvit node v når den søker i nabolisten til en alt oppdaget node u, blir node v og kanten (u,v) lagt til i treet

BFS bruker en FIFO kø til å prioritere noder, hvis denne køen endres kan vi risikere å ta omveier for å finne nodene.
###### Attributter
* u.color 
* u.pi = forgjengeren
* u.d = avstanden fra s til u
##### Å finne korteste vei
Vi definerer korteste vei til å være minimum antall kanter i enhver sti fra s til v, 𝛿(s,v). Dersom det ikke finnes en vei fra s til v så er 𝛿(s,v) = ∞

#### DFS
Målet med DFS er å søke *dypere* i en graf hvis det er mulig. DFS Utforsker kanter ut i fra den nyligst oppdagede kanten V som fortsatt har besøkte kanter som går ut ifra noden. Når alle kantene til noden er blitt utforsket går søket et nivå *opp* for å utforske noder fra der v ble oppdaget.

Som i BFS, når DFS oppdager en node v under en scan av nabolisten til en allerede oppdaget node u, tar den opp denne hendelsen ved å sette v sin forgjenger-attributt v.pi til u. Der BFS sin forgjenger-delgraf danner et tre, danner DFS flere slike trær. Dette skjer fordi søket kan gjentas fra flere kilder.

<img src="https://i.imgur.com/QsdSd4V.png"/>

I tillegg til en DF-skog lagrer og DFS timestamps på hver node. Hver node har to timestamps, v.d - start(grå farge) og v.f - slutt(svart farge). Formatet på timestamps er heltall mellom 1..2|V|.

Kjøretiden til DFS er definert av DFS-VISIT som tar Θ(E) tid og DFS som kaller DFS-VISIT tar Θ(V) tid. Legger vi dette sammen får vi en total kjøretid på `Θ(V+E)`.

##### Kantklassifisering
Vi kan bruke DFS til å klassifisere kanter. Dette kan gi oss informasjon om grafen. For eksempel så er en retta graf asyklisk hvis vi med DFS ikke finner noen *back edges*.

1. **Tree edges** er kanter i DF-skogen.
2. **Back edges** er kanter til en forgjenger i DF-skogen.
3. **Forward edges** er kanter utenfor DF-skogen til en etterkommer i DF-skogen.
4. **Cross edges** er alle andre kanter.

Noen eksempler:
* Om vi møter på en hvit node er dette en **Tree edge**
* Grå node -> **back edge**
* Svart node -> **Forward edge** eller **cross edge**

#### Parantesteoremet
I et DFS av en graf G = (V,E) for enhver to noder u og v , vil akkurat en av de følgende forholdene holde:
1. Intervallene (u.d,u.f) og (v.d,v.f) er fullstendig separate og har Ikke noe med hverandre å gjøre.
2. Intervallet (u.d,u.f) eksisterer innad i intervallet (v.d,v.f) i sin helhet, og u er en etterkommer av v i et DF-tre.
3. Intervallet (v.d,v.f) eksisterer innad i intervallet (u.d,u.f) i sin helhet, og v er en etterkommer av u i et DF-tre.

#### Topological sort
Vi kan bruke DFS til å utføre en topologisk sortering På en DAG. En topologisk sortering
av en DAG G = (V,E) er en lineær ordning av alle nodene slik at hvis G inneholder en kant (u,v)
så skrives u før v. TS kan brukes til ordning av etterkommere. Tenk eksempelvis å kle på seg / bygge hus. TS bruker `Θ(V+E)` tid siden det tar O(1) å sette inn hver av nodene inn foran i den lenkede listen. Husk at *back edges* er kanter til en forgjenger i DF-skogen, en DAG er en graf uten *back-edges*.
# Forelesning 9 - Minimale spenntrær
#### Disjoint-set operations
En disjoint-set datastruktur vedlikeholder en samling av disjunkte, dynamiske mengder. Hver menge identifiseres av en representant(et medlem av mengden).
* MAKE-SET(x) - Lager et nytt sett med kun ett medlem, x.
* UNION(x,y) - Slår sammen mengde x og mengde y. Vi går ut i fra at de er disjunkte før sammenslåingen.
* FIND-SET(x) - Returnerer pekeren til representanten til mengden der x befinner seg.
* n = Antall MAKE-SET
* m = Totalt antall MAKE-SET

Vi kan bruke disjoint-set datastrukturen til å finne de sammenkoblede komponentene i en graf.

#### Disjoint-set forests
Vi kan representere disjunkte mengder som rotfaste trestrukturer med ett element per node og hvert tre som en mengde. I en disjunkt-mengde skog har hvert tre en rotnode som er mengdens representant og den gjenkjennes ved at den refererer til seg selv som parent. x.p = x.

Denne implementasjonen er ikke nødvendigvis raskere enn en lenket liste. Men, ved å bruke noen. heuristikker("regler") kan vi forbedre kjøretiden til å være nesten lineær O(m⍺(n) der ⍺(n) er en svært saktegående funksjon. Lenket liste bruker O(m + nlgn) tid.

**Heuristikker**:
* Union-by-rank - Hver node får en rank(høyden til noden). Noder med lavere rank peker til noder med høyere rank.
* Path compression - Hver node peker til root uten å endre rank.

### Minimale spenntrær
Vi dyrker en MST en kant av gangen, grådig. Metoden administrerer en menge av kanter A og passer på å ivareta følgende løkkeinvariant: ++Før hver iterasjon så er A en delmengde av et MST++. For hvert steg så bestemmer vi en kant (u,v) som vi kan legge til i A uten å bryte invarianten. En slik kant er en trygg kant.

Definisjoner:
* Cut(S,V-S) til en uretta graf ern en partisjon av V.
* En kant krysser snittet (S,S-V) hvis en av endepunktene er i V og den andre i V-S.
* Et snitt respekterer en mengde A av kanter dersom ingen kanter i A krysser snittet.
* En lett kan er den kant som krysser kuttet med lavest vekt av alle kantene som krysser snittet. MERK: Vi kan ha flere lette kanter.

##### Hvorfor er en lett kant en trygg kant?

La G=(V,E) være en uretta graf med en vektfunksjon w definert på E. La så A være en delmengde av kanter(E) som befinner seg i en vilkårlig MST til G. La (S,V-S) være et vilkårlig snitt av G som respekterer A, og la (u,v) være en lett kant som krysser snittet (S,V-S). Da kan kanten legges til i A.


#### MST-Kruskal og MST-Prim
Begge er algoritmer for å finne minimale spenntrær. Begge er grådige fordi de alltid legger til den kanten med lavest kantvekt som er gyldig. 

Kruskal bruker en mengde-skog A. Vi ønsker å velge den kanten med lavest vekt, som ikke danner en sykel og som kobler sammen to komponenter. Algoritmen har kanter i prioritetskøen sin. Kjøretid: O(ElgV).

I Prim så er A et mengde-tre. En trygg kant er her en kant med lavest kanvekt som knytter sammen treet A med en ny node som ikke er i treet enda. Algoritmen har en prioritetskø fylt med noder. Kjøretid: O(ElgV) eller O(E+VlgV) med fib. heap.
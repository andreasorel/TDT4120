# Forelesning 10 - Korteste vei en til alle
##### Varianter av SSP problemer
* Single-destination shortest-paths - Finn korteste vei til en destinasjon t fra enhver node v. Ved å snu alle kantretningene i grafen kan dette reduseres til et SSP problem
* Single-pair shortest-path - Finn korteste vei mellom node u og v. Hvis vi løser SSP for u, løser vi og dette problemet.
* All-pair shortest path - Vi kan løse dette ved å kjøre SSP fra hver node men det er ikke optimalt. 

#### Optimal delstruktur til en korteste vei
Korteste vei algoritmer er ofte avhengig av at en korteste vei mellom to noder er vygget opp av flere korteste veier innad. Optimal delstruktur er en av indikatorene på at DP eller grådighet kanskje kan brukes. Dijkstra er en grådig algoritme, mens Floyd Warshall(APSP) bruker DP.

#### Negative kantvekter
Selv når vi har negative kantvekter i en graf er korteste vei vekten δ(s,v) ok, så lenge vi ikke har negative sykler. Hvis det finnes en negativ sykel vil vi kunne traversere i de evig og få en kortere vei. Vi setter derfor δ(s,v) = ∞ om vi har en negativ kanvekt-rykel på veien mellom s og v.

#### Sykler
En SP kan ikke inneholde en negativ sykel og den kan heller ikke inneholde en positivt vektet sykel, ettersom det vil alltid finnes en kortere vei som ikke inneholder sykelen. Det samme gjelder 0-vekt-sykler, som vi trygt kan fjerne fra stien vår. Siden enhver asyklisk sti i en graf G=(V,E) inneholder på det meste |V| distinkte noder, inneholder stien og på det meste |V|-1 kanter. Dermed trenger vi bare forholde oss til SP'er med |V|-1 kanter.


#### Respresentere SP
* Forgjenger v.pi = en annen node eller NIL -> SSP setter v.pi verdiene slik at kjeden av forgjengerne går langs den korteste stien. Dette kalles en forgjenger delgraf.
* Representere SPer ved bruk av en trestruktur. Et SP-tre er som et BFS-tre men istedenfor antall kanter inneholder SP-treet korteste vei fra s til v definert ut i fra kantvektene.
* SPer er ikke nødvendigvis unike og det er ikke SP-trær heller.

#### Kantslakking (Relax)
* v.d = Øvre grense på vekten til en kant i SP fra s->u
* v.pi = Forgjenger

Vi starter med å sette alle v.d til ∞ og v.pi til NIL. Kantslakking går ut på å se om vi kan forbedre nåværende korteste vei til v ved å gå igjennom u. Hvis vi kan det oppdaterer vi v.d og v.pi.

#### Bellman Ford
* Kan ha negative kantvekter
* Rapporterer om negative sykler
* Kjører RELAX på alle kantene til den oppnår den korteste-vei vekten δ(s,v).
* Kjøretid O(VE)

#### DAG-shortest-paths(G,w,s)
Vi finner korteste veien fra en kilde s i Th(V+E) tid ved å:
* Relax'e alle kantene
* Topologisk sorter nodene.
Alle beregninger som gjøres bottom-up i en DAG kan sees på som **dynamisk programmering**.

#### Dijkstra
Mens Prim og Kruskal finner minimale spenntrær finner Dijkstra korteste vei en til alle i en vektet, retta graf.
* Ikke negative kanter
* O(ElgV) eller O(VlgV + E) med fib.heap.
* Bruker en min-pri-kø
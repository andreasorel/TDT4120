# Forelesning 11 - Korteste vei alle til alle
Vi kan løse alle til alle problemet ved å kjøre en SSP-algoritme |V| ganger, f.eks Dijkstra (Dersom grafen ikke inneholder noen negative kanter). Dette vil ta O(V^3) tid om vi bruker en min-pri-kø, O(VElgV) med binary heap, eller O(V^2 lgV + VE) med fibonacci heap. Dersom grafen har negative kanter kan vi bruke Bellman Ford som gir oss en kjøretid på O(V^2 E), og O(V^4) på tette grafen.

Vi bruker nabomatriser når vi løser APSP problemer, fremfor nabolister som brukes i SSP.

#### Floyd Warshall
En DP-algoritme som kjører i O(V^3) tid dersom vi har en graf som potensielt inneholder negative kanvekter, men ikke negative sykler. Vi karakteriserer strukturen til korteste vei forskjellig enn det vi gjør i SSP-problemer. Floyd Warshall ser på de **mellomliggende nodene** i en kortest vei, der en mellomliggende sti til en annen sti p = <v1,v2,v3,...,v<sub>l</sub>> er enhver node untatt v1 og vl, altså enhver node i mengden {v2,v3,...,v<sub>l</sub>-1}.

Hvis *k* ++ikke++ er en mellomliggende node i stien p så er alle mellomliggende nodene i stien p i mengden {1,2,3,...,k-1}. Dermed er en korteste vei fra node til node j med alle mellomliggende nodene i mengden {1,2,3,k-1} også en korteste vei fra node i til node j med alle mellomliggende nodene i mengden {1,2,3,...,k}.

Hvis *k* ++er++ en mellomliggende node i stien p så deler vi p slik: `i--p1-->k--p2-->j`. Dermed er p1 korteste vei mellom i og k og p2 er korteste vei mellom k og j. Begge stiene p1 og p2 har mellomliggende noder i mengden. {1,2,3,...,k-1} ettersom k er den høyest nummererte mellomliggende noden i stien p.

###### En rekursiv løsning på APSP-problemet

d<sub>ij</sub><sup>k</sup> = Vekten til en korteste-vei fra i til j der alle mellomliggende noder er i mengden {1,2,3,...,k}. Dersom k=0 har stien ingen mellomliggende noder. En slik sti har på det meste 1 kant og dermed d<sub>ij</sub><sup>0</sup> = w<sub>ij</sub>. Hvis k > 0 så er d<sub>ij</sub><sup>k</sup> = min(d<sub>ij</sub><sup>k-1</sup>,d<sub>ik</sub><sup>k-1</sup> + d<sub>kj</sub><sup>k-1</sup>)

###### Kalkulerere korteste vei vekter bottom-up
Vi kan bruke en bottom-up prosedyre til å kalkulere verdiene d<sub>ij</sub><sup>k</sup> for å øke verdiene til k.
* Input: En nxn matrise W
* Output: matrisen D<sup>n</sup> som inneholder korteste vei vektene. 
Kjøretiden til Floyd Warshall er bestemt av de tre nøstede for-løkkene i prosedyren og vi får dermed en kjøretid på Th(n^3) der n = |V|.

###### Konstruere en korteste vei
Vi kan enten lage en forgjengermatrise π etter vi har funnet D eller så kan vi populere PI-matrisen mens vi kalkulerer D<sup>k</sup>. Vi definerer da pi<sub>ij</sub><sup>k</sup> som forgjengeren til node j på en korteste vei fra node i med alle mellomliggende noder i settet {1,2,3,..,k}. Når k=0 vil ikke en korteste vei fra i til j ha noen mellomliggendende noder.

For k>0, om vi tar stien i-->k-->j der k!=j, så blir forgengeren til j som vi velger den samme som forgjengeren til j vi velger på en korteste vei fra k med alle mellomliggende nodene i mengden {1,2,3,...,k-1)**HALLO**

#### Transitive closure på en retta graf
Gitt en graf med nodemengden {1,2,3,...,n}. TC finner ut om grafen inneholder en sti mellom i og j for alle nodepar i,j∈V. Vi definerer transitive closure til en graf som grafen G<sup>'</sup> = {V,E<sup>'</sup>} der E<sup>'</sup> ={(i,j): det finnes en sti fra i til j i G}.

En måte å kalkurere den transitive lukkingen til en graf er å tildele alle kantene en vekt 1 for så å kjøre Floyd Warshall. Hvis de finnes en sti mellom node i og j får vi d<sub>ij</sub> < n. Hvis det ikke finnes en sti får vi d<sub>ij</sub> = ∞.

En annen måte å kalkulere transitive closure til en graf i Th(n^3) tid som kan spare plass og tid i praksis er å bruke logiske operatorer som ∧ og ∨ istedenfor + i FW. Hvis det finnes en sti mellom i og j definerer vi t<sub>ij</sub><sup>n</sup> = 1. Hvis ikke blir t<sub>ij</sub><sup>n</sup> = 0. 

Hvis k>0 så er t<sub>ij</sub><sup>k</sup> = (t<sub>ij</sub><sup>k-1</sup> ∨ (d<sub>ik</sub><sup>k-1</sup>  ∧ d<sub>kj</sub><sup>k-1</sup>))

Som i Floyd Warshall kalkulerer vi matrisene T<sup>k</sup> = t<sub>ij</sub><sup>k</sup> for å øke k.

#### Johnson
* Kjøretid: O(V^2lgV + VE)
* Bruker nabolister
* Output: nxn matrise
* Raskere enn Floyd Warshall dersom grafen er glisn.

Finner korteste vei mellom alle nodepar ved å bruke både Bellman Ford og Dijkstra som subrutine. Den rapporterer og om negative sykler.

Algoritmen bruker en teknikk kalt revekting, som gjør følgende: 

Hvis alle kantvektene w i en graf er positive så kan vi finne korteste vei mellom alle nodepar ved å kjøre Dijkstra fra hver node. Med fib.heap min-pri-queue får vi O(V^2lgV+VE) kjøretid. Hvis grafen har negative kanvekter men ingen negative sykler kalkulerer vi bare en ny mengde med positive kantvekter w' som igjen lar oss bruke samme metode. w' må tifredstille følgende egenskaper:
1. For alle nodepar u,v så er en sti p en korteste vei sti fra u til v ved å bruke vektfunksjonen w hviss p også er en korteste vei fra u til v ved å bruke vektunksjonen w'.
2. For alle nodepar u,v så må den nye vekten w'(u,v) være ikke negativ.
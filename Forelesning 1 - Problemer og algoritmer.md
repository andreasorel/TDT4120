# Forelesning 1 - Problemer og algoritmer
* **RAM** 
    * Random access machine
    * Abstrakt maskin som kun kan utføre enkle aritmetiske operasjoner
    * Kan håndtere heltall og flyttall
    * Hver operasjon tar konstant tid å utføre
* **Problem**
    * Relasjon mellom input og output
* **Instans**
    * En bestemt input
* **Problemstørrelse (n)**
    * Lagringsplass som kreves for en instans
* **Kjøretid**
    * En funksjon av problemstørrelsen
##### Kjøretider - Hastighet
```katex
Constant:1
```
```katex
Logaritmic:lgn
```
```katex
Squared:\sqrt{n}
```
```katex
Linear: n
```
```katex
Loglinear: nlgn
```
```katex
Quadratic:n^2
```
```katex
Cubic:n^3
```
```katex
Exponential:2^n
```
```katex
Factorial:n!
```
* **Løkkeinvariant**
    * Invariant: Egenskap som ikke endres
    * Initialisering: Invariant er sann ved start
    * Vedlikehold i hver iterasjon:
        * Anta sann først
        * Vis sann etterpå
    * Terminering
        * Vis at løkka stopper
### Insertion Sort
* Effektiv for et lite antall elementer
* Kjøretid: θ(`$n^2$`)
### Asymptotisk notasjon
Vi ønsker å angi så tette grenser som mulig når vi beskriver kjøretiden til en algoritme.  Konstanter og lavere ordens ledd droppes.
```
ω > Θ(f(n)) Nedre grense, ikke asymptotisk bundet
Ω ≧ Θ(f(n)) Nedre grense
Θ = Θ(f(n)) Ligger mellom to skaleringer
O ≦ Θ(f(n)) Øvre grense
o < Θ(f(n)) Øvre grense, ikke asymptotisk bundet
```

### Best case, average case og worst case
#### Best case
Beste mulige kjøretid for en gitt størrelse
##### Average case
Forventet kjøretid gitt en sannsynlighetsfordeling
##### Worst case
Verste mulige kjøretid for en gitt størrelse


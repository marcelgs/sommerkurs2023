---
title: I - Grunnleggende sannsynlighetsteori
---


$\newcommand{\hdr}[4]{\color{#2}\boxed{\color{#2}\ #1\ \mid\ \textcolor{black}{#3} #4\ }\color{black} }$

$\newcommand{\defn}[1]{\hdr{D}{##fdc086}{#1}{}}$
$\newcommand{\defnn}[2]{\hdr{D}{##fdc086}{#1}{\ \mid\ \textcolor{black}{#2}}}$
$\newcommand{\thm}[1]{\hdr{T}{##7fc97f}{#1}{}}$
$\newcommand{\ex}[1]{\hdr{E}{##ae9ed4}{#1}{}}$
$\newcommand{\danger}[2]{\hdr{\textbf{☡}}{##cc0000}{#1}{\textcolor{##cc0000}{\textbf{☡}}}}$
$\renewcommand{\P}{\mathbb{P}}$
$\newcommand{\R}{\mathbb{R}}$
$\renewcommand{\|}{|}$



$%https://tex.stackexchange.com/a/326378$

# I - Grunnleggende sannsynlighetsteori
## Hendelser og sannsynlighetsmål

$\defnn{\text{Sannsynlighetsrom}}{(\Omega, \mathcal{E}, \P)}$ definerer et (stokastisk) eksperiment:

- $\Omega$ er mengden av alle enkeltutfall i eksperimentet.
- $\mathcal{E}$ er mengden av hendelser. Inntil videre holder det å tenke på hendelser som delmengder av $\Omega$, altså null eller flere av enkeltutfallene.[^1]
- $\defnn{\text{Sannsynlighetsmål}}{\P}$ som oppfyller *sannsynlighetsaksiomene*:
    1. $\P: \mathcal{E} \rightarrow [0,1]$\
    Sannsynlighetsmålet forteller oss sannsynligheten for en hendelse, og denne må være minst null (inntreffer aldri) og maksimalt én (inntreffer alltid).
    2. $\P(\Omega) = 1$\
    Det skjer alltid *noe*.
    3. $\P(E_1 \cup \dots \cup E_n) = \P(E_1) + \dots +\P(E_n)$ for alle hendelser $E_1, \dots, E_n$ som ikke har felles elementer (er *disjunkte*).\
    Om *enten* $E_1$ *eller* $E_2$ kan inntreffe, er sannsynligheten for at én av dem inntreffer lik summen av de to sannsynlighetene. 


$\defnn{\text{Komplement}}{A^{\complement}}$ til en hendelse $A$ oppfyller $\P(A^\complement)=1-\P(A)$

## Uavhengige hendelser

$\defnn{\text{Uavhengighet}}{A \perp B}$ hvis $\P(A\cap B)=\P(A)\P(B)$

&nbsp; &nbsp; &nbsp; Tilsvarende er flere mengder uavhengige hvis $\P(E_1 \cap \dots \cap E_n) = \P(E_1) \cdot \dots \cdot  \P(E_n)$.

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  $\danger{\text{Det er }\textbf{ikke}\text{ tilstrekkelig at mengdene er }\textit{parvis}\text{ uavhengige.}}{}$

$\ex{\text{To mynter}}$
- $\Omega = \set{\text{KK}, \text{KM}, \text{MK}, \text{MM}}$
- $\mathcal{E} = \mathcal{P}(\Omega)$[^2]. Vi gir tre mengder spesielle navn:
    - $A = \set{\text{KK}, \text{KM}}$, mengden av hendelser der første kast er kron
    - $B = \set{\text{KK}, \text{MK}}$, mengden av hendelser der andre kast er kron
    - $C = \set{\text{KK}, \text{MM}}$, mengden av hendelser der de to kastene er like

&nbsp; &nbsp; &nbsp; Er $A$, $B$ og $C$ uavhengige? Parvis uavhengige?

## Betinget sannsynlighet
$\defnn{\text{Betinget sannsynlighet}}{\P(A\mid B)} =\frac{\mathbb{P(A\cap B)}}{\P(B)}$

Med andre ord er $\P(A\mid B)$ sannsynligheten for at $A$ inntreffer, gitt at $B$ inntreffer.

## Stokastiske variabler

Ofte bryr vi oss mer om funksjoner av utfall enn utfallene i seg selv. For eksempel kan et utfall $\omega \in \Omega$ være gitt ved en fullstendig beskrivelse av alle luftmolekylene i atmosfæren over Kjeller en gitt dag. Dette er litt vanskelig å forholde seg til, så vi lager oss en "gjennomsnittlig bevegelsesenergi-funksjon" $T$ og kaller det den spytter ut for temperatur $T(\omega)$ i $\text{°C}$ ([ish](https://physics.stackexchange.com/questions/337549/what-is-the-definition-of-temperature-once-and-for-all)). Når vi skriver $\P(T \leq 20)$, snakker vi egentlig om $\P(\set{\omega : T(\omega) \leq 20})$[^3].

Det er viktig å merke seg at det ikke er noe stokastisk med variabelen (funksjonen) *i seg selv*. All tilfeldigheten "bor" i det underliggende utfallsrommet, og stokastisiteten i verdiene variabelen tar er simpelthen et resultat av dette.

Den formelle definisjonen er kronglete, så vi nøyer oss med å si at verdiene som funksjonen tar, ofte er intervaller av reelle tall, mengder av heltall, eller kategorier som ikke lar seg ordne (f.eks. rød/gul/grønn eller ja/nei).

Om vi kan definere en fornuftig ordning på verdiene, er det ofte nyttig å snakke om sannsynligheten for at variabelen er mindre enn et visst tall:

$\defnn{\text{Kumulativ fordelingsfunksjon}}{F_X(x)} = \P(X \leq x)$

&nbsp; &nbsp; &nbsp; $\ex{\text{Egenskapene til } F_X}$ Hva skjer med $F_X$ når $X\rightarrow \pm \infty?$ Hva kan vi si om $F_X(x)$ og $F_Y(y)$ når $x<y$?

I de to siste tilfellene sier vi at variabelen er *diskret*, og vi kan definere en *massefunksjon*:

$\defnn{\text{Sannsynlighetsmassefunksjon}}{p_X(x)} = \P(X=x)$

Om du husker at $\P(X=x) = \P(\set{\omega:X(\omega)=x})$ og tar en titt på sannsynlighetsaksiomene [over](#hendelser-og-sannsynlighetsmål), er det lett å se at $p_X$ har følgende egenskaper:
- $p_X(x) \in [0,1]$
- $\sum\limits_{x \in A} p_X(x) = \P(X \in A)$, der $A$ er en mengde av verdier $X$ kan ta\
Ulike verdier representerer disjunkte hendelser - $T(\omega)$ kan ikke ha flere verdier samtidig (temperaturen kan ikke være både 20 og 25 grader på samme tid!)
- $\sum\limits_{x \in \text{ran(X)}} p_X(x) = 1$, der $\text{ran}(X)$ er alle mulige verdier X kan ta

Hvis $X$ tar verdier i $\R$ og $F_X$ er kontinuerlig, sier vi at $X$ er kontinuerlig. Da gir det ikke lenger mening å snakke om sannsynlighetsmasse (hva er sannsynligheten for at temperaturen er *nøyaktig* 20 grader?)

Vi introduserer derfor konseptet *tetthet*:

$\defnn{\text{Sannsynlighetstetthetsfunksjon (pdf)}}{f_x(x)}$ slik at $F_X(x) = \int\limits_{-\infty}^x f_X(u)\ du$[^4]

&nbsp; &nbsp; &nbsp; Det følger at $\P(a < X \leq b) = \int\limits_a^b f_X(u)\ du$.

&nbsp; &nbsp; &nbsp; $\ex{\text{Egenskapene til } f_X}$ Hvilke verdier kan $f_X$ ta? Kan $f_x$ være negativ (på et intervall)? Kan $f_x$ være større enn 1?


## Simultan sannsynlighetsfordeling og uavhengige stokastiske variabler
$\defnn{\text{Simultan massefunksjon}}{p_{X,Y}(x,y)}=\P(X=x \text{ og } Y=y) = $ $\P(\set{\omega : X(\omega) = x \text{ og } Y(\omega) = y})$

Definisjonen av uavhengighet for diskrete stokastiske variabler følger direkte av den for hendelser [over](#uavhengige-hendelser).

<!-- Remark on Tonelli? -->
$\defnn{\text{Simultan tetthetsfunksjon}}{f_{X,Y}(x,y)}$ slik at $F_{X,Y}(x,y) = \P(X \leq x \text{ og }Y \leq y) = \int\limits_{-\infty}^x \int\limits_{-\infty}^y f(u,v)\ du\ dv$

På samme måte har vi at $X\perp Y \iff f_{X,Y}(x,y)=f_X(x)f_Y(y)$.


## Betinget tetthet
$\defnn{\text{Betinget massefunksjon}}{p_{Y \mid X}(y)} = \P(Y=y \mid X = x)$[^5]

$\defnn{\text{Betinget tetthet}}{f_{Y \mid X}(y)} = \frac{f_{X,Y}(x,y)}{f_X(x)}$

For uavhengige variabler er den betingede massefunksjonen (tetthetsfunksjonen) lik den marginale massefunksjonen (tetthetsfunksjonen): $p_{Y \mid X} = p_Y$, $f_{Y \mid X} = f_Y$.

## Bayes' teorem

$\thm{\text{Bayes (hendelser)}}$ $\P(B \mid A) = \frac{\P(A \mid B)\P(B)}{\P(A)}$

$\thm{\text{Bayes (tettheter)}}$ $f_{Y \mid X = x }(y) = \frac{f_{X \mid Y = y}(x) f_Y(y)}{f_Y(y)}$

$\ex{\text{Bevis Bayes' teorem}}$ (følger fra definisjonen av betinget sannsynlighet)

## Momenter
$\defnn{\text{Forventning (diskret }X\text{)}}{\mu = \mathbb{E}[X]}=\sum\limits_{\text{alle } x}x\cdot p_X(x)$

$\defnn{\text{Forventning (kontinuerlig }X\text{)}}{\mu = \mathbb{E}[X]}=\int\limits_{-\infty}^{\infty}x\cdot f_X(x)\ dx$

Vi kan tolke forventningen som gjennomsnittet av verdiene $X$ tar, vektet etter hvor ofte de inntreffer.

$\defnn{\text{Varians}}{\mathbb{V}[X]}=\mathbb{E}[(X-\mu)^2]$

Tolkning: Vi finner avstanden fra hver av verdiene $X$ kan ta til forventningen (gjennomsnittet). Så tar vi forventningen igjen for å finne den gjennomsnittlige avstanden (igjen vektet etter hvor ofte verdiene inntreffer). Vi kvadrerer slik at positive og negative avstander ikke nuller hverandre ut.

$\ex{\text{Vis at }\mathbb{V}[X]=\mathbb{E}[X^2]-(\mathbb{E}[X])^2}$

$\ex{\text{Vis at }\mathbb{E}[a\cdot X+b\cdot Y]=a\cdot \mathbb{E}[X]+b\cdot \mathbb{E}[Y]}$ der $X$ og $Y$ er stokastiske variabler og $a$ og $b$ er reelle tall

$\ex{\text{Vis at }\mathbb{V}[a\cdot X+b\cdot Y]=a^2\cdot \mathbb{V}[X]+b^2\cdot \mathbb{V}[Y]}$ der $X$ og $Y$ er **uavhengige** stokastiske variabler og $a$ og $b$ er reelle tall. Hvorfor krever vi $X \perp Y$?

$\ex{X\thicksim \text{Beta}(\alpha,\beta)\text{. Finn } \mathbb{E}[X]\text{ og }\mathbb{V}[X].}$[^6]

&nbsp; &nbsp; &nbsp; $\defn{\text{Beta(}\alpha, \beta\text{)}}$ har tetthet $f(x)=\frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha)\Gamma(\beta)} x^{\alpha-1}(1-x)^{\beta-1}$[^7]

&nbsp; &nbsp; &nbsp; Hint: Flytt det som ikke avhenger av $x$ utenfor integralet. Skriv $a=a+1 -1$.

## Transformasjoner av stokastiske variabler
La den stokastiske variabelen $Y$ være gitt ved en funksjon $g$[^8] av en annen stokastisk variabel $X$, altså $Y=g(X)$.


$\thm{\text{Transformasjon av kontinuerlig stokastisk variabel}}$ $f_Y(y) = f_X(g^{-1}(y))\left\|{\frac{dx}{dy}}\right\|$
 
$\ex{Y=e^X}$

&nbsp; &nbsp; &nbsp; $g^{-1}(y)=\ln(y)$

&nbsp; &nbsp; &nbsp; $\left\|{\frac{dx}{dy}}\right\|= \left\|{\frac{dg^{-1}(y)}{dy}}\right\| = \left\|{\frac{1}{y}}\right\|=\frac{1}{y}$

&nbsp; &nbsp; &nbsp; $f_Y(y) = f_X(\ln(y))\cdot \frac{1}{y}$

$\ex{\text{La } X\thicksim \mathcal{N}(0,1)\text{. Vis at } f_Y(y)=\frac{1}{y\sqrt{2\pi}}\exp\left(-\frac{\ln(y)^2}{2}\color{black}\right).}$

<br />
<br />
<br />
<br />
<br />
<br />
<br />


[^1]: Dette er ikke helt korrekt, og fungerer ikke når vi møter på mindre "hyggelige" mengder enn de vi tar for oss nå. Da må vi introdusere konseptet *målbarhet*, som er til å få vondt i hodet av.

[^2]: $\mathcal{P}(\Omega)$ er mengden av alle delmengder av $\Omega$, og inneholder $2^4=16$ mengder (sjekk selv!).

[^3]: Kolonet betyr "slik at".

[^4]: Lenge siden du har sett et integral? Frykt ikke! Tenkt på dette som at vi begynner med den laveste mulige verdien variabelen kan ta (f.eks. $T=-273.15$) og ser på hvilken sannsynlighets*tetthet* vi har ved denne verdien. Så øker vi gradvis verdien av variabelen til vi når verdien vi ønsker, og "summerer opp" alle tetthetene. Til slutt ender vi opp med en *sannsynlighet* (f.eks. for hendelsen $T < 20$, med $\P(T < 20) = F_T(20) = \int\limits_{-\infty}^{20} f_T(u)\ du$). For ordens skyld er det verdt å nevne at vi også krever at $F$ er deriverbar.

[^5]: Husk at $X=x$ viser til hendelsen $\set{\omega : X(\omega)=x}$

[^6]: $\thicksim$ betyr "følger" (som i "$X$ følger en betafordeling")

[^7]: Gammafunksjonen $\Gamma$ dukker opp nærmest overalt i matematikken. Siden vi kun integrerer over $x$ i forventningen, trenger du ikke å forholde deg til hvordan den er definert.

[^8]: $g$ må være deriverbar og strengt stigende eller strengt synkende. Ser du hvorfor?
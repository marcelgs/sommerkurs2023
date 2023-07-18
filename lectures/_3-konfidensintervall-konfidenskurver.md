

$\newcommand{\hdr}[4]{\color{#2}\boxed{#1\ |\ \textcolor{black}{#3} #4}\color{black} }$

$\newcommand{\defn}[1]{\hdr{D}{fdc086}{#1}{}}$
$\newcommand{\defnn}[2]{\hdr{D}{fdc086}{#1}{\ |\ \textcolor{black}{#2}}}$
$\newcommand{\thm}[1]{\hdr{T}{7fc97f}{#1}{}}$
$\newcommand{\ex}[1]{\hdr{E}{ae9ed4}{#1}{}}$
$\newcommand{\danger}[2]{\hdr{\textbf{☡}}{cc0000}{#1}{\textcolor{cc0000}{\textbf{☡}}}}$
$\renewcommand{\P}{\mathbb{P}}$

$\newcommand{\iidsim}{\overset{\mathrm{iid}}{\sim}}$

$\newcommand{\distconv}{\overset{d}{\rightarrow}}$



# III: Large sample-teori, konfidensintervaller, konfidenskurver

Vi oppsummerer noen egenskaper ved MLE:

La $Y_1, \dots, Y_n \iidsim f_Y(y;\theta)$, $\theta \in \R^p$

1. $\sqrt{n}(\hat\theta - \theta)\overset{d}{\rightarrow} \mathcal{N}(0, I(\theta)^{-1})$
   Sett in defn av I i linjen under
2. Deltametoden: Gitt 1, har vi $\sqrt{n}(g(\hat\theta)-g(\theta))\overset{d}{\rightarrow} \mathcal{N}(0, \nabla g(\theta)^T I(\theta)^{-1} \nabla g(\theta))$

En svakhet ved dette er at dette baseres på en Taylorapproksimasjon. Hvis $n$ er liten, er denne ikke nødvendigvis særlig god.

I tillegg gir det alltid symmetriske konfidensintervaller.

Et universelt bedre alternativ er å bruke Wilks' teorem:

La *fokusparameter* $\gamma=g(\theta) = g(\theta_1, \dots, \theta_p)$

For eksempel kan $\gamma$ være variansen til en gammafordeling eller et kvantil til en normalfordeling.

**Steg 1: profilering**

$\defnn{\text{Profilert likelihood}}{\ell_{prof}(\gamma)}= \max{\ell(\theta): g(\theta)=\gamma}$

Merk at $\hat\gamma = g(\hat\theta)$

$\max_\theta \ell(\theta) = \max_\gamma \ell_{prof}(\gamma)$

**Steg 2: deviance function**

$D(\gamma) = 2(\ell(\hat\theta)-\ell_{prof}(\gamma))$

**Steg 3: Wilks' teorem**

$\defnn{\chi^2\text{-fordeling}}{}$
Sett inn pdf og support samt defn som snitt av N(0,1)

$\thm{\text{Wilks}}D(\gamma) \distconv \Chi_1^2$ altså kvadratet av N(0,1)

**Steg 4: konfidensintervaller**

$100p\%\ \text{CI} = \set{\gamma: D(\gamma) \leq \Gamma_1^{-1}(p)}$

Er det Gamma eller T? Iaf CDF til chi_1^2

Tegner plott med z på x-aksen, cdf på y-aksen. Ser litt ut som log z. D(gamma) er intervallet på førsteaksen fra 0 til et punkt. På andreaksen er det merket av et punkt som jeg ikke klarer å lese aksemerket til.

Vi går tilbake til gammafordelingen.

Skriver opp pdf og support.

$\ell(a,b) = \sum_1^n{a \log b - log \Gamma (a) + (a-1)\log y_i - b y_i}
= na\log b - n log \Gamma(a) + (a-1) \sum_1^n \ log (y_i) - b \sum_1^n y_i$

Vi profilerer:  $g(a,b) = \frac{a}{b^2}$

$\ell_{prof} (\gamma) = \max {\ell(a,b): \frac{a}{b^2}=\gamma} = \max{\ell(a,b):a=\gamma b^2} = \max_b n_b^2 \gamma \log b - n \log \Gamma()b^2 \gamma + (b^2 \gamma -1 ) \sum_1^n \log y_1 - b \sum_1^n y_1$

## Konfidenskurver

Det er temmelig vilkårlig at vi velger å se på 95%-konfidensintervallet. Hvorfor ikke 90 eller 99%?

Intuisjonssjekk: hva er 100% CI?


y-akse: alle mulige konfidensnivåer
x-akse: grensene (bounds) av alle mulige konfidensintervaller

Hvilken \gamma-verdi svarer til konfidensnivå 0? Jo, \hat\gamma!

$\text{cc}(\gamma) = \Gamma_1(D(\gamma))$

For eksempel: $\P(\gamma, D(\gamma) \leq 0.95) \rightarrow 0.95$

Vi kan legge inn flere kovariater. Vi tar for oss studien med etnisk diskriminering ved fotballag. Definer x = andel ikkevestlige i kommunen.

Ja, det har noe å si. Han tegner for minoritetsgruppen p (responsrate) som en linær oppadstigende funksjon av x. For majoritetsgruppen er det en konstant funksjon, høyere enn den forrige.

p_min defn som empirisk nitt av p(x_i)
p_maj er konstant, så da trenger vi ikke noen finurligheter

definerer \delta = p_maj - p_min
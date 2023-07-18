$\newcommand{\hdr}[4]{\color{#2}\boxed{#1\ |\ \textcolor{black}{#3} #4}\color{black} }$

$\newcommand{\defn}[1]{\hdr{D}{fdc086}{#1}{}}$
$\newcommand{\defnn}[2]{\hdr{D}{fdc086}{#1}{\ |\ \textcolor{black}{#2}}}$
$\newcommand{\thm}[1]{\hdr{T}{7fc97f}{#1}{}}$
$\newcommand{\ex}[1]{\hdr{E}{ae9ed4}{#1}{}}$
$\newcommand{\danger}[2]{\hdr{\textbf{☡}}{cc0000}{#1}{\textcolor{cc0000}{\textbf{☡}}}}$
$\renewcommand{\P}{\mathbb{P}}$

$\newcommand{\iidsim}{\overset{\mathrm{i.i.d.}}{\sim}}$

# II: Likelihood-funksjonen, Fisherinformasjon og deltametoden
## Grunnleggende konsepter
Modell: $Y_1, \dots, Y_n \iidsim f_Y(y;\theta)$[^1]\
Data (realiseringer, observasjoner): $y_1, \dots, y_n$

Sannsynlighetsteori: modell $\rightarrow$ data\
Statistikk: data $\rightarrow$ modell

Siden antikkens tid har en grunnleggende forståelse av sannsynlighet gjort nytte for seg innen [forsikring](https://en.wikipedia.org/wiki/History_of_insurance), [kryptoanalyse](https://en.wikipedia.org/wiki/Al-Kindi#Cryptography) og (selvsagt) [lykkespill](https://en.wikipedia.org/wiki/De_vetula#Non-poetic_content). Det aksiomatiske grunnlaget for feltet kom derimot først på plass i 1933 da Andrej N. Kolmogorov formulerte sannsynlighetsaksiomene vi møtte i forrige forelesning. Epistemologene strides fortsatt om hvordan sannsynligheter skal forstås, men vi skyver den diskusjonen under teppet og nøyer oss med superkorte forklaringer av de to dominerende paradigmene:

Frekventistisk sannsynlighetsteori: $\theta$ er bestemt, men ukjent. Sannsynlighet forstås som andeler av utfallene når et eksperiment gjentas mange ganger[^2]. Frekventistiske metoder går stort sett ut på å konstruere ulike estimatorer med ønskede egenskaper, der *maximum likelihood*-estimatoren er den viktigste.


Bayesiansk sannsynlighetsteori: $\theta$ er en stokastisk variabel. Sannsynlighet forstås som en grad av (epistemisk) usikkerhet. Bayesianske metoder er konseptuelt mye enklere - vi må "bare" definere en *likelihood* $f(x \mid \theta)$ og en *prior* $\pi (\theta)$ (vi kommer tilbake til hva dette betyr), og så er vi i prinsippet ferdige.

De tre neste forelesningene skal handle om frekventistiske metoder.

## Likelihood-funksjonen

Vi skal se på likelihood-funksjonen:

$\defnn{\text{Likelihood}}{\mathcal{L_n}(\theta)} = \prod_1^n f_y(y_i; \theta)$

$\defnn{\text{Log-likelihood}}{\ell_n(\theta)} = \log \mathcal{L_n} = \sum_1^n \log f(y_i;\theta)$

Siden vi antok at uavhengighet, ser vi at høyresiden av den første definisjonen rett og slett er simultanfordelingen til $Y_1, \dots, Y_n$. Forskjellen er at vi nå ser på uttrykket som en funksjon av $\theta$. Da blir det naturlig å spørre hvilken verdi av $\theta$ som maksimerer sannsynligheten for de observerte verdiene:

$\defnn{\text{Maximum likelihood estimator (MLE)}}{\hat{\theta}} = $ $\argmax\limits_{\theta \in \Theta} \mathcal{L}_n(\theta) = $
$\argmax\limits_{\theta \in \Theta} \mathcal{\ell}_n(\theta)$

$\ex{y_1, ..., y_n \iidsim \operatorname{Bernoulli}(\theta)\text{. Vis at }\hat{\theta} = \bar{y} = \frac{1}{n}\sum_1^n y_i .}$

## Digresjon: matrisederivasjon

I multivariabeltilfellet blir $\mathcal{L}(n)$ en matrise. Vi repeterer noen regler for derivasjon av matriser:

La $A$ være en matrise som avhenger av $x$: $A = A(x)$.

$$\begin{aligned}

A^{-1}A = I_n \\

\frac{\partial}{\partial x} A^{-1}A = 0 \\

\frac{\partial}{\partial x} A^{-1} A + A^{-1}\frac{\partial}{\partial x}A = 0 \\

\frac{\partial}{\partial x} A^{-1} = -A^{-1} \frac{\partial}{\partial x} A^{-1}

\end{aligned}$$

Vi tar resten av resultatene vi trenger [herfra](https://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf):

$\nabla_A (A^{-1})= -A^{-2}$

$\nabla_A(\mathrm{Tr}(AB)) = B^T$

$\nabla_A(\log |A|) = (A^{-1})^T = (A^T)^{-1}$

## MLE for $\mathcal{N_p}(\mu, \Sigma)$

Som i det enkelvariate tilfellet er den multivariate normalfordelingen parametrisert ved forventning og (ko)varians.

Def positiv definitt og symmetrisk.

$\ex{y_1, ..., y_n \iidsim \mathcal{N}_p(\mu, \Sigma)\text{. Finn }\hat{\theta}\text{ og }\hat{\Sigma}.}$

TODO: sett inn  Tricky fordi sigma må oppfylle kravene til kovariansmatrise, men vi glemmer det og håper/sjekker at det går greit

grad_z (l_n(mu, sigma)) = det du får

grad_z(y-mu)^T sum^-1 (y-mu)
= grad_z(Tr{(y-mu)^T sigma^-1 (y-mu)})
= grad_z(Tr{sigma^-1 (y-mu)(y-mu)^T})
= (y-mu)(y-mu^T)(- sigma^-2) (vi får en 1 x 1 matrise, altså et tall)

\ex y \dots \y_n \iidsim N_p(mu, Sigma)

n * sigma^-1 = sigma^-2 sum_1^n (y_i-mu)(y_i-mu)^2
sigma_hat = 1/n sum (y_i-muhat)(y_i-muhat)^T

\ex iid Exp(\theta), f(y;\theta) = theta e^(-theta y), 0 < y < inf
Sjekk at MLE = 1/ybar = 1/(1/n * sum yi)

\ex gamma (generalisering av Exp (sjekk hvilke parametre som reduserer Gamma til Exp))
TODO: Sett in pdf
TODO: Kommentar om ulike parametriseringer

-- kodeeksempel --

## Fisher-informasjon

$\defnn{\text{Fisher-informasjon}}{I(\theta)}$

Forventningen til partial_theta^t partial_theta av log f

\thm

y_i kommer fra f(y;theta)

sqrt(n)(theta_hat - theta) conv in dist Z thicksim N(0, I(theta)^-1)

Sammenlikn dette med CLT: sqrt(n)(y_hat - (mu=exp y)) rightarrow N(0, sigma^2 = V(Y))

Ex: finn asymptotisk fordeling til a hat/b hat^2

Fact: Var(Y\thicksim gamma) = a/b^2

## Deltametoden
La mathcal L være glatt
Anta at sqrt(theta hat_n - theta) rightarrow N(0, *S*igma)

h: \R^p -> \R

Da konvergerer sqrt(n) (h(theta hat_n) - h(theta) rightarrow N(0, grad h(theta)^T [n x p] * Sigma [p x p] * grad h(theta) [p x n])

Eks: h(a,b) = a/b^2
del h = vec(1/b^2 -2a/b^3)

%deltavariance i koden er variansen etter å ha brukt deltametoden%


[^1]: $\mathrm{i.i.d.}:$ independent and identically distributed. Du *kan* ([ifølge Wikipedia](https://no.wikipedia.org/wiki/Uavhengige,_identisk_fordelte_variabler)) skrive $\mathrm{u.i.f.}$ ("uavhengige og identisk fordelte") på norsk, men da ser folk rart på deg.

[^2]: Denne teoretiske antakelsen er det ofte vanskelig å implementere i praksis. Lykke til med å folk med på å nullstille verden til 1990 $n$ ganger for at du skal finne ut hvordan inflasjon og arbeidsledighet henger sammen.
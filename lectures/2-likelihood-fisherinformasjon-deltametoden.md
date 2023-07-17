$\newcommand{\hdr}[4]{\color{#2}\boxed{#1\ |\ \textcolor{black}{#3} #4}\color{black} }$

$\newcommand{\defn}[1]{\hdr{D}{fdc086}{#1}{}}$
$\newcommand{\defnn}[2]{\hdr{D}{fdc086}{#1}{\ |\ \textcolor{black}{#2}}}$
$\newcommand{\thm}[1]{\hdr{T}{7fc97f}{#1}{}}$
$\newcommand{\ex}[1]{\hdr{E}{ae9ed4}{#1}{}}$
$\newcommand{\danger}[2]{\hdr{\textbf{☡}}{cc0000}{#1}{\textcolor{cc0000}{\textbf{☡}}}}$
$\renewcommand{\P}{\mathbb{P}}$

$\newcommand{\iidsim}{\overset{\mathrm{iid}}{\sim}}$

# Likelihood-funksjonen, Fisherinformasjon og deltametoden
## Grunnleggende konsepter
Modell: $Y_1, \dots, Y_n \iidsim f_Y(y;\theta)$[^1]\
Data (realiseringer, observasjoner): $y_1, \dots, y_n$

Sannsynlighetsteori: modell $\rightarrow$ data\
Statistikk: data $\rightarrow$ modell

Siden antikkens tid har en grunnleggende forståelse av sannsynlighet gjort nytte for seg innen [forsikring](https://en.wikipedia.org/wiki/History_of_insurance), [kryptoanalyse](https://en.wikipedia.org/wiki/Al-Kindi#Cryptography) og (selvsagt) [lykkespill](https://en.wikipedia.org/wiki/De_vetula#Non-poetic_content). Det aksiomatiske grunnlaget for feltet kom derimot først på plass i 1933 da Andrej N. Kolmogorov formulerte sannsynlighetsaksiomene vi møtte i forrige forelesning. Epistemologene strides fortsatt om hvordan sannsynligheter skal forstås, men vi skyver den diskusjonen under teppet og nøyer oss med superkorte forklaringer av de to dominerende tolkningene:

Frekventistisk sannsynlighetsteori: $\theta$ er bestemt, men ukjent. Sannsynlighet forstås som andeler av utfallene når et eksperiment gjentas mange ganger[^2]. Frekventistiske metoder går stort sett ut på å konstruere ulike estimatorer med ønskede egenskaper, der *maximum likelihood*-estimatoren er den viktigste.


Bayesiansk sannsynlighetsteori: $\theta$ er en stokastisk variabel. Sannsynlighet forstås som en grad av usikkerhet. Bayesianske metoder er konseptuelt mye enklere - vi må "bare" konstruere en modell og en priorfordeling (vi kommer tilbake til hva dette betyr), og så er vi i prinsippet ferdige. Problemet ligger 

De tre neste forelesningene skal handle om frekventistiske metoder.

## Likelihood-funksjonen

Vi skal se på likelihood-funksjonen:

$\defnn{\text{Likelihood}}{\mathcal{L_n}(\theta)} = \prod_1^n f_y(y_i; \theta)$

$\defnn{\text{Log-likelihood}}{\ell_n(\theta)} = \log \mathcal{L_n} = \sum_1^n \log f(y_i;\theta)$

MLE = argmax av L_n = argmax av \ell_n

$\ex{y_1, ..., y_n \iidsim \operatorname{Bn}(\theta)\text{. Finn }\hat{\theta}.}$

TODO: Sett inn (skal bli theta hat = empirisk snitt (bar) av y_i)

$\ex{y_1, ..., y_n \iidsim \mathcal{N}_p(\mu, \Sigma)\text{. Finn }\hat{\theta}\text{ og }\hat{\Sigma}.}$

Def positiv definitt og symmetrisk.

## Digresjon: matrisederivasjon, hvordan vi deriverer L(sigma)

$A = A(x)$ n x n

$A^{-1}A = I_n$

\partial på x fra venstre m chain rule: part (A^-1)A + A^-1 partial A = 0

flytt til hver sin side og gang med A^-1 fra venstre

grad_a(A^-1) = A^-1 A^-1 = -A^-2 (tilsvarende univariate deriv av 1/x)

Vi slår opp: grad_A(Tr(AB))= B^T og grad_A(log|A|)=(A^-1)^T

## Digresjon slutt

TODO: sett inn  (gir samme svar). Tricky fordi sigma må oppfylle kravene til kovariansmatrise, men vi glemmer det og håper/sjekker at det går greit

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
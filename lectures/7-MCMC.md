---
title: II: MCMC
---


$\newcommand{\hdr}[4]{\color{#2}\boxed{\color{#2}\ #1\ \mid\ \textcolor{black}{#3} #4\ }\color{black}\ }$

$\newcommand{\defn}[1]{\hdr{D}{##fdc086}{#1}{}}$
$\newcommand{\defnn}[2]{\hdr{D}{##fdc086}{#1}{\ \mid\ \textcolor{black}{#2}}}$
$\newcommand{\thm}[1]{\hdr{T}{##7fc97f}{#1}{}}$
$\newcommand{\ex}[1]{\hdr{E}{##ae9ed4}{#1}{}}$
$\newcommand{\danger}[1]{\hdr{\textbf{☡}}{##cc0000}{#1}{\textcolor{##cc0000}{\mid \textbf{☡}}}}$
$\newcommand{\wip}[1]{\hdr{\textbf{🚧}}{##fcd100}{#1}{\textcolor{##fcb100}{\mid \textbf{🚧}}}}$

$\renewcommand{\P}{\mathbb{P}}$
$\newcommand{\E}{\mathbb{E}}$
$\newcommand{\V}{\mathbb{V}}$
$\newcommand{\R}{\mathbb{R}}$
$\renewcommand{\|}{|}$
$\newcommand{\norm}[1]{\mathcal{N}(#1)}$
$\newcommand{\tr}{\operatorname{tr}}$

$\newcommand{\iidsim}{\overset{\mathrm{i.i.d.}}{\sim}}$

$\newcommand{\deldel}[1]{\frac{\partial}{\partial #1}}$
$\newcommand{\bm}[1]{\boldsymbol #1}$

# VII: MCMC

% !CHECK NVOTES!

% Antar vel at den er stasjonær her?

La $p_{ij}^{(k)}=\P(X_{n+k}=i \mid X_n = j)$

% Mer at k utelates hvis k = 1

$\defn{\text{Periodisk tilstand}}$ Tilstanden $i$ har periode $t$ hvis $p_{ii}^{(k)}=0$ for $k\neq t, 2t, 3t, \dots$ og $p_{ii}^{(k)}>0$ for $k = t, 2t, 3t, \dots$

Vi sier at kjeden er aperiodisk hvis alle dens tilstander er aperiodiske.

% Irreduserbarhet?

$\thm{\text{Tilstrekkelig betingelse for irredusibilitet}}$ $\exist i: p_{ii}^{(1)} > 0$

% Begrunnelse mangler - sett inn.

Ekvivalent med at pu er en stasjonær tilstand:

$\pi_j = \sum_i pi_i P_{ij}$

Dette er ofte vanskelig å verifisere. Enklere:

$\defn{\text{Detailed balance}}$ $\pi_i P_{ij} = \pi_j P_{ji}$

$\lemma{\text{Detailed balance } \Implies \text{ stasjonær tilstand}}$

Bevis:
$\sum_i \pi_i P_{ij} = \sum_i \pi_j P_{ji} = \pi_j \sum_i P_{ji} = \pi_j$

$\thm{}$
La X_1, ... være en aperiodisk irredusibel Markovkjede. Da finnes det en unik stasjonør fordeling $\pi_i$, og $X_n \rightarrow \pi$ når $n \rightarrow \infty$.

---
Vi skal nå se på MC på kontinuerlige state spaces

Kernel: går fra p_{ij} til k(x,y)

Transition matrix P_ij -> transition kernel k(x,y)

Går fra sum til integral, altså matrise til kernel

$\P(X_{n+1}\in A \mid X_n = x) = \int_A k(x,y)\ dy$

Merk at vi kan også definere aperiodisitet og irredusibilitet, og vi har våre tilstrekkelige betingelser, for kontinuerlige Markovkjeder:

k(x,y)>0 \forall x,y \implies irredusibel (equiv?)

P(X_{n+1}=x | X_n = x)>0 \forall x og k(x,y)>0 \forallxy impleis aperiodic

% Stemmer det? Trodde irredusibel impl aperiodic?

Om stasjonære fordelinger:

% Dette er forsatt en venstre egenvektor!

$\pi(y) = \int pi(x)k(x,y)\ dx$

Detailed balance:

$\pi(x)k(x,y) = \pi(y) k(y,x)$

Ex: U%er det U?% is at DB \implies \pi stasjonær
Hint: $\int k(x,y)\ dy = 1$


# Metropolis-Hastings
$\theta \thicksim \pi(\cdot)$ Prir

$y \mid \theta \thicksim \pi(\cdot \mid \theta)$ Data model/likelihood

Bayes: sett inn

Marginal likelihood: sett in (integral)

----

Notasjon: $\theta_s$ er ved iterasjon $s$

Algoritme

1. $\theta_1 \thicksim \pi(\cdot)$
2. For s=2, ..., N do
   1. $\theta' \thicksim \mathcal{N}(\theta_{s-1}, \sigma^2)$ Propose new value
   2. $\alpha(\theta_{s-1}, \theta') = \min{1, \frac {\pi(\theta' \mid y)} {\pi(\theta_{s-1} \mid y)}}$
   3. With probability $\alpha(\theta_{s-1}, \theta')$: $\theta_s\leftarrow \theta'$
   4. Else: $\theta_s\leftarrow \theta_{s-1}$
3. Return $\theta_1, \dots, \theta_N$

Hvorfor funker dette? Mer at:

a) MH er en Markovkjede
b) Kernel: $k(\theta, \theta') = \alpha(\theta, \theta')N(\theta', \theta\sigma^2)+(1-\alpha(\theta,\theta'))\delta_\theta (\theta')$
c) Irredusibel: %rakk ikke å skrive dette%
d) %rakk ikke å skrive dette%

Lemma: Stasjonær fordeling pi(theta|y)

bevis: Sjekk DB: pi(theta|y) k(theta, theta') = pi(theta'|y)k(theta', theta) stemmer når theta' = theta


Anta at theta' = theta, k(theta, theta') = alpha(theta, theta')N(theta'; theta,pi^2)

$\pi(\theta \mid y)k(\theta, \theta') = \pi(\theta \mid y)\alpha(\theta, \theta)N(\theta'; \theta, \sigma^2)$ hvor siste N er propto $\exp(- \frac 1 {2\sigma^2} (\theta'-\theta)^2)$

Må sjekke at $\pi(\theta \ y)\alpha(\theta, \theta')=\pi(\theta'\mid y)\alpha(\theta' \mid \theta)$

$\pi(\theta \mid y)\alpha(\theta, \theta')=\pi(\theta \mid y)\times \min{1, \frac{\pi(\theta' \mid y)}{\pi(\theta\mid y)}}=\min{\pi(\theta \mid y), \pi(\theta' \mid y)=\pi(\theta \mid y)\alpha(\theta, \theta')}$

Mer at

\alpha(theta, theta') = min(1, \frac{\pi(\theta')\pi(y\mid \theta')/pi(y)}{pi(theta)pi(y|theta)pi(y)})=min(1, det samme med pi(y) strøket)

# MCMC i praksis
A: Burn-in: vi tar bort de første 5-10% av samplene

B: Trace plots skal se omtrent iid ut

C: Effective sample size  må være stor nok


## Kodeeksempel her
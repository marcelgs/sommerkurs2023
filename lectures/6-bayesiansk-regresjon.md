---
title: VI: Bayesiansk regresjon
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

$\newcommand{\distconv}{\overset{d}{\rightarrow}}$

$\wip{\text{WORK IN PROGRESS}}$

# VI: Bayesiansk regresjon
## Repetisjon: regresjon

Regresjonsuttrykk $y = \Phi w + \epsilon$ med:

- designmatrise $\Phi =
\begin{bmatrix}
\phi_0(x_1) & \dots & \phi_{m-1}(x_1) & \\
\vdots & \ddots & \vdots \\
\phi_{0}(x_n) & \dots & \phi_{m-1}(x_n) \\
\end{bmatrix}$

- koeffisienter $w = \begin{pmatrix}w_0 & \dots & w_{m-1}\end{pmatrix}^T$

- basisfunksjoner $\phi_j$ med $\phi_0 = 1$

- $\epsilon = \begin{pmatrix}\epsilon_0 & \dots & \epsilon_{n}\end{pmatrix}^T$, $\epsilon_i \iidsim \norm{0, \beta^{-1}}$


OLS: $\min\limits_w ||\Phi w-y||^2 = (\Phi w - y)^T (\Phi w -y)$ med løsning $\hat w = (\Phi^T \Phi)^{-1} \Phi^T y$

RLS: $\min\limits_w ||\Phi w-y||^2 + \lambda ||w||^2$ med løsning $\hat w_p = (\Phi^T \Phi + \lambda I)^{-1} \Phi^T y$


# Bayesiansk regresjon

Vi tar for oss eksempelet fra forrige gang:

Prior $w \thicksim \norm{m_0, S_0}$

Likelihood $y \thicksim \norm{\Phi w, \beta^{-1} I}$

Posterior: $w \mid y \thicksim \norm{m_n, S_n}$

Vi har da:

$m_n = S_n(S_0^{-1} + \beta \Phi^{-1} y)$

$S_n^{-1} = S_0^{-1} + \beta \Phi^T \Phi$

<!--velg m_0 = 0

Isotropisk S_0 = \alpha^{-1} I

m_n = \beta S_N \Phi^T y
S_n^{-1} = \alpha I + \beta \Phi^T \Phi-->

## Maksimum a posteriori-estimator

Hvilken verdi $w_{\text{MAP}}$ av $w$ maksimerer $\pi(w\mid y)$?

$\argmax\limits_w \log \pi(w \mid y) = \argmax\limits_w (\log \pi(y \mid w)+\log \pi(w)) = \argmax\limits_w (-\frac{\beta}{2} ||y-\Phi w||^2 - \frac\alpha2 ||w||^2) = \argmax\limits_w (||y-\Phi w||^2 + \frac{\alpha}{\beta}||w||^2)$

Dette gir en korrespondanse mellom MAP og RLS med $\lambda = \frac{\alpha}{\beta}$.

$\ex{\text{For en vilkårlig estimator, hva er forholdet mellom MAP-estimatoren og MLE?}}$

## Prediksjon
Vi ønsker ofte å finne fordelingen til et nytt datapunkt $Y'$ gitt eksisterende data $\set{(\bm x_i, y_i)}_{i\in{1,...,n}}$.



Litt ulik notasjon her. Vi velger konvensjonen der kun skriver at vi betinger på stokastiske variable (sett in mer her, mangler). Nevn uttrykket "posterior predictive".

$\pi(y' \mid y) = \int \pi(y', w \mid y)\ dw = \int \pi(y' \mid w) \pi(w\mid y)\ dw$, der første og andre faktor i det siste integralet er hhv likelihood og posterior

Vi vet at $y' \mid w \thicksim \norm(w^T \phi(x'), \beta^{-1})$

$w \mid y \thicksim \norm(m_n, S_n)$

Merk at $\phi(x')=(phi_0(x'), \dots, phi_n(x'))$

Der følger at $y \mid y' \thicksim \norm(m_n^T \phi(x'), \sigma_n^2(x'))$

der $\sigma_n^2(x') = 1/beta + phi(x')^T S_n phi(x')$

--kodeeksempel -- merk at alpha og beta er temmelig vilkårlig valgt her, men vi skal se på hvordan vi kan slippe det senere

## Hvordan velger vi $m$?

(graden i polynomet)

## Hvordan velger vi $\alpha$ og $\beta$?

Vi vil sette en prior på $\alpha$ og $\beta$. Da har vi ikke lenger conjugate priors, og må bruke MCMC.

## Modellsammenlining

Vi så tidligere at det er meningsløst å sammenlikne maximum likelihood-VERDIEN (da belønner vi overfitting).

Her sammenlikner vi (log) MARGINAL likelihood, og det går fint!

Altså: $\log \pi_m(y)$

I vårt tilfelle: $log \pi_m(y) = \frac{m}{2} \log \alpha + \frac{n}{2} \ log{\beta} - \frac\beta2 ||y-\Phi m_n ||^2 - \frac\alpha2 ||m_klarer ikke å se subscript||^2 -\frac12 \log|S_N^{-1}|(stemmer at det er én 1) -\frac n2 \log(2\pi)$

--Kodeekesmpel-- Kommenter de ulike verdiene av m (hvorfor nedgang i fit fra 1 til 2, økning til 3, fall videre?)


## Markovkjeder

I eksemplene vi har sett på så langt, har det gått relativt greit å regne ut normaliseringskonstanten $f(x) = \int f(x \mid \theta) \pi(\theta)\ d\theta$ i Bayes' teorem. I den virkelige verden er dette ofte beregningsmessig intraktabelt.

-- sett inn enkelt eksempel som viser MC for å estimere arealet til en figur --

$\defn{\text{Stokastisk prosess}}$

$\defn{\text{Markovantakelsen}} \P(X_{n+1} \mid X_n = x_n, \dots, X_0 = x_0)= \P(X_{n+1} \mid X_n = x_n)$\
"Fremtiden er uavhengig av fortiden, gitt nåtiden."

$\defn{\text{Markovkjede}}$ En stokastisk prosess som oppfyller Markovantakelsen.

$\defnn{\text{Transisjonsmatrise}}{P_n} = $  $(p_{ij})_n$ med $p_{ij} = \P(X_{n+1}=j \mid X_n = i)$

$\defn{\text{Homogen Markovkjede}}$ hvis $P_n = P_{n-1}\ \forall n$, altså hvis transisjonssannsynlighetene ikke avhenger av $n$

$\defn{\text{Stasjonær Markovkjede}}$ hvis $\P(X_n, \dots, X_{n+k})=\P(X_0, \dots, X_k)\ \forall n,k$

$\ex{\text{Vis at alle stasjonære Markovkjeder er homogene}}$

$\ex{\text{Kan du finne et eksempel på en ikke-stasjonær homogen Markovkjede?}}$

Eksempel: ${X_i \in \set{1,2,3}}$, definer noen sannsynligheter og be dem finne stationary distribution (hint: egenvektor). P = [[1/6 2/3 1/6][0 1 0][1/2 1/2 0]]

$\defn{\text{Kommuniserende tilstander }i, j}$


$\defn{\text{Kommunikasjonsklasser}}$

Kommunikasjonsklassene parterer (kan man si det på norsk) av mengden av tilstander

Merk at hver tilstand er i én og bare én kommunikasjonsklasse

defn irredusibel MC. Kun én kommunikasjonsklasse. Ønsker irreversibel, ellers kan vi ikke sample fra posterior.
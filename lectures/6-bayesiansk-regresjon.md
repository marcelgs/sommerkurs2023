---
title: VI: Bayesiansk regresjon
---


$\newcommand{\hdr}[4]{\color{#2}\boxed{\color{#2}\ #1\ \mid\ \textcolor{black}{#3} #4\ }\color{black}\ }$
$\newcommand{\defn}[1]{\hdr{D}{##fdc086}{#1}{}}$
$\newcommand{\defnn}[2]{\hdr{D}{##fdc086}{#1}{\ \mid\ \textcolor{black}{#2}}}$
$\newcommand{\thm}[1]{\hdr{T}{##7fc97f}{#1}{}}$
$\newcommand{\ex}[1]{\hdr{E}{##ae9ed4}{#1}{}}$
$\newcommand{\danger}[1]{\hdr{\textbf{☡}}{##cc0000}{#1}{\textcolor{##cc0000}{\mid \textbf{☡}}}}$
$\renewcommand{\|}{|}$

$\renewcommand{\P}{\mathbb{P}}$
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\iidsim}{\overset{\mathrm{i.i.d.}}{\sim}}$
$\newcommand{\deldel}[1]{\frac{\partial}{\partial #1}}$
$\newcommand{\norm}[1]{\mathcal{N}(#1)}$
$\renewcommand{\epsilon}{\varepsilon}$


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

--- kodeeksempel ---

OLS: $\min\limits_w ||\Phi w-y||^2 = (\Phi w - y)^T (\Phi w -y)$ med løsning $\hat w = (\Phi^T \Phi)^{-1} \Phi^T y$

RLS: $\min\limits_w ||\Phi w-y||^2 + \lambda ||w||^2$ med løsning $\hat w_p = (\Phi^T \Phi + \lambda I)^{-1} \Phi^T y$


# Bayesiansk regresjon

Vi tar for oss eksempelet fra forrige gang:

Prior w \thicksim N(m_0, S_0)

Likelihood y \thicksim N(\Phi w, \beta^-1 I)

Posterior (beviste sist): w \mid y \thicksim N(m_n, s_n)

m_n = S_n(S_0^{-1} 0 \beta \Phi^{-1} y)
S_n^{-1} = S_0^{-1} + \beta \Phi^T \Phi

velg m_0 = 0
Isotropisk S_0 = \alpha^{-1} I

m_n = \beta S_N \Phi^T y
S_n^{-1} = \alpha I + \beta \Phi^T \Phi

## MAP

Hvilken verdi $w_{\text{MAP}}$ av $w$ maksimerer $\pi(w\mid y)$?

argamx_w log \pi(w \mid y) = argmax_w (log \pi(y \mid w)+log \pi(w)) = argmax_w (-\frac{\beta}{2} ||y-\Phi w||^2 - \alpha/2 ||w||^2) = argmax_w /(||y-\Phi w||^2 + \frac{\alpha}{\beta}||w||^2)

Dette gir en korrespondanse mellom MAP og RLS med $\lambda = \frac{\alpha}{\beta}$

## Prediksjon
Ny input $x'$

Ønsker å finne fordelingen til $y'$ gitt data {x,y}

Litt ulik notasjon her. Vi velger konvensjonen der kun skriver at vi betinger på stokastiske variable (sett in mer her, mangler)

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

Bayes: $\pi(\theta \mid y) = \frac{\pi(y \mid \theta)\pi(\theta)}{\pi (y)}$

Ofte ikke en fin form på normaliseringskonstanten

$\defnn{\text{Markovkjede}}{}$
Sekvens av stokastiske variabler som tilfredstiller Markov assumption:
$\pi(X_n \mid X_{n-1} = x_{n-1}, \dots, X_1 = x_1)= \pi(X_n \mid X_{n-1} = x_{n-1})$

$\defn{\text{Homogen Markovkjede}}$ hvis $p_{ij} = \P(X_{n+1}=j \mid X_n = i)$ ikke avhenger av $n$

$\defnn{\text{Transisjonsmatrise}}{P}$ = $(p_{ij})$

Eksempel: ${X_i \in \set{1,2,3}}$, definer noen sannsynligheter og be dem finne stationary distribution (hint: egenvektor). P = [[1/6 2/3 1/6][0 1 0][1/2 1/2 0]]

$\defn{\text{Kommuniserende tilstander }i, j}$


$\defn{\text{Kommunikasjonsklasser}}$

Kommunikasjonsklassene parterer (kan man si det på norsk) av mengden av tilstander

Merk at hver tilstand er i én og bare én kommunikasjonsklasse

defn irredusibel MC. Kun én kommunikasjonsklasse. Ønsker irreversibel, ellers kan vi ikke sample fra posterior.
---
title: II: Likelihood-funksjonen, Fisherinformasjon og deltametoden
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
$\newcommand{\bm}{\boldsymbol}$

# II: Likelihood-funksjonen, Fisherinformasjon og deltametoden
## Grunnleggende konsepter
Modell: $X_1, \dots, X_n \iidsim f_X(x;\theta)$[^1]\
Data (realiseringer, observasjoner): $x_1, \dots, x_n$

Sannsynlighetsteori: modell $\rightarrow$ data\
Statistikk: data $\rightarrow$ modell

Siden antikkens tid har en grunnleggende forståelse av sannsynlighet gjort nytte for seg innen [forsikring](https://en.wikipedia.org/wiki/History_of_insurance), [kryptoanalyse](https://en.wikipedia.org/wiki/Al-Kindi#Cryptography) og (selvsagt) [lykkespill](https://en.wikipedia.org/wiki/De_vetula#Non-poetic_content). Det aksiomatiske grunnlaget for feltet kom derimot først på plass i 1933 da Andrej N. Kolmogorov formulerte sannsynlighetsaksiomene vi møtte i forrige forelesning. Epistemologene strides fortsatt om hvordan sannsynligheter skal forstås, men vi skyver den diskusjonen under teppet og nøyer oss med superkorte forklaringer av de to dominerende paradigmene:

Frekventistisk sannsynlighetsteori: $\theta$ betraktes som bestemt, men ukjent. Sannsynlighet forstås som andeler av utfallene når et eksperiment gjentas mange ganger[^2]. Frekventistiske metoder går stort sett ut på å konstruere ulike estimatorer med ønskede egenskaper, der *maximum likelihood*-estimatoren er den mest fremtredende.

Bayesiansk sannsynlighetsteori: $\theta$ betraktes som en stokastisk variabel. Sannsynlighet forstås som en grad av (epistemisk) usikkerhet. Bayesianske metoder er konseptuelt mye enklere - vi må "bare" definere en *likelihood* $f(x \mid \theta)$ og en *prior* $\pi (\theta)$ (vi kommer tilbake til hva dette betyr senere), og så er vi i prinsippet ferdige.

## Likelihood-funksjonen


Anta at vi har $n$ uavhengige realiseringer $x_1, \dots, x_n$ av en stokastisk variabel $X$.

$\defnn{\text{Likelihood}}{\mathcal{L_n}(\theta)} = \prod_1^n f_X(x_i; \theta)$

$\defnn{\text{Log-likelihood}}{\ell_n(\theta)} = \log \mathcal{L_n} = \sum_1^n \log f_X(x_i;\theta)$

Siden vi antok uavhengighet, ser vi at likelihood-funksjonen rett og slett er simultanfordelingen til de uavhengige og identisk fordelte variablene $X_1, \dots, X_n$. Merk at vi her ser på uttrykket som en funksjon av parameteren $\theta$. Da blir det naturlig å spørre oss hvilken verdi av $\theta$ som maksimerer sannsynligheten for de observerte verdiene:

$\defnn{\text{Maximum likelihood-estimatoren (MLE)}}{\hat{\theta}_\text{MLE}} = $ $\argmax\limits_{\theta \in \Theta} \mathcal{L}_n(\theta) = $
$\argmax\limits_{\theta \in \Theta} \mathcal{\ell}_n(\theta)$

$\ex{X_1, ..., X_n \iidsim \operatorname{Bernoulli}(\theta)\text{. Vis at }\hat{\theta} = \bar{y} = \frac{1}{n}\sum_1^n x_i .}$

$\ex{X_1, ..., X_n \iidsim \norm{\mu, \sigma^2}\text{. Finn MLE }\hat\mu\text{ og }\hat\sigma^2.\text{ Er estimatorene forventingsrette?}}$

## Digresjon: matrisederivasjon

I flervariabeltilfellet blir $\mathcal{L}(n)$ en matrise. Vi repeterer noen regler for derivasjon av matriser som vi kommer til å få bruk for i denne og senere forelesninger:

La $A$ være en matrise som avhenger av $x$: $A = A(x)$.

$$\begin{gather*}

A^{-1}A = I_n \\

\deldel{x} A^{-1}A = 0 \\

\deldel{x} A^{-1} A + A^{-1}\deldel{x}A = 0 \\

\deldel{x} A^{-1} = -A^{-1} \deldel{x} A^{-1} \tag{1}

\end{gather*}$$

Vi tar resten av resultatene vi trenger [herfra](https://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf):

$$\deldel{\bm x} \bm x ^T A \bm x = (A + A^T)\bm x \overset{\text{A symm.}}{=} 2 A \bm x \tag{2}$$

$$\tr(ABC)=\tr(CAB) \tag{3}$$

$$\deldel{A}(\tr(AB)) = B^T \tag{4}$$

$$\deldel{A}(\log |A|) = (A^{-1})^T = (A^T)^{-1} \tag{5}$$

$$\deldel{A} (A^{-1})= -A^{-2} \tag{6}$$







## MLE for $\bm{\mu}$ og $\Sigma$ i multivariat normalfordeling

Som den univariate er den multivariate normalfordelingen parametrisert ved forventning og (ko)varians.

En vektor av stokastiske variabler $\mathbf{X}=(X_1, \dots, X_n)^T$ har kovariansmatrise $\Sigma$ med $\Sigma_{i,j}=\operatorname{Cov}(X_i, X_j)$. Merk at $\Sigma_{i,i} = \operatorname{Cov}(X_i, X_i) = \mathbb{V}[X_i]$.

$\Sigma$ må være symmetrisk og *positiv definitt*. Ser du hvorfor? Hvilke verdier kan $|\Sigma|$ ha?

$\defn{\text{Positiv definitt matrise }A_{n\times n}}\ $ $\bm{a}^TA\bm{a}\geq 0\ \ \forall \bm{a} \in \R^n$ 

$\defnn{\text{Multivariat normalfordeling}}{\mathcal{N_p}(\bm{\mu}, \Sigma)}$ har tetthet $f(\bm{x};\bm{\mu}, \Sigma)=(2\pi)^{\frac{1}{2}p}|\Sigma|^{-\frac{1}{2}}\exp(-\frac{1}{2}(\bm{x}-\bm{\mu})^T\Sigma^{-1}(\bm{x}-\bm{\mu}))$.

$\ex{\bm x_1, ..., \bm x_n \iidsim \mathcal{N}_p(\bm{\mu}, \Sigma)\text{. Finn }\bm{\hat\mu}\text{ og }\hat{\Sigma}.}$

Som nevnt over må vi sørge for at $\hat\Sigma$ blir symmetrisk og positiv definitt. Her velger vi i første omgang å glemme dette, og håper at vi har flaks og kravet likevel blir oppfylt.

$$\begin{gather*}

\ell_n (\bm\mu, \Sigma) = 

\sum_{i=1}^n\left( -\frac{1}{2} (\bm{x_i-\bm{\mu}})^T\Sigma^{-1}(\bm{x_i-\bm{\mu}}) - \frac{1}{2}\log |\Sigma| - \frac{1}{2} p \log 2\pi\right) = \\

-\frac{1}{2} \sum_{i=1}^n \left( (\bm{x_i-\bm{\mu}})^T\Sigma^{-1}(\bm{x_i-\bm{\mu}}) \right) + \frac{n}{2}\log |\Sigma^{-1}| - \frac{n}{2} p \log 2\pi

\end{gather*}$$

$$

\deldel{\bm\mu} \ell_n (\bm\mu, \Sigma) \overset{\text{(2)}}{=} -\frac{1}{2} \sum_{i=1}^n\Sigma^{-1}(\bm x_i - \bm\mu) = - \left(\sum_{i=1}^n \Sigma^{-1}\bm{x_i}\right)-n\Sigma^{-1}\bm{\mu}= \bm 0

$$

Siden $\Sigma^{-1}$ er inverterbar, følger det at $\sum_{i=1}^n \bm{x_i}=n\bm{\mu}$, altså har vi $\bm{\hat\mu}=\bar{\bm x}$.

$$
\deldel{\Sigma^{-1}} \ell_n (\bm\mu, \Sigma) =  -\frac{1}{2} \sum_{i=1}^n \left( \deldel{\Sigma^{-1}} (\bm{x_i-\bm{\mu}})^T\Sigma^{-1}(\bm{x_i-\bm{\mu}}) \right) + \frac{n}{2} \deldel{\Sigma^{-1}} \log |\Sigma^{-1}|
$$

$\tr$ angir diagonalsummen. Merk at $\tr(\bm a^T A \bm a) = \bm a^T A \bm a$, siden $\bm a^T A \bm a$ er en skalarverdi. Dermed har vi:

$$\begin{aligned}

\deldel{\Sigma^{-1}}(\bm{x_i}-\bm\mu)^T \Sigma^{-1} (\bm{x_i}-\bm\mu) &=\\

\deldel{\Sigma^{-1}}\tr((\bm{x_i}-\bm\mu)^T \Sigma^{-1} (\bm{x_i}-\bm\mu)) &\overset{\text{(3)}}=\\

\deldel{\Sigma^{-1}}\tr(\Sigma^{-1}(\bm{x_i}-\bm\mu) (\bm{x_i}-\bm\mu)^T) &\overset{\text{(4)}}=\\

((\bm{x_i}-\bm\mu) (\bm{x_i}-\bm\mu)^T)^T &= \\

(\bm{x_i}-\bm\mu) (\bm{x_i}-\bm\mu)^T

\end{aligned}
$$


$$

\deldel{\Sigma^{-1}} \log |\Sigma^{-1}| \overset{\text{(5)}}= ((\Sigma^{-1})^{-1})^T = \Sigma^T = \Sigma

$$

$$
\deldel{\Sigma^{-1}} \ell_n (\bm\mu, \Sigma)  = 0 \Rightarrow \Sigma = \frac 1 n \sum_{i=1}^n (\bm x_i-\bm\mu)(\bm x_i -\bm\mu)^T \coloneqq \hat\Sigma
$$

Siden $\Sigma^{-1}$ er unik (det finnes en bijeksjon som mapper $\Sigma$ til $\Sigma^{-1}$), følger det at $\hat\Sigma$ maksimerer $\ell_n$ (og dermed $\mathcal{L}(n)$).

Til slutt må vi verifisere at $\hat{\Sigma}$ er symmetrisk og positiv definitt:

$\ex{\text{Vis at }\hat\Sigma\text{ er symmetrisk og positiv definitt.}}$[^3]



Etter litt omstendelig algebra har vi altså funnet at MLE for parametrene til normalfordelingen er identisk med gjennomsnittet og kovariansen i utvalget. Er dette alltid tilfelle? Følg med i neste episode!

Neida, det skal du få finne ut av selv:

$\defnn{\text{Eksponensialfordeling}}{\operatorname{Exp}(\lambda)}$ $f(x)=\lambda x^{-\lambda x}$, $x\in[0,\infty)$, $\lambda \in [0,\infty)$

$\ex{x_1, \dots, x_n \iidsim \operatorname{Exp}(\lambda)\text{. Finn } \hat\lambda.}$

$\defnn{\text{Gammafordeling}}{\operatorname{Gamma}(\alpha, \beta)}$ $f(x)=\frac{\beta^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\beta x}$, $x \in (0,\infty)$, $\alpha \in (0,\infty)$, $\beta \in (0,\infty)$

$\danger{\text{Gammafordelingen kan parametriseres på to ulike måter. Sjekk alltid hvilken parametrisering som brukes.}}$

$\ex{x_1, \dots, x_n \iidsim \operatorname{Gamma}(\alpha, \beta)\text{. Finn } \hat\beta.}$

## Fisherinformasjon

$\wip{\text{Denne delen må motiveres - fyll ut med flere detaljer og et eksempel!}}$

$\defnn{\text{Fisherinformasjon}}{\mathcal{I}(\theta)} = -\E\left[\deldel\theta^T \deldel\theta\ \ell(\theta)\right]$ [^4]

$\thm{\text{Asymptotisk normalitet for MLE}}$ $\sqrt{n}(\hat\theta_n - \theta^*)\overset{d}{\rightarrow}\norm{0, \mathcal{I}(\theta^*)^{-1}}$, der $n$ er utvalgsstørrelsen og $\theta^*$ er den (ukjente) sanne verdien av $\theta$.[^5]

Se [her](https://gregorygundersen.com/blog/2019/11/28/asymptotic-normality-mle/) for bevis og et eksempel.

<!--Ex: finn asymptotisk fordeling til a hat/b hat^2

Fact: Var(Y\thicksim gamma) = a/b^2-->

## Deltametoden

Vi møter ofte situasjoner hvor vi må utlede egenskapene til transformasjoner av estimatorer eller andre stokastiske variabler. Her er deltametoden et nyttig verktøy for å vise asymptotisk normalitet og finne variansen til den transformerte variabelen. Dette er for eksempel nyttig når vi skal konstruere konfidensintervaller for punktestimater.


<!-- h må vel være glatt? Tror beviset bruker en rekkeutvikling. Sjekk dette! -->

$\thm{\text{Deltametoden}}$
Anta at vi har en estimator $\hat\theta$ slik at $\sqrt{n}(\hat\theta_n-\theta)\overset{d}{\rightarrow}\mathcal{N}_p(\bm0,\Sigma)$ for en eller annen $\Sigma$. Vi har også en funksjon $h: \R^p \rightarrow \R$.

Da følger det at $\sqrt{n}(h(\hat\theta_n)-h(\theta))\overset d\rightarrow \mathcal{N}_p (\bm0, \underset{[n \times p]}{\nabla h(\theta_n)^T}\ \underset{[p\times p]}{\Sigma}\ \underset{[p\times n]}{\nabla h(\theta)})$

I det univariate tilfellet reduseres det siste uttrykket til $\mathcal{N}\left(0,\sigma^2 \left(\frac{dh(\theta)}{d\theta}\right)^2\right)$

$\ex{\text{Gammafordeling, }h(\alpha,\beta)=\frac\alpha{\beta^2}}$

$\nabla h = \begin{pmatrix} \frac 1 {\beta^2}\\ \frac{-2\alpha}{\beta^3} \end{pmatrix}$

I [kodeeeksempelet](https://colab.research.google.com/drive/1hdqR6nb6lyQM6MpMnjFsFx5TSkO4rIau?usp=sharing) utforsker vi dette eksempelet og bruker deltametoden til å konstruere et konfidensintervall.

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

[^1]: $\mathrm{i.i.d.}:$ independent and identically distributed. Du *kan* ([ifølge Wikipedia](https://no.wikipedia.org/wiki/Uavhengige,_identisk_fordelte_variabler)) skrive $\mathrm{u.i.f.}$ ("uavhengige og identisk fordelte") på norsk, men da ser folk rart på deg.

[^2]: Denne teoretiske antakelsen er det ofte vanskelig å implementere i praksis. Lykke til med å folk med på å nullstille verden til 1990 $n$ ganger for at du skal finne ut hvordan inflasjon og arbeidsledighet henger sammen.

[^3]: [Fasit](https://stats.stackexchange.com/questions/52976/is-a-sample-covariance-matrix-always-symmetric-and-positive-definite)

[^4]: Underlagt [visse](https://en.wikipedia.org/wiki/Fisher_information#Regularity_conditions) (regularitets)betingelser og vilkår. Ved bruk av definisjonen godtar du nevnte betingelser og vilkår.

[^5]: $\overset{d}{\rightarrow}$ betyr at en følge (her $(\hat\theta_n)_{n\in\N}$) av stokastiske variabler *konvergerer i fordeling* ("convergence in distribution"), som uformelt betyr at den fordelingsfunksjonen definert av $\hat\theta_n$ ligger vilkårlig nært fordelingsfunksjonen definert av $\theta^*$ når $n$ er stor nok. Vi går ikke inn på detaljene her, men [Wikipedia](https://en.wikipedia.org/wiki/Convergence_of_random_variables#Convergence_in_distribution) har en grei forklaring. Dette er den typen konvergens vi kjenner fra sentralgrensetoremet.

<iframe src="https://docs.google.com/forms/d/e/1FAIpQLScyF8YFFvS9C_m7fGVgf47wZaJS75MEBUb1SB7dGLRiCwK13w/viewform?embedded=true" width="640" height="553" frameborder="0" marginheight="0" marginwidth="0">Loading…</iframe>

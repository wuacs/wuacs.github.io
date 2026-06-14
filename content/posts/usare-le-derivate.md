+++
date = '2026-05-16T10:16:02+02:00'
draft = false
title = 'Usare le derivate'
tags= ['italian', 'inequalities', 'shor']
+++

A metà giugno 2026 stavo ripassando la dimostrazione sulla correttezza dell'algoritmo di Shor, quando mi sono imbattuto su questo (leggermente modificato ed incompleto) esercizio:


> Siano $|\alpha|<\beta< \frac{\pi}{K}, \beta >0, K \in \mathbb{N}$ allora dimostra che $$\frac{\sin^2(K\alpha)}{\sin^2(\alpha)}>\frac{\sin^2(K\beta)}{\sin^2(\beta)}$$

Poiché stiamo elevando al quadrato il $\sin$ la disequazione sopra è soddisfatta quando:
$$
\begin{align}
 \left| \frac{\sin(K\alpha)}{\sin(\alpha)}\right| >& \left|\frac{\sin(K\beta)}{\sin(\beta)}\right|\\ 
 \frac{\sin (K |\alpha|)}{\sin(|\alpha|)}>&\frac{\sin(K \beta)}{\sin(\beta)}
\end{align}
$$

dove per derivarci $(1) \iff (2)$ abbiamo sfruttato principalmente il vincolo $\beta <\pi/K$:
- La parte a sinistra è conseguenza della definizione di modulo
- La parte a destra invece usa l'ipotesi $\beta < \pi/K$; abbiamo $\sin(K\beta)<\sin(\pi)$ quindi $\sin(K\beta)$ ha lo stesso segno di $\sin(\beta)$: possiamo rimuovere il modulo

Ora possiamo riformulare il problema in questo modo:

> Siano $0<x < y < \frac{\pi}{K}\in \mathbb{R}, K \in \mathbb{N}$ dimostra che $$\frac{\sin(K x)}{\sin(x)}>\frac{\sin(Ky)}{\sin(y)}$$

Una divisione tra seni: sembra particolarmente difficile.
Qual è una funzione che "trasforma" le divisioni?
Il logaritmo.
Ricordiamo:
> $$\ln(x/y)=\ln(x)-\ln(y)$$

Ma applicare il logaritmo ad ambo i lati presuppone avere la certezza che queste quantità siano positive. Per quello che stiamo per fare, ci basta considerare l'intervallo $(0, \pi/K)$.

> Lemma: $$\forall x \in (0, \pi/K), f(x)=\frac{\sin(K x)}{\sin(x)} >0 $$
{ #lemma-1 }

> Dimostrazione:
>
> L'argomento del denominatore si trova in $(0, \pi/K)$, siccome $K > 0$, esso rappresenta sempre un angolo con l'origine tra $(0, \pi)$, i.e., ha $\sin$ positivo. 
>L'argomento del $\sin$ al numeratore invece rappresenta un angolo tra $(0, \pi)$.

Oltre a "spezzare" le divisioni il logaritmo ha un'altra interessante proprietà: è monotona.
Questo significa che se scopro che $\ln(f(x))$ è monotona crescente (in $(0, \pi/K)$, perché lì *solo* ho dimostrato essere definita) allora (2) è falsa: perché $$x < y \xrightarrow[\text{monotonia crescente}\ \ln \circ f]{}\ln(f(x))<\ln(f(y)) \xrightarrow[\text{monotonia}\ \ln ]{} f(x) < f(y)$$

Stiamo quindi sfruttando la *monotonia* di $\ln$ per inferire cosa succeda da $f(x)$ a $f(y)$ perché sappiamo che $x < y$ per ipotesi.

Dimostriamo quindi che $\ln \circ f$ è monotona decrescente:

> Lemma: $$\forall x,y \in (0, \pi/K), x < y \implies \ln (f(x))>\ln(f(y))$$

> Dimostrazione:
>
> per capire l'andamento della funzione (da qui il nome dell'articolo) calcoliamo la derivata di $\ln \circ f(x)$:
>$$\begin{align*}
((\ln \circ f)(x))' &=\\
\ln'(\sin(Kx))-\ln'(\sin(x))&=\\
\frac{(\sin(Kx))'}{\sin(Kx)}-\frac{\sin'(x)}{\sin(x)}&=\\
K\cot(Kx)-\cot(x)\end{align*}\
$$ 
>
>Ora riscriviamo l'espressione come $$1/x(Kx\cot(Kx)-x\cot(x))\tag{3}$$
>Ora ci basta cercare la derivata della funzione $g(x)=x\cot x$ su $(0, \pi)$(e quindi varrà per $(0, \pi/K)$):
>$$
\cot(x)-\frac{x}{\sin^2(x)}
$$
>Moltiplichiamo ora per $\sin^2(x)$, la quantità nuova manterrà il segno della derivata:
>$$
\sin(x)\cos(x)-x<_{x>\sin(x)}0
$$
>Quest'ultima disuguaglianza vale perché $\sin(x)\cos(x) \le \sin(x) < x$ vale su $(0, \pi)$.
>
>Dunque, in (3) abbiamo $$\underbrace{1/x}_{>0}\underbrace{(g(Kx)-g(x))}_{<0}<0$$

L'unica cosa che manca è dimostrarsi che $x < y < \pi/K$ altrimenti non possiamo usare il [lemma](#lemma-1).

Nel caso dell'algoritmo di Shor, giusto per dare del contesto, avevamo da dimostrare che $$y=\frac{r \pi}{2^{L+1}}\le \frac{\pi}{J_k}$$ 
dove 

- r rappresenta il periodo di una funzione
- L rappresenta un upper-bound del periodo, cioè $r < 2^{L/2}$
- $J_k\le \lfloor \frac{2^{L}-1}{r} \rfloor+1$ rappresenta il numero massimo di volte un certo elemento dell'immagine appare applicando l'oracolo su un registro di dimensione $2^L$. 

E veniva immediatamente:
$$
\frac{r\pi}{2^{L+1}}=\frac{\pi}{\frac{2^{L+1}}{r}}<\frac{\pi}{\frac{2^L}{r}+1}<\frac{\pi}{J_k}
$$


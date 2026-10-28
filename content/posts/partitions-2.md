+++
date = '2026-10-26'
layout = 'blog'
katex = true
showDate = true
title = 'Partitions in number fields 2: The asymptotics for integer partitions'
summary = 'The second post in the series, giving useful context for what comes next.'
categories = ['featured']
tags = ['math-heavy','partitions']
+++

In the [first post](https://zinmik.github.io//math-blog/posts/partitions-1/) of the series, we discussed how the notion of integer partition can be extended to number fields. Our ultimate goal is to give an exposition of the asymptotic formula for the number of these partitions. But before we do that, we will review the formula for $p(n)$, the integer partition counting function. Then we will be able to better appreciate the difficulties that come with trying to generalize it.

Famously, the precise asymptotics for $p(n)$ was obtained by Hardy and Ramanujan in 1918. For a positive integer $k$, let
\[
    P_k(n) = \frac{1}{2\sqrt{2}}\sqrt{k}A_k(n)\frac{d}{dn}\left(\frac{e^\frac{C\lambda_n}{k}}{\lambda_n}\right)
\]
with $C = \pi\sqrt{2/3}$ and $\lambda_n=\sqrt{n-\frac{1}{24}}$, where
\[
    A_k(n) = \sum_{\substack{0\leq h < k\\gcd(h,k)=1}}\omega_{h,k}e^\frac{-2\pi i nh}{k}
\]
and $\omega_{h,k}$ denotes a certain $24$-th root of unity.

**Theorem** (Hardy–Ramanujan). For an arbitrary constant $\alpha>0$, we have
\[
    p(n) = \sum_{k=1}^{\alpha\sqrt{n}}P_k(n)+O_\alpha\left(n^{-\frac{1}{4}}\right).
\]

The dominant term is $P_1(n)$, which shows
\[
    p(n) \sim \frac{e^{C\sqrt{n}}}{4n\sqrt{3}}.
\]

The formula is not only asymptotic, but also exact: When $\alpha$ is fixed, the error term will drop below $\frac{1}{2}$ for large enough $n$, so $p(n)$ is the integer nearest to the main term. However, the error term is not effective, which means that it is not clear how large we need to take $\alpha$ for a given $n$. This point was lost on me for a long time. We can truncate the series after a finite number of terms in an attempt to calculate $p(n)$ but to the best of my knowledge, it is not feasible to leverage the proof of the Hardy–Ramanujan theorem for an effective error term. Luckily, we have no need to do that. Rademacher expressed $p(n)$ by a convergent series in his 1927 paper. And his result can be used to obtain a completely explicit bound for the remainder in the Hardy–Ramanujan formula!

**Theorem** (Rademacher).
\[
    p(n) = \frac{1}{\pi\sqrt{2}}\sum_{k=1}^{\infty}\sqrt{k}A_k(n)\frac{d}{dn}\left(\frac{\sinh\left(\frac{C\lambda_n}{k}\right)}{\lambda_n}\right).
\]

As a corollary [2, (8.3)], we have
\[
    p(n) = \frac{1}{2\pi\sqrt{2}}\sum_{k=1}^N \sqrt{k}A_k(n)\frac{d}{dn}\left(\frac{e^\frac{C\lambda_n}{k}}{\lambda_n}\right)+R(n,N),
\]
where
\[
    \begin{aligned}
        |R(n,N)| &\leq \frac{44\pi^2}{225\sqrt{3}}N^{-\frac{1}{2}}+\frac{\pi\sqrt{2}}{75}\left(\frac{N}{n-1}\right)^{\frac{1}{2}}\sinh\left(\frac{C\sqrt{n}}{N}\right)\\
        &+\frac{1}{2\sqrt{3}}\frac{(N+1)^{\frac{3}{2}}}{n-1}e^{-\frac{C(n-1)^{\frac{1}{2}}}{N}}\left(\frac{1}{3}+\frac{\sqrt{3}}{5\pi\sqrt{2}}\frac{N+1}{(n-1)^{\frac{1}{2}}}\right).
    \end{aligned}
\]
There is a similar bound for the error when we truncate Rademacher's series instead.

The proof of the Hardy–Ramanujan theorem is an application of the circle method. In fact, it was precisely this application for which the circle method was developed. Consider the generating function
\[
    F(q) = \sum_{n=0}^{\infty}p(n)q^n = \prod_{n=1}^{\infty}\frac{1}{1-q^n}
\]
convergent for $|q|<1$. By Cauchy's integral formula, we have
\[
    p(n) = \frac{1}{2\pi i}\int_{\mathcal{C}} \frac{F(q)}{q^{n+1}}dq,
\]
where $\mathcal{C}$ is a circle centered at the origin with radius $\rho < 1$. Next, we divide the path of integration into so-called *Farey arcs*. For a positive integer $N$, the set $F_N$ of *Farey fractions* of order $N$ consists of the reduced fractions in the interval $[0,1]$ with denominators $\leq N$. For example,
\[
    F_5 = \left\{0,\frac{1}{5},\frac{1}{4},\frac{1}{3},\frac{2}{5},\frac{1}{2},\frac{3}{5},\frac{2}{3},\frac{3}{4},\frac{4}{5},1\right\}.
\]
If $\frac{h_0}{k_0}$, $\frac{h}{k}$, and $\frac{h_1}{k_1}$ are three successive fractions in $F_N$, then we let
\[
    \begin{aligned}
        \theta'_{0,1}& = \frac{1}{N+1},\\
        \theta'_{h,k}& = \frac{h}{k}-\frac{h_0+h}{k_0+k},\\
        \theta''_{h,k}& = \frac{h_1+h}{k_1+k}-\frac{h}{k}.
    \end{aligned}
\]
The Farey arcs are defined by $C_{h,k} = \left\{e^{2\pi i\tau}:-\theta_{h,k}'+\frac{h}{k}\leq \tau \leq \theta_{h,k}''+\frac{h}{k}\right\}$. Hence, $e^{\frac{2\pi i h}{k}}$ is the midpoint of $C_{h,k}$. Now
\[
    \begin{aligned}
        p(n)& = \sum_{k=1}^N\sum_{\substack{0\leq h < k\\\gcd(h,k)=1}}\frac{1}{2\pi i}\int_{C_{h,k}}\frac{F(q)}{q^{n+1}}dq\\
        & = \rho^{-n}\sum_{k=1}^N\sum_{\substack{0\leq h < k\\\gcd(h,k)=1}}\int_{-\theta'_{h,k}+\frac{h}{k}}^{\theta_{h,k}''+\frac{h}{k}}F\left(\rho e^{2\pi i\tau}\right)e^{-2\pi i n\tau}d\tau.
    \end{aligned}
\]
We choose $\rho = e^{-\frac{2\pi}{N^2}}$.

The reason why we did this setup is that we have a good information about the behavior of $F(q)$ near the point $e^{\frac{2\pi i h}{k}}$. This is directly tied to the fact that $F(q)$ behaves well under modular transformations. Let $\mathbb{H}=\{\tau\in\mathbb{C}:\operatorname{Re}(\tau)>0\}$ be the upper half-plane of the complex plane. There is a close connection between $F(q)$ and the *Dedekind $\eta$-function* defined for $\tau\in\mathbb{H}$ by
\[
    \eta(\tau) = q^\frac{1}{24}\prod_{n=1}^{\infty}\left(1-q^n\right),\qquad q=e^{2\pi i\tau}.
\]
Namely, $F(q) = q^\frac{1}{24}\eta^{-1}(\tau)$. The $\eta$-function is a modular form of weight $\frac{1}{2}$ on the group $\operatorname{SL}_2(\mathbb{Z})$ with a multiplier system, that is to say, it satisfies the following functional equation.

**Proposition.** For $\begin{pmatrix}a&b\\c&d\end{pmatrix}\in\operatorname{SL}_2(\mathbb{Z})$ with $c>0$ and $\tau\in\mathbb{H}$, we have
\[
    \eta\left(\frac{a\tau+b}{c\tau+d}\right) = \varepsilon(a,b,c,d)(c\tau+d)^\frac{1}{2}\eta(\tau),
\]
where
\[
    \varepsilon(a,b,c,d) = \exp\left(\pi i\left(\frac{a+d}{12c}+s(-d,c)-\frac{1}{4}\right)\right)
\]
and
\[
    s(h,k) = \sum_{r=1}^{k-1}\frac{r}{k}\left(\frac{hr}{k}-\left\lfloor\frac{hr}{k}\right\rfloor-\frac{1}{2}\right).
\]

The quantity $s(h,k)$ is called a *Dedekind sum*. Particular cases of the transformation formula are
\[
    \eta(\tau+1) = e^\frac{\pi i}{12}\eta(\tau),\qquad \eta\left(-\frac{1}{\tau}\right) = (-i\tau)^{\frac{1}{2}}\eta(\tau).
\]
There are two possible approaches to the proof of this proposition: Either we establish the general transformation formula directly, or we establish the special formula for $\eta(-1/\tau)$ first and then take advantage of the fact that the modular group is generated by the two matrices
\[
    T=\begin{pmatrix}1&1\\0&1\end{pmatrix},\qquad S=\begin{pmatrix}0&-1\\1&0\end{pmatrix}.
\]
A detailed exposition of the modularity of the $\eta$-function may be found in Chapter 3 of Apostol's book [1], with the second approach in the Supplement to Chapter 3. We will return to the proof of the special case in one of the later posts. For now, we will show that the modularity of $\eta(\tau)$ is equivalent to the modularity of $F(q)$.

**Lemma.** Let $k$ be a positive integer and $0\leq h < k$ such that $\gcd(h,k)=1$. Define $h'$ as the solution to the congruence $hh'\equiv 1\pmod{k}$. The generating function $F(q)$ satisfies the functional equation
\[
    F\left(e^{2\pi i\frac{h+iz}{k}}\right) = \omega_{h,k}\sqrt{z}\exp\left(\frac{\pi\left(z^{-1}-z\right)}{12k}\right)F\left(e^{2\pi i\frac{h'+iz^{-1}}{k}}\right)
\]
for $\operatorname{Re}(z)>0$, where
\[
    \omega_{h,k} = e^{\pi i s(h,k)}.
\]

**Proof.** Let $\tau=\frac{h+iz}{k}$ and $\tau'=\frac{h'+iz^{-1}}{k}$. The matrix
\[
    \gamma = \begin{pmatrix}h'&-\frac{hh'+1}{k}\\k&-h\end{pmatrix}
\]
belongs to $\operatorname{SL}_2(\mathbb{Z})$, and we have $\gamma\tau = \tau'$ since
\[
    \gamma\tau = \frac{h'\frac{h+iz}{k}-\frac{hh'+1}{k}}{k\frac{h+iz}{k}-h} = \frac{h'iz-1}{kiz} = \frac{h'+iz^{-1}}{k} = \tau'.
\]
Using the functional equation from $\eta(\tau)$ and $k\tau-h=iz$, we obtain
\[
    \begin{aligned}
        F\left(e^{2\pi i\tau}\right)&=e^{\frac{\pi i \tau}{12}}\eta^{-1}(\tau) = e^{\frac{\pi i \tau}{12}}\varepsilon\left(h',-\frac{hh'+1}{k},k,-h\right)(k\tau-h)^{\frac{1}{2}}\eta^{-1}(\tau')\\
        &=\exp\left(\frac{\pi i(\tau-\tau')}{12}\right)\exp\left(\pi i\left(\frac{h'-h}{12k}+s(h,k)\right)\right)\sqrt{z}F\left(e^{2\pi i\tau'}\right).
    \end{aligned}
\]
<div style="text-align: right;">$\square$</div>

Clearly, one can also start from the functional equation for $F(q)$ and end with that for $\eta(\tau)$. As $z\to 0$, we have
\[
    F\left(e^{\frac{2\pi i h}{k}-\frac{2\pi z}{k}}\right) \sim \omega_{h,k}\sqrt{z}\exp\left(\frac{\pi\left(z^{-1}-z\right)}{12k}\right),
\]
which provides excellent information about the growth of $F(q)$ near the root of unity $e^\frac{2\pi i h}{k}$. This was the reason why we divided the path of integration into Farey arcs.

Next time, we will look into an asymptotic formula for $p_K(\alpha)$, the partition function in a real quadratic field $K$. The idea behind the proof, due to Rademacher, was carried out in all details by his student Meinardus. But since we have no information about the modularity of the corresponding generating function (hence, there is no division into Farey arcs in this case), the resulting asymptotics for $p_K(\alpha)$ is incomparably worse.

## References

[1] T. M. Apostol, *Modular functions and Dirichlet series in number theory*, Second edition. Grad. Texts in Math., 41, Springer-Verlag, New York, 1990. x+204 pp.

[2] H. Rademacher, *On the partition function $p(n)$*, Proc. London Math. Soc. (2) **43** (1937), no. 4, 241–254.
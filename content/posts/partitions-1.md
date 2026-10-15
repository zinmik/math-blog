+++
date = '2026-10-15'
layout = 'blog'
katex = true
showDate = true
title = 'Partitions in number fields 1: The basics'
summary = 'The first post in a planned series on this topic.'
categories = ['featured']
tags = ['math-heavy','partitions']
+++

We review selected aspects of the elementary theory of integer partitions, introduce partitions in number fields, and point out some differences between the two. This is the first installment in a planned series on this topic.

A partition is simply a way of writing a positive integer as a sum of positive integers, while two partitions that differ only by the order of their parts are considered to be the same. For example, the partitions of $4$ are
\[
    4,\quad 3+1,\quad 2+2,\quad 2+1+1,\quad 1+1+1+1.
\]
One of the things that I worked on during my PhD was how to make sense of the properties of partitions in the setting of number fields. For our purposes, the prototypical number field will be the real quadratic field $K=\mathbb{Q}(\sqrt{2})$. The role of the integers $\mathbb{Z}$ is played by the ring of integral elements $\mathbb{Z}[\sqrt{2}]$ in $K$. Unsurprisingly, the correct analog of positive integers $\mathbb{N}$ turns out to be the set of totally positive integral elements $\mathcal{O}_K^+$. We say that $a+b\sqrt{2}$ is totally positive if both $a+b\sqrt{2}>0$ and $a-b\sqrt{2}>0$ (when it comes to number fields, one usually has to look at all the embeddings at once). The element $2+\sqrt{2}$ is totally positive but $1+\sqrt{2}$ is not. In $\mathbb{Q}(\sqrt{2})$, $4$ has $6$ partitions in total: the $5$ from before and also
\[
    (2+\sqrt{2})+(2-\sqrt{2}).
\]

The theory of integer partitions is well known for how beautiful it is. It can boast the story of the discovery of the exact formula for the number of partitions of $n$ by Hardy and Ramanujan. There are elegant partition identities and surprising congruences. Some of the deepest results are intimately tied with the theory of modular forms. So what do we know about partitions in number fields? Compared to the extensive knowledge about integer partitions, very little. It is true that when we take a theorem which works over $\mathbb{Z}$ and directly translate it into $\mathbb{Z}[\sqrt{2}]$, it usually breaks down. But it is also true that no one systematically studied this topic until fairly recently. Perhaps we can find less obvious analogues of some of the properties mentioned above.

Since the parts of an integer partition can be ordered by size, we can *define* it as a non-increasing finite sequence of positive integers. For example, $(4,3,1,1)$ is a partition of $9$. This can be visualized using what's called a *Ferrers diagram*:
<figure>
    <img    src="/math-blog/images/ferrers-diagram.svg"
            alt="Ferrers diagram">
    <figcaption>
        Figure 1. Ferrers diagram of a partition.
    </figcaption>
</figure>

A Ferrers diagram is also called a *Ferrers graph*. A similar representation where dots are replaced with squares is called a *Ferrers board*. The word “Ferrers” is not spelled with an apostrophe (I have definitely made that mistake before).

By manipulating these diagrams, one can already prove some partition identities, such as: “The number of partitions of a positive integer $n$ with exactly $r$ parts is equal to the number of partitions of $n$ where the largest part is $r$”. This can be seen by applying an operation called *conjugation* which reflects the entire diagram along the main diagonal:
<figure>
    <img    src="/math-blog/images/conjugation.svg"
            alt="Conjugation of Ferrers diagrams">
    <figcaption>
        Figure 2. Conjugation of Ferrers diagrams.
    </figcaption>
</figure>

Let $p(n)$ be the number of partitions of a positive integer $n$. Additionally, we define $p(0)=1$. The function $p$ is called the *partition function*. The generating function for partitions is given by
\[
    F(q) = \sum_{n=0}^{\infty}p(n)q^n = \prod_{j=1}^{\infty}\frac{1}{1-q^j}.
\]
The equality of the infinite series and product is explained by the fact that $\frac{1}{1-q^j}$ is the sum of the geometric series $1+q^j+q^{2j}+\dots$, and $p(n)$ is the coefficient of $q^n$ in the product
\[
    (1+q^1+q^{2\cdot 1}+\dots)(1+q^2+q^{2\cdot 2}+\dots)(1+q^3+q^{2\cdot 3}+\dots)\dots
\]
The first thing we might want to know about the partition function is how to efficiently evaluate it. The answer is provided by Euler's pentagonal number theorem:
\[
    \prod_{j=1}^{\infty}(1-q^j) = 1+\sum_{n=1}^{\infty}(-1)^n(q^{\omega(n)}+q^{\omega(-n)}) = \sum_{n=-\infty}^{\infty}(-1)^n q^{\omega(n)},
\]
where $\omega(n)=\frac{3n^2-n}{2}$ is the generalized pentagonal number. Multiplying this by the generating function for partitions, we obtain
\[
    \left(\sum_{n=0}^{\infty}p(n)q^n\right)\left(\sum_{n=-\infty}^{\infty}(-1)^n q^{\omega(n)}\right) = 1.
\]
Let us define $p(n)=0$ if $n<0$. Then, comparing the coefficient of $q^n$ on both sides proves that for $n\geq 1$, we have
\[
    p(n) = -\sum_{k=1}^{\infty}(-1)^{k}\left(p(n-\omega(k))+p(n-\omega(-k))\right),
\]
where in the sum on the right-hand side, only finitely many terms are non-zero. In other words,
\[
    p(n) = p(n-1)+p(n-2)-p(n-5)-p(n-7)+\dots
\]
This recurrence formula was famously used by MacMahon to compute $p(n)$ up to $n=200$ by hand. Euler's pentagonal number theorem can be proved by analytic methods, although, there is also Franklin's combinatorial proof which uses certain operations on Ferrers diagrams (see Apostol, Introduction to Analytic Number Theory, Section 14.5).

I would like to mention that there is another, often overlooked, recurrence for the partition function involving the sum of divisors function $\sigma$:
\[
    np(n) = \sum_{k=1}^n \sigma(k)p(n-k).
\]
The proof is by taking the logarithmic derivative of $F(q)$. On the one hand, we have
\[
    qF'(q) = \sum_{n=1}^{\infty}np(n)q^n.
\]
On the other,
\[
    q\frac{F'(q)}{F(q)} = q\sum_{d=1}^{\infty}(-\log(1-q^d))' = q\sum_{d=1}^{\infty}\left(\sum_{j=1}^{\infty}\frac{q^{dj}}{j}\right)' = \sum_{d=1}^{\infty}\sum_{j=1}^{\infty}dq^{dj},
\]
hence
\[
    \sum_{n=1}^{\infty}np(n)q^n = \left(\sum_{n=0}^{\infty}p(n)q^n\right)\left(\sum_{k=1}^{\infty}\sigma(k)q^k\right).
\]
Comparing the coefficients on both sides concludes the proof.


We will also use $p(n|\text{condition})$ to denote the number of partitions of $n$ satisfying the specified condition. The famous Euler's identity states that the number of partitions of $n$ into odd parts equals the number of partitions of $n$ into even parts. In our notation, this is expressed as
\[
    p(n|\text{odd parts}) = p(n|\text{distinct parts}).
\]
There are two different approaches one can opt for to prove this. The first one is a *bijective proof*: construct a bijection between the partitions of the first kind and of the second kind. In the case of Euler's identity, this can be done by *merging and splitting*. Starting with a partition into odd parts, merge two parts of the same size together. Repeat until you are left with a partition into distinct parts. Conversely, starting with a partition into distinct parts, split every even part in half. Repeat until you are left with a partition into odd parts. It can be seen that the two processes are inverse to each other define the required bijection.

The second possible proof is by generating functions. The generating function for partitions into distinct parts can be turned by algebraic manipulation into the generating function for partitions into odd parts:
\[
    \prod_{j=1}^{\infty}(1+q^j) = \prod_{j=1}^{\infty}\frac{1-q^{2j}}{1-q^j} = \prod_{j=1}^{\infty}\frac{1}{1-q^{2j-1}},
\]
where in the second step we use that every $1-q^j$ with $j$ even in the denominator cancels with a term in the numerator. As we are doing only formal algebraic manipulations, one does not have to worry about establishing convergence for these products (although you are welcome to verify that they converge for $|q|<1$).

After this tour of the elementary theory of integer partitions, we turn back to partitions in number fields to see what can be salvaged. First of all, ordering the set $\mathcal{O}_K^+$ simply by size is not a good idea. It would define a total ordering, but since $0$ is an accumulation point of $\mathcal{O}_K^+$ on the real line, it would not be a well-ordered set. Let $\alpha'$ denote the (Galois) conjugate of $\alpha$. We let $\alpha\prec\beta$ if both $\alpha<\beta$ and $\alpha'<\beta'$. Next we define $\alpha\preceq\beta$ if and only if $\alpha\prec\beta$ or $\alpha=\beta$. The relation $\preceq$ turns $\mathcal{O}_K^+$ into a partially (but not totally) ordered set. This set contains no infinite decreasing chains, which is the reason why every element $\alpha$ has only finitely many partitions. Since the ordering is only partial, it makes sense to think of partitions as unordered tuples, or multisets. A suitable notation would be $[\alpha_1,\alpha_2,\dots,\alpha_j]$ with square brackets, except that this could get easily confused with a continued fraction, and continued fractions play quite an important role in the theory. Let $p_K(\alpha)$ be the number of partitions of $\alpha\in\mathcal{O}_K^+$, and also set $p_K(0)=1$. We can immediately observe some properties of the partition function $p_K$. The partitions of $\alpha$ are in bijection with the partitions of $\alpha'$ because if we are given a partition of $\alpha$, then we obtain a partition of $\alpha'$ by conjugating every part:
\[
    \alpha=\alpha_1+\dots+\alpha_j \Longleftrightarrow \alpha'=\alpha_1'+\dots+\alpha_j'.
\]
An invertible element of $\mathcal{O}_K$ is called a unit. If $\varepsilon$ is a totally positive unit, then multiplying every part $\alpha_i$ by $\varepsilon$ yields a partition
\[
    \varepsilon\alpha=\varepsilon\alpha_1+\dots+\varepsilon\alpha_j
\]
of $\varepsilon\alpha$. Conversely, multiplying every part in a partition of $\varepsilon\alpha$ by $\varepsilon^{-1}=\varepsilon'$ yields a partition of $\alpha$. The two properties that we just proved are
\[
    p_K(\alpha')=p_K(\alpha),\qquad p_K(\varepsilon\alpha)=p_K(\alpha).
\]
An element $\alpha\in\mathcal{O}_K^+$ is called *indecomposable* if it cannot be expressed as a sum $\alpha=\beta+\gamma$, where $\beta,\gamma \in \mathcal{O}_K^+$. Thus, indecomposable elements are precisely those elements for which $p_K(\alpha)=1$. Every totally positive unit $\varepsilon$ is indecomposable, which may be seen as follows. The norm and trace of an element $\alpha\in K$ are defined by $\operatorname{Nm}(\alpha)=\alpha\alpha'$ and $\operatorname{Tr}(\alpha)=\alpha+\alpha'$. For contradiction, assume that
\[
    \varepsilon = \beta+\gamma,
\]
where $\beta,\gamma \in \mathcal{O}_K^+$. Since $\operatorname{Nm}(\varepsilon) = \varepsilon\varepsilon' = 1$, taking the norm on both sides and expanding the product, we get
\[
    1 = (\beta+\gamma)(\beta'+\gamma') = \operatorname{Nm}(\beta)+\operatorname{Tr}(\beta\gamma')+\operatorname{Nm}(\gamma).
\]
But $\beta$ and $\gamma$ are totally positive, therefore $\operatorname{Nm}(\beta)\geq 1$, $\operatorname{Nm}(\gamma)\geq 1$, and $\operatorname{Tr}(\beta\gamma')\geq 2$. The right-hand side is $\geq 4$, a contradiction. The same proof shows that every element of norm $2$ or $3$ is also indecomposable. On the other hand, we may prove the following.

**Lemma.** There exists a constant $c_K>0$ depending only on $K$ such that every totally positive element $\alpha$ of norm $\operatorname{Nm}(\alpha)\geq c_K$ is decomposable. In particular, there exist only finitely many indecomposable elements up to multiplication by totally positive units.

**Proof.** Let $\varepsilon>1$ be the smallest totally positive unit. For a given $\alpha\in\mathcal{O}_K^+$, there exists $k\in\mathbb{Z}$ such that
\[
    \varepsilon^{2k-1} < \frac{\alpha'}{\alpha} \leq \varepsilon^{2k+1}.
\]
Consider the element $\beta=\varepsilon^k\alpha$. We have
\[
    \frac{\beta'}{\beta} = \frac{\varepsilon'^k\alpha'}{\varepsilon^k\alpha} = \varepsilon^{-2k}\alpha,
\]
hence
\[
    \varepsilon^{-1} < \frac{\beta'}{\beta} \leq \varepsilon.
\]
If $\operatorname{Nm}(\beta)=\beta\beta'\geq c_K$, then
\[
    \beta^2 = \beta\beta'\cdot\frac{\beta}{\beta'} \geq c_K\varepsilon^{-1}
\]
and similarly, $\beta'^2 \geq c_K\varepsilon^{-1}$. Therefore, if $c_K>\varepsilon$, then both $\beta>1$ and $\beta'>1$, and we have the decomposition $\beta=(\beta-1)+1$. Because $\alpha$ differs from $\beta$ be a multiple of a totally positive unit, it is also decomposable.<div style="text-align: right;">$\square$</div>

To illustrate the lemma, we determine all indecomposables in $\mathbb{Q}(\sqrt{2})$ up to multiplication by totally positive units. The fundamental unit of $K$ is $1+\sqrt{2}$, which is not totally positive. The smallest totally positive unit is therefore $(1+\sqrt{2})^2=3+2\sqrt{2}$. Every element of norm greater than $3+2\sqrt{2}=5.82\ldots$ is decomposable. It remains to solve the Pell equation $x^2-2y^2=n$ for $n\in\{1,2,3,4,5\}$ to determine the elements of norm $n$. Up to multiplication by totally positive units, we get the following:
* no solutions for $n\in\{3,5\}$,
* $\alpha=1$ for $n=1$,
* $\alpha=2+\sqrt{2}$ for $n=2$,
* $\alpha=2$ for $n=4$. This element is decomposable.

**Example.** The only indecomposable elements in $\mathbb{Q}(\sqrt{2})$ up to multiplication by totally positive units are $1$ and $2+\sqrt{2}$.

If we started looking at other quadratic fields with larger fundamental units, this method would quickly become unfeasible. Luckily, the indecomposables can be completely described in terms of a certain continued fraction. We will not give the details here as it would take us too far from our main theme. Instead, let us remark that indecomposables were first studied in connection with the theory of universal quadratic forms over number fields, where they found many applications (even recently).

If there is a useful way how to graphically represent partitions of totally positive integers similar to Ferrers diagrams, it has not been invented yet. These diagrams exist for partitions over $\mathbb{Z}$ thanks to the fact that the only indecomposable element is $1$, and therefore every positive integer uniquely decomposes as a sum of $1$s. Over number fields, every totally positive element can also be written as a sum of indecomposables, but the decomposition is not necessarily unique — consider
\[
    1+1+1+1 = (2+\sqrt{2})+(2-\sqrt{2}).
\]
That also means there is no direct way of generalizing the partition identities that are proved by manipulating Ferrers diagrams. One identity that does generalize to this setting is Euler's identity: it is enough to simply define $\alpha$ to be odd if it cannot be written as $\alpha=2\beta$ for $\beta\in\mathcal{O}_K$. Then we have
\[
    p_K(\alpha|\text{odd parts}) = p_K(\alpha|\text{distinct parts}),
\]
and the bijective proof goes through exactly as before. The proof by generating functions is trickier. What even is the generating function for partitions over $K$? If we want our generating function to be well defined as an analytic object, we must once again consider $\alpha$ and $\alpha'$ simultaneously. The “correct” choice is the two-variable generating function
\[
    F_K(q_1,q_2) = \sum_{\alpha\succeq 0}p_K(\alpha)q_1^{\alpha}q_2^{\alpha'} = \prod_{\beta\succ 0}\frac{1}{1-q_1^{\beta}q_2^{\beta'}}.
\]
Here $\alpha\succeq 0$ indicates that the summation is over all elements in $\mathcal{O}_K^+\cup\{0\}$. The series converges if $|q_1|<1$ and $|q_2|<1$. We will have an opportunity to examine this function more closely when we discuss the asymptotic formula for $p_K(\alpha)$.

The naive attempt to take
\[
    F_K(q) = \sum_{\alpha\succeq 0}p_K(\alpha)q^\alpha = \prod_{\beta\succ 0}\frac{1}{1-q^\beta}
\]
fails due to the fact that $0$ is an accumulation point of the set $\mathcal{O}_K^+$ on the real line. But an important point to make here is that although it does not converge, it can be treated as a formal series. Technically, it is an element of a certain ring of generalized series with coefficients in $\Z$. In the product, $\frac{1}{1-q^\beta}$ means the inverse of $1-q^\beta$ in this ring, which is of course $1+q^\beta+q^{2\beta}+\dots$. When the product is expanded, only finitely many terms contribute to the coefficient of $q^\alpha$ for a given $\alpha$. The upshot is that an integer partition identity that can be proved purely by formal operations with infinite series should have an analog over $K$. Unfortunately, Euler's pentagonal number theorem does not fall into this category. But the other recurrence formula for $p(n)$ does. For $n\in\Z$, the notation $n\mid\alpha$ means that there exists $\beta\in\mathcal{O}_K$ such that $\alpha=n\beta$. Then we define the generalized sum of divisiors function by
\[
    \sigma_K(\alpha) = \sum_{n\in\N:n\mid\alpha}\frac{\alpha}{n}.
\]
With this definition, we have
\[
    \alpha p_K(\alpha) = \sum_{0\prec\beta\preceq\alpha}\sigma_K(\beta)p_K(\alpha-\beta)
\]
for $\alpha\in\mathcal{O}_K^+$, where the sum runs over all $\beta\in\mathcal{O}_K^+$ such that $\beta\preceq\alpha$. The proof is the same as before, namely taking the formal logarithmic derivative of $F_K(q)$. The most efficient method available of computing $p_K(\alpha)$ is to use this recurrence.

The plan for next time is to review the exact formula for $p(n)$ proved by Hardy and Ramanujan. We will see that it hinges on the fact that the generating function $F(q)$ is closely related to the Dedekind eta function $\eta$, which is in turn a modular form of weight $\frac{1}{2}$. In the subsequent posts, we will discuss the asymptotic formula for $p_K(\alpha)$. Is there a chance of the generating function $F_K(q_1,q_2)$ being modular?

## References
For a very accessible treatment of elementary theory of integer partitions, see [1]. Euler's pentagonal number theorem together with an analytic proof and Franklin's combinatorial proof may be found in [2]. The characterization of indecomposables in terms of a continued fraction was proven in [3]. Various properties of partitions over number fields were first systematically treated in [4]. An approach to the theory via indecomposables and continued fractions is contained in [5].

1. G. E. Andrews and K. Eriksson, *Integer partitions*, Cambridge University Press, Cambridge, 2004. x+141 pp.
2. T. M. Apostol, *Introduction to analytic number theory*, Undergrad. Texts Math., Springer-Verlag, New York-Heidelberg, 1976. xii+338 pp.
3. A. Dress and R. Scharlau, *Indecomposable totally positive numbers in quadratic orders*, J. Number Theory **14** (1982), 292–306.
4. D. Stern and M. Zindulka, *Partitions in real quadratic fields*, Math. Nachr. **298** (2025), no. 2, 548–566.
5. M. Zindulka, *Totally positive elements with $m$ partitions exist in almost all real quadratic fields*, Proc. Edinburgh Math. Soc. **69** (2026), no. 2, 701–734.
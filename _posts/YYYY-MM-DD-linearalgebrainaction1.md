---
layout: post
title: "Linear Algebra at Work.\n 1: Revisiting Radicals"
author: "Josué Tonelli-Cueto"
description: "'Linear Algebra at Work' is a series of posts showing nice application of linear algebra inside mathematics. In this post: radical extensions and Kummer theory."
excerpt: "'Linear Algebra at Work' is a series of posts showing nice application of linear algebra inside mathematics. In this post: radical extensions and Kummer theory."
image: "../imgs/logo.png"
date: YYY-MM-DD
categories:
- linear algebra at work
- mathematics
tags:
- algebra
- Galois theory
lang: en
#lang: es
#lang: eu
#lang: de
#lang:fr
published: false
---

<div class="jumbotron abstract" style="font-style: italic;">
If number theory is the queen of mathematics, linear algebra is its working class—ignored by the upper disciplines of mathematics, linear algebra does the heavy work underneath. In this series of posts, I intend to share those examples of linear algebra at work to showcase not only the beauty of linear algebra but its computational, simplifying and unifying power.
</div>
<br/>
The *raison d'être*[^re] of [Galois theory](https://en.wikipedia.org/wiki/Galois_theory)[^1] is the following theorem:

[^re]: reason for existing

[^1]: Usually left out of any course of Galois theory due to lack of time at the end of the semester.

**Theorem.** A univariate polynomial $f\in K[X]$ is solvable by radical if and only if the Galois group of the Galois group its splitting field over $K$ is solvable.

We can interpret this theorem as one of the first uncomputability results, in which a certain computational method—taking adding, substracting, multiplying, dividiving and taking radicals—is not enough to express the roots of a polynomial. At the core of the proof of the above theorem lies the following proposition.

**Proposition.** Let $L/K$ be a Galois extension of degree $p$ prime such that $K$ does not have characteristic $p$ and such that $K$ contains all $p$th roots of unity. Then

$$L=K[\alpha^{\frac{1}{p}}]$$

for some $\alpha\in K.$

To prove the above proposition, one employs very explicitly that $L/K$ does not have subextensions. As a consequence, one feels that one does not really understand why solvability by radicals work. At the core of the proof is the formula for the Lagrange resolvent

$$\sum_{k=0}^{p-1}\omega^{-k}x^k,$$

where $\omega$ is a $p$th root of unity, which is very mysterious in itself. Using linear algebra we can get a gratifying proof of this result not only for cyclic with prime order, but for cyclic extensions of arbitrary order. Moreover, the technique extends to Abelian extensions allowing us to get a more efficient understanding of radical extensions without reducing to cyclic factorization. Even though many of the techniques highlighted here are not new, linear algebra allows us to get a new perspective on these old results of Galois theory in a way that they are more accessible[^ext].

[^ext]: I will leave for a future post dealing with the finite characteristic case in its full generality, the so-called [Artin–Schreier theory](https://en.wikipedia.org/wiki/Artin%E2%80%93Schreier_theory). Even though, what is written here would allow us to prove a full version of [Kummer theory](https://en.wikipedia.org/wiki/Kummer_theory) in this post, I decided against it, because my objective is to show how we can use linear algebra for understanding radical extensions better.

## Galois meets linear algebra

Given a Galois extension $L/K,$ we can consider any Galois automorphism $\sigma:L\rightarrow L.$ Since Galois automorphisms are field-automorphisms of $L$ and fix every element of $K,$ we have that $\sigma$ is, in particular, a $K$-linear endomorphism of the $K$-vector space $L,$ i.e., a $K$-linear map of the $K$-vector space $L$ to itself. Once we make this realization, we can ask the following questions about $\sigma$ as a linear map: what is its characteristic polynomial? And its minimal polynomial? What are the eigenvalues? How does the Jordan normal form of $\sigma$ looks like?

However, considering Galois automorphisms as linear endomorphisms is nothing new. On the way to prove the fundamental theorem of Galois theory, one proves the following lemma whose proof we omit[^artin]. The objective of this lemma is to show that there cannot be more Galois automorphisms than the degree of the extension.

**Artin's Lemma.** Let $L/K$ be a field extension and $\sigma_1,\ldots,\sigma_n\in\mathrm{Gal}(L/K)$ distinct Galois automorphisms of $L/K.$ Then $\sigma_1,\ldots,\sigma_n$ are linearly independent over $L$ (as elements of the $L$-vector space of $K$-linear endomorphisms of $L$).

[^artin]: *Proof of Artin's Lemma.* The argument is by induction on $n.$ For $n=1,$ the statement is obvious. For $n>1,$ assume that $\sum_{k=1}^n a_k\sigma_k=0$ for some $a_1,\ldots,a_n.$ Note that this means that for all $x\in L,$ $\sum_{k=1}^n a_k\sigma_k(x)=0$; and so for all $\alpha,x\in L,$ $\sum_{k=1}^n a_k\sigma_k(\alpha)\sigma_k(x)=0,$ by changing $x$ by $\alpha x.$ Thus for all $\alpha\in L,$ $\sum_{k=1}^n a_k\sigma_k(\alpha)\sigma_k=0.$ Take $\alpha$ such that $\sigma_1(\alpha)\neq \sigma_n(\alpha),$ which exists because $\sigma_1\neq\sigma_n.$ Then, by substracting $\sigma_n(\alpha)\sum_{k=1}^n a_k\sigma_k(x)$ from $\sum_{k=1}^n a_k\sigma_k(\alpha)\sigma_k,$ we obtain that $\sum_{k=1}^{n-1} a_k(\sigma_k(\alpha)-\sigma_n(\alpha))\sigma_k=0.$ Hence, by the induction hypothesis, $a_1=0,$ and so, by the induction hypothesis, $a_2=\cdots=a_n=0,$ since $\sum_{k=2}^n a_k\sigma_k=0.$ Since $\sum_{k=1}^n a_k\sigma_k=0$ implies $a_1=\cdots=a_n=0,$ $\sigma_1,\ldots,\sigma_n$ are linearly independent over $L.$ $\square$

Now, Artin's lemma does not answer our questions about characteristic polynomials and eigenvalues, so let's answer them with the following theorem:

**Theorem A.** Let $L/K$ be a field extension of degree $n$ and $\sigma\in\mathrm{Gal}(L/K)$ a Galois automorphism of order $o.$ Then:
1. The minimal polynomial of $\sigma$ is $X^o-1.$
2. The characteristic polynomial of $\sigma$ is $(X^o-1)^{n/o}.$
3. If the characteristic of $K$ is not a divisor of $o$ and $K$ contains all $n$th roots of unity $1, \omega,\ldots,\omega^{o-1},$ then there is a $K$-basis of $L$ such that the associated matrix of $\sigma$ is a diagonal matrix with entries $1,\ldots, 1\omega,\ldots,\omega^{o-1}$ repeated $n/o$ times.
4. Let $o=\tilde{o}p^s$ where $p$ is prime and $\tilde{o}$ is not divisble by $p.$ If the characteristic of $K$ is $p$ and $K$ contains all $\tilde{o}$th roots of unity $\omega,\ldots,\omega^{\tilde{o}-1},$ then there is a $K$-basis of $L$ such that the associated matrix of $\sigma$ is a block-diagonal matrix with the $\tilde{o}$ Jordan blocks of size $p^s$

$$J_{p_s}(\omega^k):=\begin{pmatrix}\omega^k&1&&\\&\omega^k&\ddots&\\&&\ddots&1\\&&&\omega^k\end{pmatrix}\in K^{p^s\times p^s}\,(k\in\{0,\ldots,\tilde{o}-1\})$$

repeated $n/o$ times.

*Proof.* First, let us show that we can assume without loss of generality that $n=o,$ i.e., that $L/K$ is a Galois extension whose Galois group is generated by $\sigma.$

Let $\tilde{K}$ be the field whose elements are fixed by $\sigma.$ Then $L/\tilde{K}$ is Galois with Galois group generated by $\sigma.$ If $\{x_1,\ldots,x_{o}\}$ is a $\tilde{K}$-basis of $L$ and $\{\lambda_1,\ldots,\lambda_{n/o}\}$ a $K$-basis of $\tilde{K},$ then

$$\{\lambda_1x_1,\ldots,\lambda_{1}x_o,\lambda_2x_1,\ldots,\lambda_{2}x_o,\ldots,\lambda_{n/o}x_1,\ldots,\lambda_{n/o}x_o \}$$

is a $K$-basis of $L.$ Moreover, if $\tilde{A}$ is the matrix associated to $\sigma$ with respect the basis $\{x_i\}$ and $A$ is the matrix associated with respect the basis $\{x_iy_j\},$ then

$$A=\mathbb{I}_{n/o}\otimes\tilde{A}=\begin{pmatrix}\tilde{A}&&\\&\ddots&\\&&\tilde{A}\end{pmatrix}.$$

Therefore if the theorem holds for $L/\tilde{K},$ the it holds for $L/K.$ Hence we can assume without loss of generality that $n=o.$

From now on, we are assuming that $n=o.$ For proving the first and second point, note that $\sigma^o-\mathrm{id}=0.$ Thus the minimal polynomial of $\sigma$ divides $X^o-1.$ Now, $\mathrm{id},\sigma,\ldots,\sigma^{o-1}$ are distinct automorphisms, and so, by Artin's lemma, they are linearly independent over $K.$ Therefore

$$p(\sigma)=\sum_{k=0}^{o-1}a_k\sigma^k$$

cannot vanish for any non-zero polynomial $p=\sum_{k=0}^{o-1}a_kX^k.$ In particular, the minimal polynomial of $\sigma$ should have degree $\geq o.$ Hence $X^o-1$ is the minimal polynomial of $\sigma,$ and so it is its characteristic polynomial in the case $n=o$ that we are considering.

For the third point, observe that the minimal polynomial of $\sigma,$ $X^o-1,$ splits over $K.$ Hence $\sigma$ is diagonalizable with respect a $K$-basis. The claim about the entries of the diagonalization follows from the shape of the characteristic polynomial.

For the fourth point, we have that the minimal polynomial of $\sigma$ is $(X^{\tilde{o}}-1)^{p^s},$ where $X^{\tilde{o}}-1$ splits over $K$ by assumption. Hence there is a $K$-basis that puts $\sigma$ in Jordan normal form. Now, for each root $\omega^k$ of $X^{\tilde{o}}-1,$ there has to be a Jordan block of size $p^s$ since that's the order of $\omega^{k}$ as a root of the minimal polynomial of $\sigma.$ However, this means that there cannot be more Jordan blocks for any $\omega^k,$ since $\tilde{o}$ block of size $p^s$ fills a matrix of order $o=\tilde{o}p^s.$

<p style="text-align:right">$\square$</p>

## Radicals and cyclic extensions

Recall that a *cyclic extension* is a Galois extension whose Galois group is cyclic. The above proposition holds in more generality for cyclic extensions whose degree is not necessarily prime.

**Theorem B.** Let $L/K$ be a cyclic extension of degree $n$ such that the characteristic of $K$ does not divide $n$ and such taht $K$ contains all $n$th roots of unity. Then
$$L=K[\alpha^{1/n}]$$
for some $\alpha\in K.$

*Proof.* Let $\sigma$ be a generator of the Galois group of $L/K$ and $\omega\in K$ a primitive $n$th root of unity. By Theorem A, $\sigma$ has $\omega$ as an eigenvalue. Let $x\in L$ be one a non-zero $\omega$-eigenvector of $\sigma$. Then

1. $x^n\in K,$ since $x^n$ is fixed by $\sigma,$ and
1. $L=K[x],$ since $x$ is only fixed by the trivial automorphism—we have that $\sigma^k(x)=\omega^kx\neq x$ whenever $\sigma^k$ is not the identity, i.e., when $k$ does no divide $n.$

Hence, taking $\alpha=x^n\in K,$ we have that $L=K[\alpha^{1/n}],$ as desired.

<p style="text-align:right">$\square$</p>

Now, in a more traditional approach, we don't use the language of eigenvalues and eigenvectors, we use the so-called *Lagrange resolvents* which are polynomials of the form

$$\mathcal{L}_n:=\frac{1}{n}\sum_{k=0}^{n-1}\omega^{-k}X^k$$

where $\omega$ is a primitive $n$th root. Using linear algebra, we can still recover the usual approach.

**Theorem B'.** In the setting of Theorem B, let $\sigma$ be a generator of the Galois group of $L/K$ and $\omega\in K$ a primitive $n$th root of unity. Then the linear map

$$\mathcal{L}_n(\sigma)\frac{1}{n}\sum_{k=0}^{n-1}\omega^{-k}\sigma^k$$

is a projection onto the subspace of $\omega$-eigenvector of $\sigma$, i.e., for any $x\in L$, the following are equivalent:
1. $x$ lies on the image of $\mathcal{L}(\sigma)$.
1. $x$ is an $\omega$-eigenvector of $\sigma$.
1. $x$ is a fixed point of $\mathcal{L}(\sigma)$.

In particular, if $u\in L$ satisfies that for all $v\in L$, $\sigma v\neq u+\omega v$, then

$$\mathcal{L}(\sigma)u=\frac{1}{n}\sum_{k=0}^{n-1}\omega^{-k}\sigma^ku$$

is a non-zero $\omega$-eigenvector of $\sigma$—and so it is a primitive element of $L/K$ with irreducible polynomial of the form $X^n-\alpha$ for some $\alpha\in K$.

*Proof.* Since the minimal polynomial of $\sigma$ factors as

$$X^n-1=n\omega^{-1}(X-\omega)\mathcal{L}_n,$$

we have that a) $\mathrm{im}(\sigma-\omega\mathrm{id})=\ker \mathcal{L}_n(\sigma)$, b) $\mathrm{im}\,\mathcal{L}_n(\sigma)=\ker(\sigma-\omega\mathrm{id})$, and c) $L$ is a direct sum of the image of $\mathcal{L}_n(\sigma)$ and the image of $\sigma-\omega\mathrm{id}$.

Now, let's show that $\mathcal{L}_n(\sigma)$ is a projection onto the subspace of $\omega$-eigenvector of $\sigma$:
* $1\Rightarrow 2.$ This follows from b) in the first paragraph of the proof.
* $2\Rightarrow 3.$ Using the Euclidean algorithm, we have that

$$1=q_n(X-\omega)+\mathcal{L}_n$$

where $q_n:=\frac{1}{n}\sum_{k=1}^{n-1}(n-k)\omega^{-k}X^{k-1}$. Therefore, if $x$ is an $\omega$-eigenvector of $\sigma$, then

$$x=q_n(\sigma)(\sigma-\omega\mathrm{id})x+\mathcal{L}_n(\sigma)x=\mathcal{L}_n(\sigma)x,$$

and so $x$ is a fixed point of $\mathcal{L}_n(\sigma)$.
* $3\Rightarrow 1.$ This is trivial, as a fixed point of a map necessarily lies on the image.

Finally, by a) in the first paragraph, the condition we impose on $u$ is equivalent to $u$ not lying on the kernel of $\mathcal{L}_n(\sigma)$. Hence for such $u\in L$,

$$\frac{1}{n}\sum_{k=0}^{n-1}\omega^{-k}\sigma^ku$$

is non-zero, and so, by b) above, it is a non-zero $\omega$-eigenvector of $\sigma$, as desired.
<p style="text-align:right">$\square$</p>

It is important to note how the classical theory can be fully recovered through linear algebra. Moreover, we obtain sufficient and necessary conditions for guaranteeing that the Lagrange resolvent gives us the desired primitive element. We finish with Hilbert's Theorem 90 for cyclic extensions, which can be used to prove that $\omega$-eigenvectors of $\sigma$ exist.

**Hilbert's Theorem 90 for cyclic extensions.** Let $L/K$ be a cyclic extension of degree $n$ and $\sigma$ a generator of its Galois group. For $x\in L^*$, $x$ has norm,

$$N(x):=\prod_{k=0}^{n-1}\sigma^k(x),$$

equal to one, if and only if there is $z\in L^*$ such that

$$x=\frac{\sigma z}{z}.$$

*Proof.* Given $x\in L^*$, there is $z\in L^*$ such that $x=\sigma (z)/z$ if and only if the $K$-linear map $x^{-1}\sigma:L\mapsto L$ has $1$ as an eigenvalue.

Now, by direct computation,

$$\left(x^{-1}\sigma\right)^n=\prod_{k=0}^{n-1}\sigma^k(x^{-1})\sigma^n=\frac{1}{N(x)}\mathrm{id},$$

due to the definition of norm and the fact that $\sigma$ has order $n$. Hence, the minimal polynomial of $x^{-1}\sigma$ divides $X^n-N(x)^{-1}$. Moreover, by Artin's lemma,

$$\sum_{i=0}^{n-1}a_i\left(x^{-1}\sigma\right)^i= \sum_{k=0}^{n-1}\left(a_k\prod_{k=0}^i\sigma^k(x^{-1})\right)\sigma^i$$

cannot be zero unless all the $a_k$ are so—note that Artin's Lemma imply that the $\sigma^i$ are not only $K$-linear independent, but also $L$-linear independent. Thus, the minimal polynomial of $x^{-1}\sigma$ is precisely

$$X^n-N(x)^{-1}.$$

Now, $1$ is an eigenvalue of $x^{-1}\sigma$ if and only if $1$ is a root of its minimal polynomial $X^n-N(x)^{-1}$ if and only if $N(x)=1$, as we wanted to prove.
<p style="text-align:right">$\square$</p>

Again we note how the knowledge we obtain about the minimal polynomial alone allows us to answer the question effortlessly. Moreover, using the fact that $X^n-1=(X-1)(\sum_{i=0}^{n-1}X^i)$, we obtain immediately the following result when the characteristic of $K$ does not divide $n$. This explains a formula that appears in some proofs of Hilbert's Theorem 90 for cyclic extensions, such as the one in Lang's *Algebra*.

**Constructive Hilbert's Theorem 90 for cyclic extensions.** Let $L/K$ be a cyclic extension of degree $n$, not divisible by the characteristic of $K$, $\sigma$ a generator of its Galois group, and $x\in L^*$ an element of norm one. Then if $u\in L$ satisfies that for all $v\in L$, $\sigma v\neq x(u+v)$, then

$$z=\sum_{i=0}^{n-1}\frac{\sigma^i(u)}{\prod_{k=0}^i\sigma^k(x)}$$

is non-zero and satisfies that $x=\sigma(z)/z$.

*Proof.* By the proof of Hilbert's Theorem 90, we have that

$$X^n-1=(X-1)(\sum_{i=0}^{n-1}X^i)$$

is the minimal polynomial of $x^{-1}\sigma$. Since the characteristic of $K$ does not divide $n$, this is a factorization into coprime polynomials. Hence a) $\mathrm{im}\,\sum_{i=0}^{n-1}(x^{-1}\sigma)^i=\ker (x^{-1}\sigma-\mathrm{id})$, and b) $\mathrm{im}(x^{-1}\sigma-\mathrm{id})=\ker \sum_{i=0}^{n-1}(x^{-1}\sigma)^i$. Now, after a simple computation,

$$\sum_{i=0}^{n-1}(x^{-1}\sigma)^i=\sum_{i=0}^{n-1}\frac{1}{\prod_{k=0}^i\sigma^k(x)}\sigma^i.$$

Hence the desired claim follows since any element in the non-zero image of this map satisfies the desired property, and to obtain such a non-zero element we only have to evaluate this map at an element $u$ not on the image of $(x^{-1}\sigma-\mathrm{id})$, i.e., such that for all $v\in L$, $\sigma(v)\neq x(u+v)$.
<p style="text-align:right">$\square$</p>

## Radicals and Abelian extensions

Let $L/K$ be an Abelian extension of degree $n$, which form does it have? When the extension is cyclic, the answer was given above under certain assumptions regarding the roots of unity and the characteristic of $K$. We extend Theorem B to Abelian extensions—the so-called Kummer extensions[^kummerext]—obtaining that the radical structure of Abelian structures is very simple. Recall that the *exponent* of a group $G$, $\exp(G)$, is the minimum number divided by the order of every element of $G$, i.e.,

$$\exp(G):=\min\{n\in\mathbb{N}\mid \text{ for all }g\in G,\,g^n=1\}.$$

[^kummerext]: A *Kummer extension* of exponent $n$ is an Abelian extension $L/K$ such that 1) every Galois automorphism of $L/K$ has order dividing $n$, 2) the characteristic of $K$ does not divide $n$, and 3) $K$ contains all $n$th roots of unity.

**Theorem C.** Let $L/K$ be an Abelian extension of degree $m$ and $n\in \mathbb{N}$ such that
1. the Galois group of $L/K$ has exponent dividing $n$,
1. the characteristic of $K$ does not divide $n$, and
1. $K$ constains all $n$th roots of unity $1,\omega,\ldots,\omega^{n-1}$.

Then there are $\alpha_1,\ldots,\alpha_\ell\in K$ such that

$$L=K[\alpha_1^{1/n},\ldots,\alpha_\ell^{1/n}].$$

More precisely, let $\mathrm{Gal}(L/K)=\prod_{i=1}^{\ell}\langle \sigma_i\rangle$ with $\sigma_i$ of order $o_i$ such that $o_i$ divides $o_{i-1}$—this is always the case by the classification of finite Abelian groups. Then there are non-zero $x_1,\ldots,x_\ell\in L$ such that
1. for all $i$, $x_i$ is a $\omega^{n/o_i}$-eigenvector of $\sigma_i$;
1. for all $i$, for all $j\neq i$, $x_i$ is a $1$-eigenvector of $\sigma_j$, i.e., $x_j$ is fixed by $s\igma_j$; and
And for any non-zero $x_1,\ldots,x_\ell\in L$ satsifying the above conditions, the following holds:
* $L=K[x_1,\ldots,x_\ell],$ and
* for all $i$, $X^{o_i}-x^{o_i}$ is the irreducible polynomial of $x_i$ over $K$.

*Proof.* If we find non-zero $x_1,\ldots,x_\ell\in L$ satisfying conditions 1 and 2, then the only Galois automorphism fixing every element in $K[x_1,\ldots,x_\ell]$ is the trivial one. This follows from the following observation: If $\sigma_1^{k_1}\cdots \sigma_\ell^{k_\ell}$ is not trivial, then there is some $i$ for which $k_i$ is not divisible by $o_i$, and so

$$\sigma_1^{k_1}\cdots \sigma_\ell^{k_\ell}x_i=\omega^{nk_i/o_i}x_i\neq x_i.$$

Moreover, by the same argument, we can see that $K[x_i]$ is the subfield of $L$ fixed precisely by $\prod_{j\neq i}\langle \sigma_k\rangle$ and so the Galois group of $K[x_i]/K$ is $\langle \sigma_i\rangle$. Hence, by the proof of Theorem B, we have that $X^{o_i}-x^{o_i}$ is the irreducible polynomial of $x_i$ over $K$, since $x_i$ is a $\omega^{n/o_i}$-eigenvector of $\sigma_i$.

Hence we only have to show the existence of non-zero $x_1,\ldots,x_\ell\in L$ satisfying conditions 1 and 2. Now, let $L_i$ be the subfield of $L$ whose elements are fixed by $\prod_{j\neq i}\langle \sigma_k\rangle$, then, since $\mathrm{Gal}(L/K)$ is Abelian, we have that  


<p style="text-align:right">$\square$</p>

We could state a Theorem C' in the same fashion as Theorem B', but the formulas and conditions will be more complicated.

## Back to radical formulas!

Up to now, we have been using formulas

The above result suggest that radical formulas for Abelian extensions are not complicated. In other words, they don't have nested radicals! We can do this explicit as follows.

**Theorem R.** Let $K$ be a field of zero characteristic and $p\in K[X]$. If the Galois group $G$ of the splitting field of $p$ over $K$ is Abelian, then every root of $p$ can be written as

$$\sum_{k=1}^\ell \left(\sum_{i=0}^{n-1}a_{k,i}\omega^i\right)\sqrt[n]{\sum_{j=0}^{n-1}b_{k,j}\omega^j}$$

where $\ell$ is the minimal number of generators of $G$, $n$ is its exponent and $a_{k,i},b_{k,j}\in K$ and $\omega$ is a primitive $n$th root of unity.

*Proof.*


<p style="text-align:right">$\square$</p>

The above means that the number of nestings in the radical formulas can related to the length of the series

***

---
layout: post
title: "Linear Algebra at Work.\n 1: Radicals and Kummer's Theory"
author: "Josué Tonelli-Cueto"
description: "'Linear Algebra at Work' is a series of posts showing nice application of linear algebra inside mathematics. In this post: radical extensions and Kummer theory."
excerpt: "'Linear Algebra at Work' is a series of posts showing nice application of linear algebra inside mathematics. In this post: radical extensions and Kummer theory."
image: "../imgs/logo.png"
date: 2022-02-22 22:20:22
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
The *raison d'être* of [Galois theory](https://en.wikipedia.org/wiki/Galois_theory)[^1] is the following theorem:

*[raison d'être]: reason for existing

**Theorem.** A univariate polynomial $f\in K[X]$ is solvable by radical if and only if the Galois group of the Galois group its splitting field over $K$ is solvable.

We can interpret this theorem as one of the first uncomputability results, in which a certain computational method—taking adding, substracting, multiplying, dividiving and taking radicals—is not enough to express the roots of a polynomial. At the core of the proof of the above theorem lies the following proposition.

**Proposition.** Let $L/K$ be a Galois extension of degree $p$ prime such that $K$ does not have characteristic $p$ and such that $K$ contains all $p$th roots of unity. Then

$$L=K[\alpha^{\frac{1}{p}}]$$

for some $\alpha\in K$.

To prove the above proposition, one employs very explicitly that $L/K$ does not have subextensions. As a consequence, one feels that one does not really understand why solvability by radicals work. At the core of the proof is the formula for the Lagrange resolvent

$$\sum_{k=0}^{p-1}\omega^{-k}x^k,$$

where $\omega$ is a $p$th root of unity, which is very misterious in itself. Using linear algebra we can get a gratifying proof of this result and more: even a full proof of [Kummer theory](https://en.wikipedia.org/wiki/Kummer_theory) with computational content[^ext].

[^ext]: I leave for a future post dealing with the [Artin–Schreier theory](https://en.wikipedia.org/wiki/Artin%E2%80%93Schreier_theory).

## Galois meets linear algebra

Given a Galois extension $L/K$, we can consider any Galois automorphism $\sigma:L\rightarrow L$. Since Galois automorphisms are field-automorphisms of $L$ and fix every element of $K$, we have that $\sigma$ is, in particular, a $K$-linear endomorphism of the $K$-vector space $L$, i.e., a $K$-linear map of the $K$-vector space $L$ to itself. Once we make this realization, we can ask the following questions about $\sigma$ as a linear map: what is its characteristic polynomial? And its minimal polynomial? What are the eigenvalues? How does the Jordan normal form of $\sigma$ looks like?

However, considering Galois automorphisms as linear endomorphisms is nothing new. On the way to prove the fundamental theorem of Galois theory, one proves the following lemma whose proof we omit[^artin]. The objective of this lemma is to show that there cannot be more Galois automorphisms than the degree of the extension.

**Artin's Lemma.** Let $L/K$ be a field extension and $\sigma_1,\ldots,\sigma_n\in\mathrm{Gal}(L/K)$ distinct Galois automorphisms of $L/K$. Then $\sigma_1,\ldots,\sigma_n$ are linearly independent over $L$ (as elements of the $L$-vector space of $K$-linear endomorphisms of $L$).

[^artin]: The argument is by induction on $n$. For $n=1$, the statement is obvious. For $n>1$, assume that $\sum_{k=1}^n a_k\sigma_k=0$ for some $a_1,\ldots,a_n$. Note that this means that for all $x\in L$, $\sum_{k=1}^n a_k\sigma_k(x)=0$; and so for all $\alpha,x\in L$, $\sum_{k=1}^n a_k\sigma_k(\alpha)\sigma_k(x)=0$, by changing $x$ by $\alpha x$. Thus for all $\alpha\in L$, $\sum_{k=1}^n a_k\sigma_k(\alpha)\sigma_k=0$. Take $\alpha$ such that $\sigma_1(\alpha)\neq \sigma_n(\alpha)$, which exists because $\sigma_1\neq\sigma_n$. Then, by substracting $\sigma_n(\alpha)\sum_{k=1}^n a_k\sigma_k(x)$ from $\sum_{k=1}^n a_k\sigma_k(\alpha)\sigma_k$, we obtain that $\sum_{k=1}^{n-1} a_k(\sigma_k(\alpha)-\sigma_n(\alpha))\sigma_k=0$. Hence, by the induction hypothesis, $a_1=0$, and so, by the induction hypothesis, $a_2=\cdots=a_n=0$, since $\sum_{k=2}^n a_k\sigma_k=0$. Since $\sum_{k=1}^n a_k\sigma_k=0$ implies $a_1=\cdots=a_n=0$, $\sigma_1,\ldots,\sigma_n$ are linearly independent over $L$.

Now, Artin's lemma does not answer our questions about characteristic polynomials and eigenvalues, so let's answer them with the following theorem:

**Theorem A.** Let $L/K$ be a field extension of degree $n$ and $\sigma\in\mathrm{Gal}(L/K)$ a Galois automorphism of order $o$. Then:
1. The minimal polynomial of $\sigma$ is $X^o-1$.
2. The characteristic polynomial of $\sigma$ is $(X^o-1)^{n/o}$.
3. If the characteristic of $K$ is not a divisor of $o$ and $K$ contains all $n$th roots of unity $1, \omega,\ldots,\omega^{o-1}$, then there is a $K$-basis of $L$ such that the associated matrix of $\sigma$ is a diagonal matrix with entries $1,\ldots, 1\omega,\ldots,\omega^{o-1}$ repeated $n/o$ times.
4. Let $o=\tilde{o}p^s$ where $p$ is prime and $\tilde{o}$ is not divisble by $p$. If the characteristic of $K$ is $p$ and $K$ contains all $\tilde{o}$th roots of unity $\omega,\ldots,\omega^{\tilde{o}-1}$, then there is a $K$-basis of $L$ such that the associated matrix of $\sigma$ is a block-diagonal matrix with the $\tilde{o}$ Jordan blocks of size $p^s$

$$J_{p_s}(\omega^k):=\begin{pmatrix}\omega^k&1&&\\&\omega^k&\ddots&\\&&\ddots&1\\&&&\omega^k\end{pmatrix}\in K^{p^s\times p^s}\,(k\in\{0,\ldots,\tilde{o}-1\})$$

repeated $n/o$ times.

*Proof.* First, let us show that we can assume without loss of generality that $n=o$, i.e., that $L/K$ is a Galois extension whose Galois group is generated by $\sigma$.

Let $\tilde{K}$ be the field whose elements are fixed by $\sigma$. Then $L/\tilde{K}$ is Galois with Galois group generated by $\sigma$. If $\{x_1,\ldots,x_{o}\}$ is a $\tilde{K}$-basis of $L$ and $\{\lambda_1,\ldots,\lambda_{n/o}\}$ a $K$-basis of $\tilde{K}$, then

$$\{\lambda_1x_1,\ldots,\lambda_{1}x_o,\lambda_2x_1,\ldots,\lambda_{2}x_o,\ldots,\lambda_{n/o}x_1,\ldots,\lambda_{n/o}x_o \}$$

is a $K$-basis of $L$. Moreover, if $\tilde{A}$ is the matrix associated to $\sigma$ with respect the basis $\{x_i\}$ and $A$ is the matrix associated with respect the basis $\{x_iy_j\}$, then

$$A=\mathbb{I}_{n/o}\otimes\tilde{A}=\begin{pmatrix}\tilde{A}&&\\&\ddots&\\&&\tilde{A}\end{pmatrix}.$$

Therefore if the theorem holds for $L/\tilde{K}$, the it holds for $L/K$. Hence we can assume without loss of generality that $n=o$.

From now on, we are assuming that $n=o$. For proving the first and second point, note that $\sigma^o-\mathrm{id}=0$. Thus the minimal polynomial of $\sigma$ divides $X^o-1$. Now, $\mathrm{id},\sigma,\ldots,\sigma^{o-1}$ are distinct automorphisms, and so, by Artin's lemma, they are linearly independent over $K$. Therefore

$$p(\sigma)=\sum_{k=0}^{o-1}a_k\sigma^k$$

cannot vanish for any non-zero polynomial $p=\sum_{k=0}^{o-1}a_kX^k$. In particular, the minimal polynomial of $\sigma$ should have degree $\geq o$. Hence $X^o-1$ is the minimal polynomial of $\sigma$, and so it is its characteristic polynomial in the case $n=o$ that we are considering.

For the third point, observe that the minimal polynomial of $\sigma$, $X^o-1$, splits over $K$. Hence $\sigma$ is diagonalizable with respect a $K$-basis. The claim about the entries of the diagonalization follows from the shape of the characteristic polynomial.

For the fourth point, we have that the minimal polynomial of $\sigma$ is $(X^{\tilde{o}}-1)^{p^s}$, where $X^{\tilde{o}}-1$ splits over $K$ by assumption. Hence there is a $K$-basis that puts $\sigma$ in Jordan normal form. Now, for each root $\omega^k$ of $X^{\tilde{o}}-1$, there has to be a Jordan block of size $p^s$ since that's the order of $\omega^{k}$ as a root of the minimal polynomial of $\sigma$. However, this means that there cannot be more Jordan blocks for any $\omega^k$, since $\tilde{o}$ block of size $p^s$ fills a matrix of order $o=\tilde{o}p^s$.

<p style="text-align:right">$\square$</p>

## Radicals and cyclic extensions

Recall that a *cyclic extension* is a Galois extension whose Galois group is cyclic. The above proposition holds in more generality for cyclic extensions whose degree is not necessarily prime.

**Theorem B.** Let $L/K$ be a cyclic extension of degree $n$ such that the characteristic of $K$ does not divide $n$ and such taht $K$ contains all $n$th roots of unity. Then $$L=K[\alpha^{\frac{1}{n}}]$$for some $\alpha\in K$.

*Proof.* Let $\sigma$ be a generator of the Galois group of $L/K$ and $\omega\in K$ a primitive $n$th root of unity. By Theorem A, $\sigma$ has $\omega$ as an eigenvalue. Let $x\in L$ be one of its eigenvectors. Then

1. $x^n\in K$, since $x^n$ is fixed by $\sigma$, and
1. $L=K[x]$, since $x$ is only fixed by the trivial automorphism—we have that $\sigma^k(x)=\omega^kx\neq x$ whenever $\sigma^k$ is not the identity, i.e., when $k$ does no divide $n$.

Hence, taking $\alpha=x^n\in K$, we have that $$L=K[\alpha^{\frac{1}{n}}]$$, as desired.

<p style="text-align:right">$\square$</p>

Moreover, we can obtain some extra information on how to find $\alpha$ if we have the irreducible polynomial of a primitive element of $L/K$. In general, this is the only information that we will have.

**Theorem B'.** In the setting of Theorem $B$, let $\sigma$ be a generator of the Galois group of $L/K$, $\omega\in K$ a primitive $n$th root of unity and $p=X^n-\sum_{k=0}^na_kX^k$ the irreducible polynomial of a primitive element of $L/K$. Then we can take $\alpha\in K$ to be
$$\omega^{-\binom{n}{2}}\det\,L_n(C(p))\in K$$
where
$$L_n:=\frac{1}{n}\sum_{k=0}^{n-1}\omega^{-k}X^k$$
is the Lagrange resolvent and
$$C(p):=\begin{pmatrix}0 &  &  &  & -a_0 \\1 & 0 &  &  & -a_1 \\ & 1 & \ddots &  & -a_2 \\ & & \ddots & 0 & \vdots \\ &  & & 1 & -a_{n-1}\end{pmatrix}$$
is the companion matrix of $p$.




The Lagrange resolvent is the formula
$$L_n:=$$
where $\omega$ is a primitive $n$th root of unity. By a simple computation,
$$X^n-1=n(X-\omega)L_n,$$
and so, since $X-\omega$ and $L_n$ are coprime, we have—after using the Euclidean algorithm—that
$$1=\left(\frac{1}{n}\sum_{k=1}^{n-1}(n-k)\omega^{-k}X^{k-1}\right)(X-\omega)+L_n.$$


## Kummer theory


***

[^1]: Usually left out of any course of Galois theory due to lack of time at the end of the semester.

---
layout: post
title: "Sobre el meme integral de Gaussianos"
author: "Josué Tonelli-Cueto"
description: "..."
excerpt: "..."
image: "../imgs/logo.png"
date: YYYY-MM-DD
categories:
- mathematics
- computation
- divulgación
tags:
- computación
- álgebra
lang: es
published: false
---

El 12 de octubre de 2021, [Gaussianos](https://www.gaussianos.com/) (*aka* Miguel Ángel Morales Medina) sacudió twitter con [este tweet](https://twitter.com/gaussianos/status/1447990247627841536?s=20&t=yApl55rTuQMTP_dZo7bBpg):

<blockquote class="twitter-tweet"><p lang="es" dir="ltr">No me he podido contener 😂 <a href="https://t.co/Z0ewQ8OEr9">pic.twitter.com/Z0ewQ8OEr9</a></p>&mdash; gaussianos (@gaussianos) <a href="https://twitter.com/gaussianos/status/1447990247627841536?ref_src=twsrc%5Etfw">October 12, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Posteriormente, el 15 de octubre de 2021, Gaussianos explicaría su meme en [un post de su blog](https://www.gaussianos.com/la-integral-de-el-juego-del-calamar/). La conclusión aparente de dicho post es que integrar
\\[\frac{1}{X^5}\\]
es mucho más difícil que integrar
\\[\frac{1}{X^5+1}\\]
dado que la segunda integral conlleva muchos cálculos tediosos. Si bien es cierto que el método usado por Gaussianos—que es el que se enseña—es tedioso, este no es el único modo de realizar la integración. Mi objetivo con este post es mostrar que existen formas alternativas de afrontar este cómputo si nos ayudamos de un poco de álgebra computacional y de algunos trucos de análisis complejo[^ngaussianos]. Esto es, podemos usar matemáticas para hacernos la vida más fácil a la hora de calcular.

[^ngaussianos]: Con esto no quiero más que agradecer a [Gaussianos](https://www.gaussianos.com/) y [su post](https://www.gaussianos.com/la-integral-de-el-juego-del-calamar/) por traer a mi mente estas técnicas para la integración simbólica de funciones racionales.

## Descomposición en fracciones simples

A la hora de computar la integral indefinida
\\[\int\,\frac{P(t)}{Q(t)},\\]
el primer paso es dividirla en una suma de fracciones simples, esto es, fracciones de la forma
\\[
\frac{1}{(t-\zeta)^k},
\\]
que son fáciles de integrar—en la siguiente sección veremos como lidiar con esto cuando $\zeta$ es un número complejo. ¿Cómo hacemos eso?

Por supuesto, podemos escribir una ecuación y resolverla, pero hay un mejor método si conocemos las raíces de $Q(t)$. Ahora, esto no es una gran suposición, porque escribir $P(t)/Q(t)$ como suma de fracciones simples requiere que sepamos las raíces[^notaraices].

[^notaraices]: Aparte, en cualquier problema razonable propuesto para integrar $P(t)/Q(t)$ es necesario que seamos capaces de resolver $Q(t)$. Aunque esto pueda ser complicado en general por razones varias como la teoría de Galois que implica que no toda ecuación pueda ser resuelta mediante radicales.

El método se divide en cuatro pasos:
1. Hallar las raíces $Q(t)$. Más concretamente, asumamos que las raíces (reales y complejas) de $Q(t)$ son $\zeta_1,\ldots,\zeta_n$ con multiplicidades respectivas $m_1,\ldots,m_n.$
1. Expresar $1/Q(t)$ como sumar de fracciones simples. Más concretamente, usando la notación de arriba, escribiremos $1/Q(t)$ como
   \\[\frac{1}{Q(t)}=\sum_{i=1}^{n}\frac{q_i}{(t-\zeta_i)^{m_i}}=\frac{q_1}{(t-\zeta_1)^{m_1}}+\cdots+\frac{q_n}{(t-\zeta_n)^{m_n}}\\]
   donde los $q_i$ son constantes, posiblemente complejas.
1. Expresar $P(t)$ como suma the potencias de $(t-\zeta_i)$. Más concretamente, usando la notación de arriba, escribiremos $P(t)$ como
   \\[P(t)=\sum_{k=0}^{m_i-1} a_{i,k}(t-\zeta_i)^k+P_i(t)(t-\zeta_i)^{m_i},\\]
   donde los $a_{i,k}$ son constantes, posiblemente complejas, y $P_i(t)$ un polinomio.
1. Combinar lo anterior para obtener la descomposición deseada. Más concretamente, usando la notación de arriba, obtendremos
   \\[\frac{P(t)}{Q(t)}=r(t)+\sum_{i=1}^n\sum_{k=1}^{m_i}\frac{q_ia_{i,k}}{(t-\zeta_i)^k},\\]
   donde $r(t)=P_1(t)+\cdots+P_n(t)$ es un polinomio. Esta expresión es fácil de integrar aún cuando alguna de las raíces $\zeta_i$ es compleja.

Ahora, entremos en los detalles de los puntos 2 y 3, dado que estos son los que requieren más explicación.

### Inversa de un polinomio

Como hemos dicho queremos escribir
\\[\frac{1}{Q(t)}=\sum_{i=1}^{n}\frac{q_i}{(t-\zeta_i)^{m_i}}=\frac{q_1}{(t-\zeta_1)^{m_1}}+\cdots+\frac{q_n}{(t-\zeta_n)^{m_n}}\\]
donde $\zeta_1,\ldots,\zeta_n$ son todas las raíces—¡reales y complejas!—con multiplicidades respectivas $m_1,\ldots,m_n$ y los $q_i$ son constantes—que pueden ser complejas—. A primera vista, nos podemos preguntar: ¿por qué tal expresión va a existir?

Ahora, si multiplicamos la identidad por $Q(t)=\prod_{i=1}^n(t-\zeta_i)^{m_i},$ tenemos que
\\[1=\sum_{i=1}^{n}q_i(t)\prod_{j\neq i}(t-\zeta_j)^{m_i}\\]

Para ello, solo debemos encontrar las raíces de $Q(t)$.
Lo

La idea es sencilla
Descomponiendo la inversa de un polinomio

###

## Integrando fracciones complejas

### Grado uno

### Grados superiores

## <a name="meme"></a> ¡Al meme de Gaussianos!

## Más allá del meme de gaussianos


***

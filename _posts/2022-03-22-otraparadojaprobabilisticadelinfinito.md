---
layout: post
title: "Otra paradoja probabilística del infinito"
author: "Josué Tonelli-Cueto"
description: "En este post, mostramos como un número aleatorio con un valor esperado infinito tiene una cantidad esperada de cifras finita."
excerpt: "En este post, mostramos como un número aleatorio con un valor esperado infinito tiene una cantidad esperada de cifras finita."
image: "../imgs/logo.png"
date: 2022-03-22 03:22:22
categories:
- mathematics
- divulgación
tags:
- probabilidad
- paradojas
lang: es
published: true
---

<div class="jumbotron abstract" style="font-style: italic;">
Este post forma parte del <a href="https://carnavaldematematicas.wordpress.com/">Carnaval de Matemáticas</a>, que en esta nonagésima octava edición, también denominada 13.1, está organizado por Rafael Martínez González a través de su blog <a href="https://elmundoderafalillo.blogspot.com/">El mundo de Rafalillo</a>.
</div>
<br/>
Escojamos un número entero positivo $\mathfrak{x}\in\mathbb{Z}\_{+}$
 al azar de modo que la probabilidad de elegir el número $n\in\mathbb{Z}\_{+}$ sea
\\[\mathrm{Prob}(\mathfrak{x}=n)=\frac{6}{\pi^2}\frac{1}{n^2}.\\]
Como la suma de todas las probabilidades, $\sum_{n=1}^{\infty}\mathrm{Prob}(\mathfrak{x}=n),$ da uno[^bas], este es un modo válido de escoger un entero positivo al azar.

[^bas]: Esto se debe al [llamado *problema de Basilea* resuelto por Euler](https://es.wikipedia.org/wiki/Problema_de_Basilea).

## ¿Cómo de grande es $\mathfrak{x}$?

Para responder esta pregunta, un método popular es computar la *esperanza* de $\mathfrak{x},$
\\[\mathbb{E}\mathfrak{x}:=\sum_{n=1}^\infty k\mathrm{Prob}(\mathfrak{x}=n).\\]
En el caso en cuestion, se da que
\\[\mathbb{E}\mathfrak{x}=\sum_{n=1}^{\infty}n\frac{6}{\pi^2}\frac{1}{n^2}=\frac{6}{\pi^2}\sum_{n=1}^{\infty}\frac{1}{n}=\infty,\\]
porque la [serie armónica](https://es.wikipedia.org/wiki/Serie_arm%C3%B3nica_(matem%C3%A1tica)), $\sum_{n=1}^{\infty}\frac{1}{n}$, tiene suma infinita.

Ahora, ¿qué quiere decir que el valor esperado–esperanza–de $\mathfrak{x}$ sea infinito? Ciertamente, cualquier valor concreto de $\mathfrak{x}$ que escojamos va a ser finito. Una interpretación habitual de la esperanza es en términos de la *ley de los grandes números*[^lgn]. Para ello, tomemos que no escojemos un número al azar solo una vez, sino que producimos una sucesión de números aleatorios $\mathfrak{x}_1,\mathfrak{x}_2,\mathfrak{x}_3,\ldots$ de modo que cada número aleatorio es independiente del resto y es escogido al azar del mismo modo que $\mathfrak{x}.$[^lm] Entonces, la *la ley de los grandes números* nos dice que la media aritmética de $\mathfrak{x}_1,\ldots,\mathfrak{x}_n,$
\\[\frac{\mathfrak{x}_1+\cdots+\mathfrak{x}_n}{n},\\]
converge a $\mathbb{E}\mathfrak{x}$ con casi toda seguridad, esto es, con probabilidad uno.

[^lm]: En lenguaje matemático, las $\mathfrak{x}_i$ son variables aleatorias independientes e idénticamente distribuidas, con distribuión la misma que la de $\mathfrak{x}$. Esto es, para cada $i,n\in\mathbb{N},$
\\[\mathrm{Prob}(\mathfrak{x}_i=n)=\mathrm{Prob}(\mathfrak{x}=n)=\frac{6}{\pi^2}\frac{1}{n^2}.\\]

[^lgn]: Para les expertes: Como estamos tratando con variables no-negativas, la ley de los grandes números sigue siendo cierto incluso cuando la esperanza es infinito. Por ejemplo, [véase este link para referencias](https://math.stackexchange.com/q/1644218/15330).

Ahora, la esperanza de $\mathfrak{x}$ es infinita. Esto significa que, con probabilidad uno,
\\[\frac{\mathfrak{x}_1+\cdots+\mathfrak{x}_n}{n}\rightarrow\infty\\]
a medida que $n$ va hacia infinito. Esto es, a medida que escogemos más y más números al azar de la misma forma que $\mathfrak{x}$, su valor medio crecerá cada vez más y más con la cantidad de números que escogemos.

## ¿Cuánto me va a costar escribir $\mathfrak{x}$?

A la hora de escribir un número, el aspecto más importante que va a determinar cuánto nos va a costar escribirlo es cuántas cifras tiene ese número. En términos coloquiales, la cantidad de tinta necesaria para escribir un número es aproximadamente proporcional al número de cifras---es solo aproximadamente, porque no toda cifra requiere la misma cantidad de tinta para ser escrita. Ahora, ¿cuántas cifras tiene $\mathfrak{x}?$ La resuesta es
\\[1+\lfloor \log(\mathfrak{x})\rfloor\\]
donde $\log$ es el logaritmo en base 10 y $\lfloor~\rfloor$ denota que redondeamos hacia abajo, esto es, $\lfloor \log(\mathfrak{x})\rfloor$ es $\log(\mathfrak{x})$ omitiendo los decimales tras la coma.

Así, siguiendo la misma lógica probabilística, ¿cuál es el coste esperado para escribir $\mathfrak{x}$? Esto es, ¿cuál es el número de digitos esperado para escribir $\mathfrak{x}$? Computando podemos ver que
\\[\mathbb{E}\,\mathrm{número-de-digitos}(\mathfrak{x})\\]
está dado por
\\[1+\frac{6}{\pi^2}\sum_{n=1}^\infty\frac{\lfloor \log(n)\rfloor}{n^2}\simeq 1.0670073952\ldots<2.\\]
Esto es, ¡el coste esperado de escribir $\mathfrak{x}$ es a lo sumo dos! Usando la ley de los grandes números para interpretar esto, si elegimos una gran cantidad de números al azar de la misma forma que $\mathfrak{x}$, el coste medio de escribir estos números será constante, esto es, el coste de escribir todos los números será aproximadamente proporcional a la cantidad de números aleatorios considerados.

## Llegando a la paradoja...

Por un lado, hemos visto que el valor esperado de $\mathfrak{x}$ es infinito. Por otro lado, la cantidad esperada de dígitos de $\mathfrak{x}$ es a lo sumo dos. Así, hemos llegado a la siguiente 'paradoja'[^petersburgo]:
> A pesar de que el valor esperado de $\mathfrak{x}$ es infinito, el coste esperado para escribir $\mathfrak{x}$ (o el número de cifras esperado de $\mathfrak{x}$) es menos de dos. Esto es, podemos 'esperar' escribir un número aleatorio 'esperadamente' infinito con un número finito de cifras.

Por supuesto, lo paradójico de esto se encuentra en que este hecho ser contraintuitivo. Esta paradoja solo ilustra que podemos escribir número enormes con una pequeña cantidad de cifras. Esto es, esta paradoja ilustra la potencia de nuestro sistema de escritura posicional para escribir números.

[^petersburgo]: Aquelles sabedores de probabilidad, notaran la similitud con otra paradoja probabilística del infinito: [la paradoja de San Petersburgo](https://es.wikipedia.org/wiki/Paradoja_de_San_Petersburgo). Sin embargo, nótese que esta paradoja

***
<!-- Para facilitar la tarea de recopilar las entradas participantes, os recomiendo que, una vez que hayáis publicado vuestra aportación, me lo notifiquéis por al menos uno de los siguientes medios:
-Publicando un comentario en esta misma entrada con un enlace a tu aportación.
-A través de Twitter con un tweet que incluya el enlace a tu entrada y el hashtag #CarnaMat13_1, y que haga mención a mi cuenta (@Rafalillo86) y a la del Carnaval de Matemáticas (@CarnaMat).-->

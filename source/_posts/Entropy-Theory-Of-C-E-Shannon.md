---
title: Entropy Theory Of C.E.Shannon
mathjax: true
date: 2019-10-04 22:50:08
tags: Math and Basic knowledge of ML
categories: Maths
---

# Abstract
***

This article is about C.E.Shannon's famous article *A Mathematical Theory of Communication*. Inspired by what I learnt after the physics and Probability and Mathematical Statistics class, I'm going to reintroduce this great concept, and make the important prove inferred by myself. What's more, I will give my personal comprehension on concept of the entropy both phtsics and the information theory, by combing the knowledge I learnt by myself after that two class.



**Keyword**:   **C.E.Shannon's Entropy**	**Boltzmann's Entropy**  	 **Uncertainty** 	 **Choice**


# Communication System[<sup>1</sup>](#refer-anchor)
***

It consists of essentially five parts:

* An information source which produces a message or sequence of messages to be communicated to the receiving terminal.
* A transmitter which operates on the message in some way to produce a signal suitable for transmission over the channel.
* The channel is merely the medium used to transmit the signal from transmitter to receiver.
* The receiver ordinarily performs the inverse operation of that done by the transmitter, reconstructing the message from the signal. 
* The destination is the person (or thing) for whom the message is intended. 

We may roughly classify communication systems into three main categories: discrete, continuous and mix.

# Choice, Uncertainty And Entropy[<sup>1</sup>](#refer-anchor)
***

In Shannon's article, Shannon has came up with an important question that how to measure how much information is "produced" by such a process.

Suppose we have a set of possible events whose probabilities of occurrence are $p_1, p_2, \dotsc, p_n$. Now we focus mainly on how to measure how much "choice" which can help us concern which event will occur, is involved in the selection of the event or how "uncertain" we are of the outcome. The more choices we have to make, the more uncertainty we can say about this event.

We can define a function $H(p_1, p_2, \dotsc, p_n)$ , it is reasonable to make these contraints for this function.

* H should be continuous in the $p_i$
* If all the $p_i$ are equal, $p_i= \frac{1}{n}$, then $H$ should be a monotonic increasing function of n. With equally likely events there is more choice, or uncertainty, when there are more possible events.
* If a choice be broken down into two successive choices, the orginal $H$ should be the weighted sum of the individual values of $H$. This can be equivalent described as the content I have learnt in the probability theory class: $$H(p_1, \dotsc , p_n)= H(p_1+p_2+\dotsc +p_M, p_{M+1},\dotsc ,p_n)+(p_1+p_2+\dotsc +p_n)\cdot H(q_1, q_2, \dotsc q_M),\quad q_i= \frac{p_i}{p_1+\dotsc +p_M}$$ As you can see, this is strongly connected with the concept of conditional probability.

We can prove that $$
H=-K \sum_{i=1}^{n} p_{i} \log p_{i}
$$ is the only form that can suit these three requirements. Before I show the provement, let me explain why this formula form is intuitively correct.

## Intuitively Explaination
***

* If something has lower probability to happen, but it happens, then it bring more "surprise" for you. In the expression of entropy, we can see that the less the probability is, the more it contributes to the entropy.
* The entropy of the whole system should be the weighted sum of all the system's event, because to measure the uncertainty, in another way, to sure how much information it contains, we should make choice to confirm. But not every choice is indispensable, whether to make a choice depends on its possibility. 

## Prove
***

### The random variables are uniformly distributed
***

With property 3, we can learn this equation:
\begin{equation}
\begin{aligned} g(M N) &=f\left(\frac{1}{M}, \ldots, \frac{1}{M}\right)+\sum_{i}^{M} \frac{1}{M} f\left(\frac{1}{N}, \ldots, \frac{1}{N}\right) \\ &=g(M)+g(N) \end{aligned}
\end{equation}

With property 2 and last conclusion, we get this:

if $s^m\leq t^n\leq s^{m+1}$, then $mg(s)\leq ng(t)\leq (m+1)g(s)$

So what we can finally get:

$\frac{m}{n}\leq \frac{g(t)}{g(s)}\leq \frac{m+1}{n}$.

Now, let's minus $\frac{m}{n}$ on the both side of the second inequality.

\begin{equation}
\left|\frac{m}{n}-\frac{g(t)}{g(s)}\right|<\frac{1}{n}
\end{equation}

And for the same $s, m, t, n$, $\log $function has the same property.
\begin{equation}
\left|\frac{m}{n}-\frac{\log(t)}{\log(s)}\right|<\frac{1}{n}
\end{equation}

Because of $\left| a-b\right| \leq \left| a\right|+\left| b\right|$:

\begin{equation}
\left|\frac{\log(t)}{\log(s)}-\frac{g(t)}{g(s)}\right|<\frac{2}{n}
\end{equation}

Let $n$ is big enough. $$
\frac{g(t)}{g(s)} \rightarrow \frac{\log t}{\log s}
$$
\begin{equation}
g(t)= C\log(t)
\end{equation}

### General Situation
***

Let's first think about rational possibility value, and irrational value can be easily solved with take the limit of the rational number sequence which is a common trick in analysis theory.

Let $P(n)= \frac{m_n}{\sum_{i=1}^{N} m_i}= \frac{m_n}{M}$, $g(M)= f(\frac{1}{M},\dotsc , \frac{1}{M})$

We can get:
\begin{equation}
\begin{aligned} g(M) &=f \left(\underbrace{\frac{1}{M}, \ldots,}_{m_{1} } \dotsc ,\underbrace{\ldots, \frac{1}{M}}_{m_{N} }\right) \\ &=f\left(P_{1}, P_{2}, \ldots P_{N}\right)+\sum_{i=1}^{N} \frac{m_{i}}{M} f\left(\frac{1}{m_{i}}, \ldots, \frac{1}{m_{i}}\right) \\ &=f\left(P_{1}, P_{2}, \ldots P_{N}\right)+\sum_{i=1}^{N} \frac{m_{i}}{M} g\left(m_{i}\right) \end{aligned}
\end{equation}

\begin{equation}
\begin{aligned}
f(P_1, P_2, \dotsc , P_N)&= g(M)-\sum_{i=1}^{N}P_ig(m_i)\\
&= C\log(M)-\sum_{i=1}^{N}P_iC\log(m_i)\\
&= -C\sum_{i=1}^{N}P_i(\log(m_i)-\log(M))\\
&= -C\sum_{i=1}^{N}P_i(\log(\frac{m_i}{M}))\\
&= -C\sum_{i=1}^{N}P_i\log{P_i}
\end{aligned}
\end{equation}

# Personal Comprehension Combined With The Concept Of Entropy In The Physics
***

After taking the class of statistic mechanics, I have learnt the concept of Boltzmann's entropy theory. Shannon's entropy is different from the entropy in physics. This idea is advised by John von Neumann. Because their form are similar and lots of similarity about their property. Inspired by the concept of the entropy concept in the physics, I consider another set of constraints to interpret entropy which is equivalent to the Shannon's definition.

* Physics's entropy represent the degree of chaos in microcosmic meaning. In the Boltzmann's equation $S= \ln(\Omega )$. $\Omega$ represents the number of microstates. And considering the problem in the information system, to confirm an event with property $p$, we discuss the meaning of $\frac{1}{p}$. We can difine this as **space complexity of target search**. The bigger $\frac{1}{p}$, the bigger the space complexity of target search is. The larger the complexity, the more information we need to confirm this event. This is just the same as the $\Omega$. So we analogy the $\Omega$ to comprehend $\frac{1}{p}$. So for the single event, we have $H(p)= C\log(\frac{1}{p})$
* The whole system consist of all these events, every single events contibutes its own entropy should be weighted by its probability $p$. This is a natural thought.

So the finally definition should be $H= -C\sum_{i=1}^{N}P_i\log{P_i}$

<div id="refer-anchor"></div>
# Reference
***
[1] [C.E.Shannon,A Mathematical Theory of Communication, ACM, v.5, January 2001](https://dl.acm.org/citation.cfm?id=584093)
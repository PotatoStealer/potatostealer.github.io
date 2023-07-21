---
layout: post
title:  "Opinions - Some Thoughts on IMO 2023"
author: Hu Man Keat
date:   2023-07-20
categories: opinions
image: false
description: IMO 2023 spoilers!
---
It's that time of the year where I get to pull out my tinfoil hat as a wannabe-contestant and loudly declare which problems I would be able to solve in contest. Fortunately for someone too old (and unqualified) for it, I have all the latitude to give my armchair thoughts and analysis. After a week or so, I give my thoughts and writeups on three problems, in the order I solved them in.

# D1/1 Look ma, no pen (or paper)
> Determine all composite integers $n>1$ that satisfy the following property: if $d_1,d_2,\cdots,d_k$ are all positive divisors of $n$ with $1=d_1<d_2<\cdots<d_k=n$, then $d_i$ divides $d_{i+1}+d_{i+2}$ for every $1\leq i\leq k-2$.

## Thoughts and Writeup
I did this in my head while in a meeting, texting a friend, and working on NanoBlocks, so... no thoughts.

**1. Induction**
We have $d_{k-2}\|n+d_{k-1}$ so $d_{k-2}\|d_{k-1}$. Since divisors come in pairs, i.e. $d_id_{k+1-i}=n$, so $d_2\|d_3$ and $d_2\|d_3+d_4$. This gives $d_2\|d_4$, so $d_{k-3}\|d_{k-1}$, so $d_{k-3}\|d_{k-2}$ as well.

By induction, $1=d_1\|d_2\|\cdots\|d_k=n$ whence $n=p^{k-1}$.

**2. Proof by contradiction**
If you tried to induct downwards as in approach 1, you may run into a roadblock. Again, $d_{k-3}\|d_{k-2}+d_{k-1}$. This motivates defining $p^m\|d_{k-3}$. If $d_{k-3}\|d_{k-2}$, we are done. Otherwise, $p^m$ necessarily appears elsewhere. Let $d_{j}=p^m$ so $d_{k+1-j}=\frac{n}{p^m}$, whence there is another prime $q\|n$.

Suppose $n$ has at least two distinct prime factors and let $p$ be the smallest such prime, $q$ be the second smallest. Let $m$ be the smallest integer such that $q>p^m$, then

$$\frac{n}{q}\|\frac{n}{p^{m-1}}+\frac{n}{p^m}=\frac{n}{p^m}(p+1),$$

so

$$\frac{rn}{q}=\frac{n}{p^m}(p+1) \iff rp^m=pq+q \iff q=rp^m-pq.$$

However, $p$ divides the right-hand side but not the left-hand side, a contradiction.

# D2/4 Leapfrog
> Let $x_1,x_2,\cdots,x_{2023}$ be pairwise different positive real numbers such that
>
> $$a_n=\sqrt{\left(x_1+x_2+\cdots+x_n\right)\left(\frac{1}{x_1}+\frac{1}{x_2}+\cdots+\frac{1}{x_n}\right)}$$
>
> is an integer for every $n=1,2,\cdots,2023$. Prove that $a_{2023}\geq 3034$.

## Thoughts and Writeup
I did this in about 15-ish minutes after the my meeting ended.

**1. Cauchy** If you looked at this and didn't think Cauchy, I don't know what's wrong with you.

Define 

$$c_n=x_1+x_2+\cdots+x_n,\;r_n=\frac{1}{x_1}+\frac{1}{x_2}+\cdots+\frac{1}{x_n},$$

then by Cauchy,

$$a_{n+1}^2=(c_n+x_{n+1})\left(r_n+\frac{1}{x_{n+1}}\right)\geq(a_n+1)^2,$$

so we have $a_{n+1}\geq a_n+1$, with equality when $x_{n+1}^2=\frac{c_n}{r_n}$.

Hmm, this bound is rather loose, and with 3034 being not *too* far away from 2023, and with each successive $a_i$ being at least one apart. An initial instinct I had was to consider when this gap was $2$, but as it turns out, we have $x_n$ controlling the growth of $a_n$, and certainly for large $n$, these $x_n$ were not easy to control, so I gave up trying to fix $x_n$.

I then investigated the odd equality case anyway. Certainly if the sequence needed to grow fast enough, we must eventually run into a contradiction. Suppose equality held throughout, so $a_{n+1}=a_n+1$, so $a_{n+2}=a_{n+1}+1$, i.e. $a_{n+2}=a_n+2$. Then,

$$x_{n+2}^2=\frac{c_{n+1}}{r_{n+1}}=\frac{c_n+x_{n+1}}{r_n+\frac{1}{x_{n+1}}}=\frac{c_n+\sqrt{\frac{c_n}{r_n}}}{r_n+\sqrt{\frac{r_n}{c_n}}}=\frac{c_n}{r_n}=x_{n+1}^2.$$

It turns out that we can't have consecutive gaps be equal to 1. Now I had to decide which relation is useful: whether focusing on successive gaps, or on $a_{n+2}-a_n > 2$. Given that this was an IMO problem, I took a leap of faith and chose the latter, so $a_{n+2}-a_n\geq 3$.

Of course, I do a sanity check first. Starting from $a_1=1$, if the sequence goes $1,4,7,10,...$, then $a_n$=1+3(n-1). Yes, equality cases exist!

Oops, now to prove what was actually asked:

$$a_{2023}\geq a_{2021}+3\geq a_{2019}+6\geq\cdots\geq a_1+1011\cdot3=3034.$$

# D1/3 Rabbits? In my pigeonhole?
> For each integer $k\geq 2$, determine all infinite sequences of positive integers $a_1,a_2\cdots$ for which there exists a polynomial $P$ of the form $P(x)=x^k+c_{k-1}x^{k-1}+\cdots+c_1x+c_0$, where $c_0,c_1,c_{k-1}$ are non-negative integers, such that
>
> $$P(a_n)=a_{n+1}a_{n+2}\cdots a_{n+k}$$
> 
> for every integer $n\geq1$.

## Thoughts and Writeup
I had a hard time deciding whether this fell under A or N, because asking about positive integers really tickled me. Eventually I decided not to look down into the number-theory pigeonhole because I probably didn't know enough theory to describe $P$'s structure. This is a long writeup so I divide it into some observations.

**Observation 1. How do the conditions work?**

Anyhow, thinking immediately about how $P$ worked gave me a headache, so I decided to play around with the conditions. Really, there's not many:

1. $a_1,a_2\cdots$ is a positive infinite sequence
2. the coefficients of $P$ are non-negative (and not strictly positive)
3. $P$ is monic.

In what follows, I focused on $k=2$ so $P(x)=x^2+c_1x+c_0$. 

I first checked the case for when $a_n$ was a sequence of only two terms. For some reason I stared at it for 10 minutes before convincing myself that the words didn't move. Instead, I tried $P(a)=b, P(b)=a$, which says that $a_n$ must be a constant sequence.

What if I gave it three terms instead, so that $P(a)=b, P(b)=c, P(c)=a$? With algebra omitted, 

$$P(x)=x^2-(a+b+c)x+(ab+bc+ca)$$

is a polynomial that works.

Okay, now we have some substance: condition 2 is necessary to force $a_n$ to be positive. But $a_n$ being periodic definitely doesn't work for $k=3$.

For the monic condition, I played with sequences of prime powers (just as in P1) because of the "multiplicative" (for lack of a better word) structure. If ${a_n}={1,2,4,8,16}$, then $P(1)=8, P(2)=32, P(4)=128$, so $P(x)=8x^2$ works cleanly. From this, we know that condition 1 stops ${a_n}$ from growing *too* quickly. Perhaps in true analysis fashion, the solution involves bounding $x^{-k}P(x)-O(x^{-(\text{something})})$.

**Observation 2. ${a_n}$ is non-decreasing**

I still have no clue what to do: it's pretty strange that the problem gives you no clue what ${a_n}$ is, so I tried to grasp at straws. We know that ${a_n}$ cannot be periodic, so it's necessary for ${a_n}$ to be non-decreasing (but not necessarily strictly increasing).

Let $n$ be such that $a_n$ is the least element in ${a_n}$, and that $a_{n+1}<a_n$, so

$$a_{n+k+1}P(a_n)=a_{n+1}\cdots a_{n+k+1}=a_nP(a_{n+1}) < a_nP(a_n)$$

which is a contradiction.

**Observation 3. ${a_n}$ does not have ADHD**

The next natural thing to ask is how does ${a_n}$ grow? I first fix $k$ to be large. Consider this "wild" case when ${a_n}$ is erratic, meaning suppose that the sequence remains constant (and somewhat small) at the start, then explodes, then remains constant again. Clearly for small $n$, $P(x)$ cannot catch up to the right-hand side. For a tractable progress, I try to show that ${a_n}$ cannot exhibit this constant behaviour, that is, ${a_n}$ cannot ever sit "too still".

From observation 2, we have 

$$a_{n+1}^k\leq a_{n+1}\cdots a_{n+k}=P(a_n) \iff a_{n+1}-a_n=P(a_n)^{\frac{1}{k}}-a_n.$$

This is cleanly bounded above by some integer $C$. Certainly, $P(a_n)<a_nP(1)$, so for sufficiently large ${c_k}$, there exists such a $C$. 

Okay but I messed this up somewhere, I meant to show that ${a_n}$ cannot sit still, but ended up proving that $a_n$ cannot grow too fast. Never mind. In any case, we know that $a_n$ has to grow somewhere, but can't go too far!

**Observation 4. What is ${a_n}$?**

It's quite amazing that we've gotten so far given just 3 seemingly weak conditions. If equality holds in observation 3, then ${a_n}$ is an arithmetic progression. But alas, we still don't have equality.

I stared at the problem statement again and I'm finally reminded that $n$ needs to run over all integers. I now look at the *difference set*:

$$D_n=\left\{a_{n+1}-a_n,\;a_{n+2}-a_n,\;\cdots,\;a_{n+k}-a_n\right\}.$$

Since the differences are bounded, there are finitely many such sets (at most $C^k$ of them) as $n$ runs. In particular, there exists one difference set that occurs infinitely many times as $n$ runs, by the Pigeonhole Principle(!!!!!).

Call this difference set (really it's a collection) $D=\{d_1,d_2,\cdots,d_k\}$ and write

$$P(a_n)=(a_n+d_1)(a_n+d_2)\cdots(a_n+d_k),$$

$$P(a_n+d_1)=(a_n+d_2)(a_n+d_3)\cdots(a_n+d_{k+1}).$$

This is a pair of eqquations that hold for infinitely many $n$, and so is a polynomial identity. To wit,

$$P(x)=(x+d_1)(x+d_2)\cdots(x+d_k).$$

The key finishing touch is that the other difference sets actually occur only finitely many times. Otherwise we discover another way to factorise $P(x)$, which is not possible.

Hence, for sufficiently large $n$, we have $D_n=D$. Finally, 
$a_{n+t}=a_n+d_t.$ By induction, $d_t=td_1$, i.e. $a_{n+1}-a_n=d_1$ for sufficiently large $n\geq N$. We now have

$$P(x)=(x+d_1)^k.$$

Now we induct downwards: we have

$$P(a_{N-1})=a_N(a_N+d_1)\cdots(a_N+(k-1)d_1)=P(a_N-d_1).$$ 

$P$ is strictly increasing in $-d<x<\infty$, so $a_{N-1}=a_N-d_1$. The end.

# Final words
I think this year's paper was the most accessible, not just to competitors but also to casual nerds like myself. While D1/1 was probably one of the simplest (with a mean mark of 5.845), D2/4 was relatively instructive, D3/3 was actually a joy to play with under no time stress. I did partially solve D2/4 as well, but my binary tree solution was a mess.

Anyhow, I continue to really enjoy papers that contain accessible openers, as well as problems that keep you thinking about them even long (some days) after you read them. 

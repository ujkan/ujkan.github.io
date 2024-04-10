---
title: 'Integers - of other kinds'
date: 2024-04-10
permalink: /posts/2024/04/complex-integers-1
tags:
  - mathematics
  - exposition
---

## Writer's Note

This is a paradoxical thing to say about a blog post on the Internet, but I didn't write this post with intelligibility in mind. This is not to say that I don't want the reader to understand what is happening here; I wouldn't have published this otherwise. I simply don't know what it means to write with the reader in mind because I am just a beginner. I also suspect, perhaps incorrectly, that any piece of good writing cannot be planned; it must *flow*. And even if it could be planned, I'm not smart enough to do it.

I wrote it, however, with one goal in mind: to take you on an adventure. In contrast to mathematical writing in textbooks and papers, I didn't carefully and deliberately structure the chain of arguments and assumptions while pretending that the entire flow of events is obvious. I tried to convey the feeling of getting lost and getting back on track, a feeling familiar to anyone solving any relatively tricky problem. A few times, I really was lost and confused. See, I wrote this largely out of (a faulty) memory and, having forgotten many crucial proof details, ended up having to revisit the relevant concepts again in the act of writing. I kept some of these little excursions so that I could more accurately convey the process of proving. My hope is that this approach leads you to deeper insights. I learned a lot about the subject matter in writing this and I hope you do too, regardless of previous background.

Lastly, I have no feeling for how accessible this is to readers with little mathematical background. I apologize if my mediocre pedagodical skills are on too bold a display.

## Prelude

I took Abstract Algebra in the third semester, as a CS student with a Minor in Mathematics, but that wasn't my first encounter with it. I was at the time overambitious and thought it was a manageable first semester course to dump into my already overfull bucket of classes (I had exceeded the credit recommendation anyway by taking Analysis too). I ended up dropping it soon after.

*(Amusing anecdote: I thought the Group Theory I had picked up before dropping the class was enough for the puny, applied group theory in my mandatory Discrete Maths class--Euclid's Extended Algorithm & the like--so I didn't bother explicitly preparing for that part of the exam. You can guess how that went.)*

Parallel to my university's lectures, I watched Harvard's lectures too, as the professor, Benedict Gross, had more entertainment to offer than the sterile style of my lecturer. My ears were, and still are, more welcoming of English than German, the latter being the instruction language of the class.

How this blog post's subject matter was handled in Gross' lectures is what prompted the post, almost 5 years later.

## Complex integers

You've presumably heard of Complex numbers. There are the Complex "integers" too. They are the subset of Complex numbers whose components are integers.

$$
\mathbb{Z} + \mathbb{Z}i =: \mathbb{Z}[i] =: \mathbb{K}
$$

To hide some of Algebra's sharp teeth for now so as not to scare you, I'll call the set of those integers $\mathbb{K}$, for there are as many letters between **K** and **Z** as there are between **C** (for complex) and **R** (for real). (Easter egg: K represents the sound of the first letter of the first name of the mathematician after whom they're usually named.)

Much like the complex numbers can be visualized on a 2D plane, the complex integers can too. (They form, after all, a subset of $\mathbb{C}$.) In fact, their discreteness allows for a more familiar representation: a lattice. To a New Yorker, each element of $\mathbb{K}$ is an intersection of a street and an avenue.

![Gaussian integer  Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9e/Gaussian_integer_lattice.svg/1200px-Gaussian_integer_lattice.svg.png)

The complex integers also inherit some operations from $\mathbb{C}$, namely addition and multiplication. Subtraction, which algebraically is nothing but the inverse of addition, is also possible. But, and this is where the adventure begins, division is not. See, just as one cannot divide all integers ($5 \div2$ is not equal to any integer), one cannot divide all complex integers ($5\div2$ is not equal to any Complex integer either). However, as every third-grader learns, you can certainly write:

$$
5\div2 = 2 \quad \text{remainder: } 1
$$

Namely, the integers admit a more restricted form of division, called division with remainder. One could also have written

$$
5\div2 = 1r[3]
$$

(Or the even more trivial fact: $5\div2 = 0r[5]$.)

Yet, for the operation to have any meaning, it is required that the remainder always be smaller than the divisor. In the integers, it is always possible to find such a quotient and remainder for any integers $a$ and $d \neq 0$. For example, starting with $q=1$, one can repeatedly calculate the remainder $a - dq$ and compare it with $d$, the divisor. If the remainder is bigger, $q$ is incremented. Eventually, $a-dq$ will be smaller than $d$ (but **positive**) as $q$ increases.

(Should the curious among you ask if there are any algebraic structures where some concept of remainderless division—*divisibility* in other words—exists, but where remainder with division is not possible, I am pleased to say that yes, such structures exist. For example: $\mathbb{Z}[\frac{1+\sqrt{-19}}{2}]$.)

It is natural to ask the same question about the Complex integers, since we are after all calling them integers. Are they, too, like the integers in this sense? *Can we divide with remainder in $\mathbb{K}$?*

### Division with remainder in $\mathbb{K}$

Before we answer that, we need to set some other things in order. We have to establish a notion of size in $\mathbb{K}$, else we won't be able to speak of the remainder being smaller than the divisor, without which division with remainder makes no sense.

One very natural way to talk about the size of a Complex integer is to look at the 2D representation of these numbers. A number like $3+4i$ is represented by a vector starting at the origin and ending at the point $(3,4)$. (See the figure below.) The length of this vector is $\sqrt{3^2+4^2}=\sqrt{25}=5$. Not coincidentally, this is the notion of size in the Complex numbers $\mathbb{C}$, so it makes sense to use this for $\mathbb{K}$ as well. Namely, we can define the size of $a+bi$ to be $\sqrt{a^2+b^2}$.

![](file:///Users/ujkan/Desktop/screenshots/Screenshot%202024-02-18%20at%2020.47.05.png?msec=1711799609405)

However, to avoid the hassle of dealing with square roots, we actually define the size (or *norm*) as:

$$
N(a+bi) = a^2 + b^2
$$

Using this, let us now investigate division with remainder in $\mathbb{K}$. We start with the simple case where the divisor is an integer, e.g. $(10+4i) \div 3$. As a first attempt, let us divide each component of the dividend separately by $3$. We have

$$
10 \div 3 = 3r[1]
$$

and

$$
4 \div 3 = 1r[1]
$$

Combining these would suggest that the answer is:

$$
(10 + 4i) \div 3  = 3 + i \quad \text{remainder: } 1+i
$$

which satisfies

$$
N(1+i) = 1^2 + 1 ^2 = 2 < 3^2 = N(3)
$$

which is indeed what we wanted.

Does this always work? Well, before looking for a counterexample, let's do some algebra. Let $a+bi$ be some dividend, $d$ some divisor. Additionally, let $r_a$ be the remainder of $a \div d$ and $r_b$ that of $b \div d$. The combined remainder is $r = r_a+r_bi$, so $N(r) = r_a^2 + r_b^2$. Since $r_a$ and $r_b$ are smaller than the divisor $d$ by definition of division in the integers $\mathbb{Z}$, we have $r_a^2 + r_b^2 < d^2 + d^2 = 2d^2$. But the norm of the divisor $d$ is $N(d) = d^2$, so we can't deduce that $N(r) < N(d)$.

This seems...confusing? Didn't we just demonstrate that the method works for $(10+4i)\div3$? How come algebra is saying this *can't* work? Well, the algebra isn't saying it *can't* work. See, it's only saying that only knowing that $r_a < d$ and $r_b < d$ isn't enough to prove $N(r) < N(d)$. With the help of some additional relations, like $r_a^2 = r_a = 1 = r_b^2 = r_b$ in the case of $(10+4i)\div3$, one can of course deduce $N(r) < N(d)$.

We can now look for a counterexample to our method; it may just give us an insight into where it falls apart, which will help us find what additional relations or constraints are necessary for a method to be bulletproof.

For our counterexample, we need, in essence, a case where both components $r_a$ and $r_b$ of the remainder are the result of a normal integer division, i.e. smaller than the divisor $d$, but where the entire remainder $r=r_a+r_bi$ is not smaller than the divisor $d$, namely $N(r) = N(r_a + r_bi)=r_a^2 + r_b^2 \geq d^2$. It's easy to see that $r_a=r_b=3$ and $d=4$ satisfy the two conditions. We can now pick any quotient we like, so we choose a simple one: $1+i$. Combining these three facts, we obtain the dividend by multiplying together the quotient and the divisor and adding the remainder on top. That is, $4\times(1+i) + (3+3i) = 7 + 7i$.

It is evident that $q=1+i$ and $r=3+3i$ is exactly what we would have arrived at with our method when dividing $7+7i$ by 4, since $7\div4=1r[3]$. The problem arises because, in this division of integers, the remainder $3$, although smaller than the divisor $4$, is not *much* smaller than $4$. But, is there an even smaller remainder than $3$? Well, let's adjust the quotient and see what comes out. If the quotient were $0$ instead of $1$ then the remainder would be $7$, which is even larger, and if the quotient were $2$, we'd have $2\times4=8$ so the remainder is $7-8=-1$, but we can't have a negative remainder...or can we?!

### Revisiting remainders

Recall that the crucial point in division with remainder is that the remainder is smaller than the divisor. Negative numbers are smaller than any positive number, so by allowing negative remainders one could just as well have written

$$
7\div4=10r[-33]
$$

since $-33 < 4$. But what does the minus sign mean in the context of division anyway? I mean, look at $-7 \div (-3)$. If we ignore the signs and go for the same quotient as in $7\div3$, we obtain $-7\div(-3)=2r[-1]$, a negative remainder. If we insist on a positive remainder, we get $-7\div(-3)=3r[2]$, but $2 > -3$. So we're in a bit of a pickle.

It is evident that our initial notion of size in the integers doesn't work that well. What if we borrow the one from $\mathbb{K}$? Namely, what if we treat integers as distances from $0$. This is of course the familiar concept of *absolute value*. Luckily, this cures our headache quite neatly: both $2r[-1]$ and $3r[2]$ are valid results, since $|-1| < |-3|$ and $|2|<|-3|$. This also implies that we're perfectly justified in writing $7\div4=2r[-1]$, since $|-1| < 4$.

If this ambiguity bothers you, think about the fractional result of $7 \div 4 = 1.75$. This number can either be rounded up to $2$ (producing remainder $-1$) or rounded down to $1$ (producing remainder $3$). In some sense, both these operations are valid: they result in small enough remainders. They also show that there can only be two possible small enough remainders, so the ambiguity is not uncertain, but predictable.

Let's now return to the division $(7+7i) \div 4$. Applying the result above, we obtain

$$
(7+7i) \div 4 =(2 + 2i)r[-1 - i]
$$

where $N(-1-i) = 1^2 + 1^2 = 2 < 16 = 4^2 = N(4)$, which indeed is correct.

We now argue that this approach always works. Observe that, of the two possible *valid* (i.e. small enough) remainders (one positive and one negative), at least one of them is **in absolute value** smaller than or equal to half of the divisor. Visually, this is immediately obvious, as seen below, where both $r_+$ and $r_-$ are within a window of $d$ (between $4d$ and $5d$), but $r_+$ is smaller than half of the window.

![](file:///Users/ujkan/Library/Application%20Support/marktext/images/2024-03-22-00-27-39-image.png?msec=1711799609387)

And algebraically? Well, think about the relation between divisor and the two remainders $r_+$ and $r_-$. The negative remainder $r_-$ is obtained by exactly increasing the quotient which produces $r_+$ by $1$, which means taking one more step of length $d$. This extra step eats into the existing remainder $r_+$, leaving now a new remainder $r_{-}$ which is equal to $r_+ - d$. Therefore

$$
r_+ - r_- = d \\
\text{or} \\
|r_+| + |r_-| = d
$$

where $\vert r_+ \vert < d$ and $\vert r_- \vert < d$. Assume both are larger than $\frac{d}{2}$, i.e. $|r_+| > \frac{d}{2}$ and $|r_-| > \frac{d}{2}$. Summing them up yields $d = \vert r_+ \vert + \vert r_- \vert > d$, which is a contradiction.

Hence, to divide $a+bi$ by an integer $d$, divide $a$ and $b$ by $d$ respectively, each time obtaining the smaller remainder, i.e. the one for which $|r|\leq\frac{d}{2}$ holds. Then the following holds:

$$
N(r) = N(r_a+r_bi) = r_a^2 + r_b^2 \leq \frac{d^2}{4} + \frac{d^2}{4} = \frac{d^2}{2} <d^2=N(d)
$$

### The "complicated" division case

Trickier, however, is division by a Complex integer that has both an integer and an imaginary component, like $2+i$. Consider, for example, the result of $9 \div (2+i)$. For starters, it's hard to intuit what it even means to divide by $2+i$, a difficulty not at all present in the division of integers, which has a direct correspondence to the real world. That immediately makes it more difficult to find some sort of iterative procedure that enables us to start with a quotient and increment it until the remainder is smaller than the divisor, like we did for the integers. Theoretically, we could start with all complex integers of norm 1 and then move on to all those of norm 2, and so on and so forth, in each step checking to see if the remainder's norm is smaller than that of the divisor, but even then it's not immediately clear that we'd end up finding a small enough remainder. Closer inspection does nonetheless reveal that this is indeed possible, but that approach is too tedious. We opt for something *neater*. The motivated and adventurous reader may certainly like to walk the untrodden path, in which case I offer a small hint: the norm is a *homomorphism*.

As mentioned, we put aside geometric interpretations. To do the algebra, we need to use some intro-level facts about the Complex numbers $\mathbb{C}$. When dividing $9$ by $2 + i$ there, we *normalize* the denominator by multiplying it with its *conjugate*, but at the same time multiply the numerator by the same quantity in order to leave the term unchanged, i.e.

$$
\frac{9}{2+i}\cdot\frac{2-i}{2-i}= \frac{18-9i}{N(2+i)}=\frac{18-9i}{5}
$$

In essence, we can reduce division by $1+i$ to division with an integer—the *norm* of the divisor in fact. Applying the same technique as above, we get

$$
(18 - 9i) \div 5 = (4 - 2i)r[-2+i]
$$

We are guaranteed, of course, that each component of the remainder $-2+i$ is at most half the divisor $5$, which we can easily check:

$$
|-2| \leq 2.5 = \frac{1}{2}\times 5 \\
|1| \leq 2.5 = \frac{1}{2}\times 5
$$

This leads us to conclude

$$
N(-2+i) = (-2)^2 + (1)^2 \leq \left(\frac{1}{2}\times5\right)^2 + \left(\frac{1}{2}\times5\right)^2 = 2 \times\frac{1}{4}\times5^2=\frac{1}{2}\times5^2
=\frac{1}{2}N(5)
$$

which is the same statement as above but for $\mathbb{K}$ instead of $\mathbb{Z}$.

But, we are trying to divide $9$ by $2+i$ and the remainder $-2+i$ is not at all smaller than $2+i$. They are, in fact, the same size. So how has that reformulation of $9\div(2+i)$ into $(18-9i) \div 5$ helped us? Well, let's rewrite

$$
(18 - 9i) \div 5 = (4 - 2i)r[-2+i]
$$

as

$$
18-9i = 5\times(4-2i) + (-2+i)
$$

Using how $18-9i$ and $5$ came about, we obtain

$$
9 \times(2-i) = (2+i)(2-i)\times(4-2i) + (-2 + i)
$$

Dividing both sides by $2-i$ yields

$$
\begin{aligned}
9 &= (2+i)\times(4-2i) + \frac{-2+i}{2-i}\\
&=(2+i)\times(4-2i) - 1
\end{aligned}
$$

In other words, dividing $9$ by $2+i$ results in the quotient $4-2i$ and the remainder $-1$, where $N(-1) = 1^2 = 1 < 5 = N(2+i)$.

You might ask: were we just lucky that the remainder $-2+i$ of $(18-9i)\div5$ just so happened to be divisible by $2-i$? Can we be sure that we can always divide both sides cleanly as we did above?

Observe once more the division equation of $(18-9i)\div5$:

$$
\begin{aligned}
9\textcolor{red}{(2-i)} &= (2+i)\textcolor{red}{(2-i)}(4-2i) + (-2 + i)\\
9\textcolor{red}{(2-i)} -(2+i)\textcolor{red}{(2-i)}(4-2i) &= -2+i \\
\textcolor{red}{(2-i)}(9 - (2+i)(4-2i)) &= -2+i
\end{aligned}
$$

It is evident that $-2+i$ is divisible by $2-i$. The quotient is $9-(2+i)(4-2i)$, clearly a Complex integer.

More interestingly, it's rather clear that we didn't need to make use of the fact that $-2+i = -(2-i)$ in proving divisibility. This is an indicator that we didn't get lucky with our choice of Complex integers, that this approach works in the general case. Indeed, a proof of this fact is straightforward. Let $k$ be the integer dividend (in place of $9$) and $z = a+bi$ be the divisor (in place of $2-i$). We then obtain

$$
\frac{k}{a+bi}\cdot\frac{a-bi}{a-bi}=\frac{k(a-bi)}{a^2+b^2}
$$

We denote $d = a^2+b^2$ (an integer) and thus divide $ka-(kb)i$ by $d$, which should yield a quotient $q=q_a + q_bi$ and a remainder $r = r_a+r_bi$, which is smaller than $d$ (using the *norm* conception of size). That is

$$
\begin{aligned}
k(a-bi) &= \textcolor{red}{d}q + r \\
&=\textcolor{red}{(a+bi)(a-bi)}q + r\\
&=\textcolor{red}{z(a-bi)}q+r
\end{aligned}
$$

Pulling $z(a-bi)q$ to the other side results in

$$
\begin{aligned}
r &= k\textcolor{red}{(a-bi)} - z\textcolor{red}{(a-bi)}q\\
&=\textcolor{red}{(a-bi)}(k - zq)
\end{aligned}
$$

Therefore $r$ is always divisible by $a-bi$, being in fact equal to $k - zq$. The result of this division the remainder that we're looking for, the remainder of the division of $k$ by $a+bi$. Call this remainder $R :=k-zq$, with $r=(a-bi)R$

The final question is (naturally): is $R$ a small enough remainder, i.e. does $N(R) < N(z)$ hold? Let's take a step back and look at our initial remainder $r$, which was the result of a division with $d=a^2+b^2\in\mathbb{Z}$. As we've established above, this means that $r$ is smaller (in the *norm*) than $d$, i.e. $N(r) < N(d)$. Expanding $N(d)$ results in $N(d) = N(a^2+b^2)$, but recall that $a^2+b^2 = N(a+bi)$, hence $N(a^2+b^2)=N(N(a+bi))$ and, given that the norm is always an integer, we have $N(N(a+bi))= N(a+bi)=N(z)^2$. In conclusion: $N(r) < N(z)^2$.

So, in some sense, we need to combine the equivalence $r=(a-bi)R$ and $N(r) <N(z)^2$ to show $N(R) < N(z)$. Our goal already hints to the fact that $R$ is potentially smaller than $r$. This is, of course, intuitive, since $r$ is the product of $(a-bi)R$ and, generally, multiplying a number by another makes it larger. The exception here are obviously *fractions*, but the whole point of this chain of argumentation is that the Complex integers are just a *kind of integer*, and there are no fractions in the integers.[^1]

Let's try to mathematically capture the notion that multiplying two Complex integers produces a larger Complex integer. As usual, we start with the ordinary integers. What does it mean for the product of two integers to be larger than the two multiplicands? Just how much larger is this product? Well, $6$, the product of $2$ and $3$ is, for example, exactly $3$ times larger than $2$ (and vice versa). In other words, the *size* of $6$ is exactly the product of the sizes of $3$ and $2$. This sounds funny because we're using the integers themselves to talk about the size of integers. Our common intuition is that integers are a measure of size and that multiplication is a measure of "by how much", so the question "by how much is the product larger than the multiplicands" is answered *by definition*! In other words:

$$
|ab| = |a||b|
$$

Does this generalize to the Complex integers? Namely, is it also true that

$$
N(z_1z_2)=N(z_1)N(z_2)
$$

(This is the same as asking: "Is $N$ a *homomorphism*?")

Well, let's calculate it step-by-step.

$$
\begin{aligned}
&N(z_1z_2)\\
=\,&N((a_1+b_1i)(a_2+b_2i))\\
=\,&N((a_1a_2-b_1b_2) +(a_1b_2 + a_2b_1)i)\\
=\,&(a_1a_2-b_1b_2)^2 + (a_1b_2+a_2b_1)^2\\
=\,&a_1^2a_2^2\textcolor{red}{-2a_1a_2b_1b_2} + b_1^2b_2^2 + a_1^2b_2^2 \textcolor{red}{+2a_1a_2b_1b_2} + a_2^2b_1^2\\
=\,&a_1^2a_2^2 + b_1^2b_2^2 + a_1^2b_2^2 + a_2^2b_1^2\\
=\,&a_1^2(a_2^2+b_2^2)+a_2^2(a_2^2+b_2^2)\\
=\,&(a_1^2+a_2^2)(a_2^2+b_2^2)\\
=\,&N(a_1+b_1i)N(a_2+b_2i)\\
=\,&N(z_1)N(z_2)
\end{aligned}
$$

And, just like that, we've reached another milestone. How does this apply to our problem? Well, if $r = (a-bi)R$, then

$$
N(r)=N(a-bi)N(R)=(a^2+b^2)N(R)=d\times N(R)=N(z)N(R)
$$

Which means

$$
N(R) = \frac{N(r)}{N(z)}
$$

and since $N(r)<N(z)^2$

$$
N(R) < \frac{N(z)^2}{N(z)} = N(z)
$$

### And thus, we have divided

Let's have a look at our path to the summit from above. In our journey to establishing division with remainder in $\mathbb{K}$, we started by defining a notion of size which would allow us to speak of a remainder being smaller or larger than a divisor.

Our next step was to investigate the division of a Complex integer $a+bi$ by an ordinary integer $d$, where we established that constructing the remainder of this division with the remainders of the division of the two components $a$ and $b$ by $d$ didn't *always* work. We had to pluck the smaller of the two possible remainders in any divison of integers in order for our constructed remainder to be small enough.

We then turned our attention to dividing by any Complex integer $a+bi$, which we saw was an operation reducible to division by an ordinary integer through multiplying both numerator and denominator by $a-bi$. Our last challenge was to find a relation between this second remainder and the remainder we were looking for in the divison by $a+bi$ and to prove that this remainder was small enough. In trying to meet this challenge, we needed to establish another crucial fact about the *norm*, which is that it's multiplicative. That is, $N(z_1z_2)=N(z_1)N(z_2)$ which is an analogue of the all-too-familiar equation $ \vert ab \vert = \vert a \vert  \vert b \vert $.

[^1]: This is a case of using what we want to prove to help us prove it, but doing so **indirectly** by using e.g. the assumption that the Complex integers are "integers" to help us create new hypotheses which, once proven to be true, can help us prove the main goal, i.e. that the Complex integers admit the same kind of division as the integers. This indirectness is crucial: using the goal as an assumption in deducing the goal itself is of course paradoxical. Our indirect use has to do with the *meta*, the human process of proving itself. It aids us in narrowing the set of paths we could take and in getting unstuck.

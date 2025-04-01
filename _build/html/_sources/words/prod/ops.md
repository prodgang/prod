(sections:prod:ops)=
# Operate

The [previous section](sections:prod:iso) showed we can write any natural number uniquely as a prod. That's great. But what can we do with prods? 

In this section, we'll take a look at some extremely simple operations that do some extremely cool things. But first, let's take a look at some bad operations.

## Counter-productive operations

My criteria for a bad operation is that it cannot be defined in a form that's coherent with productive numbers themselves. We'll see that counting is a bad operation - hence counter-productive. Haha.

### Addition

Recall that [Peano arithmetic](sections:numbers:peano) kicks off by defining addition. How do you think we could define addition in productive arithmetic? 

The quick answer is that you can't. Just adding one to a number will change its factorization properties in very unpredictable ways. Basically all you can guarantee is that its factors will be completely different. So its not gonna happen. I don't know how to formally prove this, so if you don't believe me just try it yourself.

### Multiplication

Next operation: multiplication. There's a very good case that you should be able to define multiplication productively: the fundamental idea behind prods is multiplying primes so that's kind of what they're all about. We can even see this happen with an example. Take a look at the trees of $4,3,12$ and remember that $12 = 4 \times 3$:


```{image} ../../tikz/p4.svg
:alt: 4 as tree
:align: left
```
```{image} ../../tikz/p3.svg
:alt: 3 as tree
:align: center
```
```{image} ../../tikz/p12.svg
:alt: 12 as tree
:align: right
```




You can literally see how four and three are just attached to each other side by side to give $12$! Indeed, any time $x,y$ don't share any factors (i.e. are coprime), you can multiply them side-by-side like this. However, when they *do* share factors, then we're back to the classic equation: $a^b \times a^c = a^{b+c}$. So multiplication reduces to addition. So multiplication is counter-productive.

### Expontentiation

There's a similar story for exponentiation. While you can get away with writing $2^x$ as $[x]$ and even $6^x = [x, x]$, as soon as you have nested powers you have to eventually use the fact that $(x^y)^z = x^{y \times z}$. So expontentiation reduces to multiplication. So expontention is counter-productive. And so on.

It's kind of interesting that none of the usual arithmetic operations work. Even though these counter-examples were not hard to find, it would have been reasonable to expect that defining prods based on taking the product of prime powers would at least allow you to do products and powers. But you can't. So we need to think more carefully. 

### List operations

A fun way to test the rapidly developing abilities of language models is to try to get them to recreate prod arithmetic from scratch. Its a useful test case because there's been no trace of prods on the internet (until now) and so they really are required to work things out from scratch, as opposed to memorizing the thousands of training examples they've seen. In the past few years, they've gone from being incapable of consistently writing numbers productively to proving {prf:ref}`ftpa` given only the axioms.

However, even the newest models continue to suck at coming up with productive operations. What usually happens is they propose some additive operation, I repeat the argument from above to show its not productive and then they switch to list based operations. 

For example, given two lists you can *concantenate* them which just means stick one on the end of the other one. So $[a, b, c] + [d, e] = [a, b, c, d, e]$. But this is not a productive operation because it does not respect the padding axiom {eq}`PRODPAD`: you can pad then concatenate to get $[0] + [[]] = [0, []]$ or you can concatenate then pad to get $[] + [[]] = [[]] = [[], 0]$, which is very different. 

So operations that are natural for lists are not necessarily productive.

## Productive operations

Let's take a step back. Rather than trying to reinvent the wheel, let's just find the simplest possible productive operations and see what they end up doing. 

### Grokking Graft

The simplest prod is $0$ and the simplest thing to do with $0$ is nothing. So let's define an operation that does nothing with zero:

```{math}
:label: GRAFT0
   0 \sqcup x = x = x \sqcup 0
```

I've chosen the $\sqcup$ symbol to suggestively look like the set union symbol, and made it square because prod has square vibes. But {eq}`GRAFT0` isn't enough for a fully fledged operation, because what happens to nonzero prods? What about the simplest possible thing:

```{math}
:label: GRAFT1
   [x_1, ..., x_n] \sqcup [y_1, ..., y_n] = [x_1 \sqcup y_1, ..., x_n \sqcup y_n]
```
On trees this looks like:
```{image} ../../tikz/cup1.svg
   :alt: cup tree
   :align: center
   :width: 500px
```

So it's recursive! All {eq}`GRAFT1` does is the pass the work down one level. But that's enough because all prods eventually end with zeros and then {eq}`GRAFT0` kicks in. By the way, you can safely assume that $x$ and $y$ are both the same length in {eq}`GRAFT1` by padding the shorter one with zeros. 

```{admonition} Historical Clarification
Just because I'm currently claiming this is the simplest possible operation, doesn't mean it was the first one I wrote down! In fact, the first operation I came up with was not well-defined. I found this out by trying to get python to compute it for me on the first 50 numbers. Python complained, so I mindlessly messed around with the base cases until something worked. The end result was something that could be eventually boiled down to {eq}`GRAFT0` and {eq}`GRAFT1`. So python deserves the credit for this one.
```

Let's see it in action! Here's a detailed walkthrough for how to compute $4 \sqcup 3$:
```{image} ../../tikz/egcup1.svg
   :alt: cup tree
   :align: center
   :width: 500px
````


Here's a more complicated example: $40 \sqcup 90$ (remember that $40 = 2^3 \times 5$ and $90 = 2 \times 3^2 \times 5$):
```{image} ../../tikz/egcup2.svg
   :alt: cup tree
   :align: center
   :width: 750px
````

The trick is to start off with everything padded so that they have roughly the same shape, then work bottom-up. Here's a few more examples:


```{list-table}
:align: center 
:header-rows: 1
:widths: auto
* - $x$
  - $y$
  - $x \sqcup y$
  - as numbers
* - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
         :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - $2 \sqcup 2 = 2$
* - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p3.svg
        :alt: 3 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p6.svg
        :alt: 6 as tree
        :height: 50px
        :align: center
    ```
  - $2 \sqcup 3 = 6$
* - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p4.svg
        :alt: 4 as tree
        :height: 100px
        :align: center
    ```
  - ```{image} ../../tikz/p4.svg
        :alt: 4 as tree
        :height: 100px
        :align: center
    ```
  - $2 \sqcup 4 = 4$
* - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p5.svg
        :alt: 5 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p10.svg
        :alt: 10 as tree
        :height: 50px
        :align: center
    ```
  - $2 \sqcup 5 = 10$
* - ```{image} ../../tikz/p4.svg
        :alt: 2 as tree
        :height: 100px
        :align: center
    ```
  - ```{image} ../../tikz/p8.svg
        :alt: 3 as tree
        :height: 100px
        :align: center
    ```
  - ```{image} ../../tikz/p64.svg
        :alt: 64 as tree
        :height: 100px
        :align: center
    ```
  - $4 \sqcup 8 = 64$
```

If you can't see the pattern yet, I encourage you to try some examples out yourself either by hand or with [this code](sections:draw:ops).

The easiest way to understand $x \sqcup y$ is to imagine placing $x$ on top of $y$ and keeping all the longest branches. When botanists merge trees together like this its called grafting, so I call $x \sqcup y$ the **graft** of $x$ and $y$. 

If you look at the final column of the table, you might notice some other patterns: 
1. When $x$ and $y$ don't share factors, they are multiplied.
2. $x \sqcup x = x$. You can see the proof of that below, which is also our first example of a purely productive proof.
3. When $x \neq y$ but they do share some factors, those factors are combined. 

````{dropdown} Click me for proof of idempotence

This is our first instance of productive induction!

Remember from [here](sections:numbers:induction) that additive induction proves something for every number by showing that it holds for $0$, and that if it holds for $n$ then it holds for $n+1$. 

So productive induction is very similar: first show that some property holds for $0$. Then assume that it holds for $x_1, ..., x_n$ and show that it holds for $[x_1, ..., x_n]$. Since all prods are built in such a way, this proves the property holds for every prod.

```{prf:theorem}
:label: graftidem
$x \sqcup x = x$
```

```{prf:proof} 

   Base case ($x=0$): $0 \sqcup 0 = 0$ by {eq}`GRAFT0`.

   Inductive step ($x = [x_1, ..., x_n]$): Assume for inductive hypothesis that $x_i \sqcup x_i = x_i$, for every $i \leq n$. 

   Then $x \sqcup x = [x_1, ..., x_n] \sqcup [x_1, ..., x_n] = [x_1 \sqcup x_1, ..., x_n \sqcup x_n] = [x_1, ..., x_n] = x$, where the second equality comes from {eq}`GRAFT1` and the third from IH. 
   
   Done.
```

````


Those properties make grafting look a lot like LCM. I initially thought they were the same. But my trusty method of making wildly optimistic conjectures then getting python to check on the first 50 numbers showed me a very crucial difference: LCM takes the additive max of the exponents, while graft takes the graft of the exponents (because its recursive). This has dramatic consequences: $lcm(4, 8) = 8$, but $4 \sqcup 8 = 64 = 2^6$. In this case, the exponents were multiplied but that's just because the exponents $2$ and $3$ don't share factors (try out an example where they do like $4 \sqcup 16$). 

We'll see in the [next section](sections:lattice) that graft shares a lot of *algebraic* properties with LCM, but hopefully you can nevertheless appreciate that they are very different functions indeed. I do not recommend trying to interpret graft additively.

### ... and prune

We've seen with graft that a very simple definition can produce quite a cool operation. So why not do it again? There's a very natural dual operation to graft, which I will denote $x \sqcap y$, that can be defined as follows:

```{math}
:label: PRUNE0
   0 \sqcap x = 0 = x \sqcap 0
```

```{math}
:label: PRUNE1
   [x_1, ..., x_n] \sqcap [y_1, ..., y_n] = [x_1 \sqcap y_1, ..., x_n \sqcap y_n]
```

This is almost identical to graft. The only real difference is that the base case {eq}`PRUNE0` destroys branches where {eq}`GRAFT0` preserves them. Since lopping branches off trees is called pruning, I call the operation $x \sqcap y$ the **prune** of $x$ and $y$. Here's a new table of examples:

```{list-table}
:align: center 
:header-rows: 1
:widths: auto
* - $x$
  - $y$
  - $x \sqcap y$
  - as numbers
* - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
         :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - $2 \sqcap 2 = 2$
* - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p3.svg
        :alt: 3 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p1.svg
        :alt: 1 as tree
        :height: 25px
        :align: center
    ```
  - $2 \sqcap 3 = 1$
* - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p4.svg
        :alt: 4 as tree
        :height: 100px
        :align: center
    ```
  - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - $2 \sqcap 4 = 2$
* - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p5.svg
        :alt: 5 as tree
        :height: 50px
        :align: center
    ```
  - ```{image} ../../tikz/p1.svg
        :alt: 1 as tree
        :height: 25px
        :align: center
    ```
  - $2 \sqcap 5 = 1$
* - ```{image} ../../tikz/p4.svg
        :alt: 2 as tree
        :height: 100px
        :align: center
    ```
  - ```{image} ../../tikz/p8.svg
        :alt: 3 as tree
        :height: 100px
        :align: center
    ```
  - ```{image} ../../tikz/p2.svg
        :alt: 2 as tree
        :height: 50px
        :align: center
    ```
  - $4 \sqcap 8 = 2$
```

Hopefully you can see that pruning is very similar to GCD. In particular, $gcd(x, y) = 1$ iff $x \sqcap y = 1$. Once again there's some important differences: for example, $gcd(4, 8) = 4$ but $4 \sqcap 8 = 2$. As before, you can play around with [the code](sections:draw:ops) if you want. 

Here's a brief highlight of some other properties of these operations. If you don't know what the words mean, don't worry about it.
- Like any mergey operation worth its salt, graft is a commutative monoid. 
  - The identity is obviously $0$ because of the base case {eq}`GRAFT0`. But $[]$ is also the identity on everything else, which you can check for yourself.
  - I spent the longest time trying to make it a group, because at the time groups were the only structure I was familiar with, but you can't. Because of the idempotence, for one thing.
- Although its not the least, graft does give you a common multiple. Similarly, prune gives you a (not-necessarily-greatest) common divisor. 
- Prune distributes over graft! I'll prove this in the next section, but perhaps you were already wondering. 
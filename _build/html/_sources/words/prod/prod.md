(sections:prod)=
# Productive Numbers

Recap so far:
1. Numbers are additively axiomatized in [Peano Arithmetic](sections:numbers) (PA)
2. [Additive numbers](sections:algebra:additive) are boring

**So what happens if we axiomatize numbers, but without counting?** Productive Numbers! That's literally the whole idea. The rest of the book is about what happens when you do. It's up to you to decide if it's still boring.

## Factorization

Behind the scenes, the reason PA works is because of the following basic fact:
````{prf:theorem} 
:label: ftaa
$n = 1 + 1 + ... + 1$ ($n$ times)
````
Though extremely dull, this is nice because it shows how to additively represent any number using only more basic numbers.

For productive numbers to work, we're gonna need a similar guarantee that we can productively represent any number. Thankfully, we don't have to look too far. There's a niche little result called *The Fundamental Theorem of Arithmetic* that fits the bill perfectly. 

````{prf:theorem} 
:label: fta

For any number $n > 1$, $n$ can be factored as $n = 2^{e_1} \times 3^{e_2} \times ... \times p_k^{e_k}$, where $p_k$ is the $k$th prime number and $e_i \geq 0$. This is unique up to the ordering of primes and inclusion of $e_i = 0$.
````
Those $e_i$ guys are going to play an important role, and I will call them the *exponents* of $n$. 

In short, any number can be uniquely written as the product of some primes. That it can be done at all is obvious - if a number can't be decomposed then it's a prime so we're done. The interesting part is that this can be done uniquely which means you can't have two different ways of writing the same number (excluding the boring edge cases like $2 \times 3 = 3 \times 2 = 3 \times 2 \times 1$).

## Productivization

So the most obvious way to write $n$ productively would be $[e_1, e_2, ..., e_k]$. The $i$th value in the list is just the exponent of the $i$th prime.

Then $6$ would be $[1, 1]$, $8$ would be $[3]$ (because $8 = 2^3$) and $20$ would be $[2, 0, 1]$. Sounds pretty good right?

Well, no. It took me about a year to realize, but there is a big problem with this definition that basically defeats the entire point. I'll let you think about what the problem is and how to fix it (not necessarily for a year) before moving to the next part.

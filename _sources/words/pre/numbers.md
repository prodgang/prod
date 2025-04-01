(sections:numbers)=
# Numbers


Everyone knows what numbers are. County things. But what does that really mean?

(sections:numbers:peano)=
## Peano Arithmetic 

A lot of maths is about taking a very obvious concept and giving it a meticulous definition. This process is called *axiomatization*. Naturally, mathematicians have spent quite a lot of time axiomatizing numbers. 

Numbers are so fundamental that you can't really define them in terms of anything else. So you basically have to start from nothing. Conveniently, nothing is itself a number: *zero*. So the first stage of axiomatizing numbers is to simply demand that zero is a number. Symbolically,

```{math}
:label: PA0
    0 \in \mathbb{N} 
```

OK great. We have our first number. The next stage of axiomatizing numbers is to come up with a way of making old numbers from new numbers. The idea is to have a function that takes a number $n$ to the 'next' number. This is called the successor function, written $S(n)$. You can think of the successor function as adding one, but technically we are yet to define what one is or what addition is and so aren't allowed to call it that yet. Instead, we can now say that $S(0)$ is a number and that this is the *definition* of one. Then we can get $S(S(0))$ and call it two. And so on and so on and so on. In summary, if $n$ is a number, then so is $S(n)$. Symbolically, this is:

```{math}
:label: PA1
    n \in \mathbb{N}  \implies S(n) \in \mathbb{N} 
```



Intuitively, we think of numbers arranging themselves on a line that stretches out foreover. We know this line continues forever because we know we can always just add another one on the end. But $S$ doesn't know that yet, so we have to give it a rule so that it never produces an old number and makes numbers go in circles. A concise way of expressing this is that different numbers have different successors. Symbolically,

```{math}
:label: PA2
    n \neq m \implies S(n) \neq S(m) 
```

That just about completes our definition of numbers. All we need now is something to do with them. Let's try addition. Take a moment to think about what adding really means and try to find a way of expressing it using only $0$ and $S$. Once upon a time, some dude called Peano did exactly this and managed to come up with the following two conditions. Actually, there's some disagreement about whether it was Peano or some other dude called Dedekind. But who cares - they're both dead now anyway. What lives on are the following two equations:


```{math}
:label: PA3
    0 + m = m 
```


```{math}
:label: PA4
    S(n) + m = S(n+m) 
```

The equation {eq}`PA3` shouldn't come as much of a surprise. The second equation {eq}`PA4`, is a little weirder. Doesn't using $+$ on both sides of the equals sign mean we're defining addition in terms of itself? Well yes, but also no. We are defining addition in terms of itself, but also in such a way that if you keep applying {eq}`PA4`, you'll keep peeling of layers of $S$ from the left of $+$ until you hit $0$. That's where {eq}`PA3` comes in. Such symbolic witchcraft is called *recursion*. Let's see it in action as we prove our first theorem!

````{prf:theorem} 
:label: oneplusone
$1 + 1 = 2$
````

````{prf:proof} (Baby's First Theorem)

Remember that $1$ is defined as $S(0)$. So start with 

$S(0) + S(0)$

Now set $n = 0$ and $m = S(0)$, so that we can apply {eq}`PA4` and get: 

$S(0) + S(0) = S(0 + S(0))$

Now apply {eq}`PA3` inside the parentheses to get: 

$S(0 + S(0)) = S(S(0))$

But $S(S(0))$ is the definition of $2$, so we're done!

    
````


You'll have to trust me that wasn't as much a waste of time as it may have felt. While proving things directly with these axioms is rather tedious, the important thing is that we are able to do so having started with effectively nothing. The logic game is all about maximizing the bang for your axiomatic buck, and there really is quite a lot of bang with Peano arithmetic. Not only can you do any sum you like, but you can also go on to define multiplication with just two equations (one for zero, one for everything else just like before) and much more. 

(sections:numbers:induction)=
### Induction

To be able to prove slightly more interesting facts about all numbers, we do need one last axiom called *induction*. Actually, its a placeholder for infinitely many different axioms but don't worry too much about that. The idea behind induction is that if every number inherits some property from its predecessor, then every number will posess that property. Imagine there was some family curse that couldn't be cured and was eternally passed down by the sucessor function. Then every number would be cursed. Symbolically, this is written as 

```{math}
:label: PA5
\phi(0) \land (\forall x, \phi(x) \implies \phi(S(x))) \implies \forall n, \phi(n) 
```

$\phi(n)$ is a placeholder for the curse/property we're interested in. Please don't feel intimidated by the equation - ignore it if you must. Let's see induction in action with another quick theorem, $n + 0 = n$. Don't be fooled into thinking this could be immediately proven with {eq}`PA3` because doing so would assume $n + m = m + n$, which we are yet to prove (but could also be done with induction in case you want to try).

````{prf:theorem} 
:label: nplus0
$n + 0 = n$
````

````{prf:proof}
In this case $\phi(n)$ will be the statement $n + 0 = n$. To use induction, we need to prove it separately for $0$ and then for everything else. The $0$ case really is just {eq}`PA3`: $0 + 0 = 0$.

The remaining case is more interesting. We can assume that $x + 0 = x$. Now we must show $S(x) + 0 = S(x)$. By {eq}`PA4`, $S(x) + 0 = S(x+0)$. Now using our assumption $S(x + 0) = S(x)$, so we are done.

````

It may feel strange that we can get away with just assuming $x + 0 = x$ in the second part, when that looks a lot like the thing we were originally proving. But that's the beauty of induction: assume the thing you're trying to prove is indeed true for $x$ and then just show that it gets inherited by the sucessor $S(x)$. The role of $\phi(0)$ (which is often called the base case) is to kick off the chain of inheritance in the first place, but that's usually even easier to prove than inheritance. 

There's a variant of induction called *strong induction* which is basically the same except rather than assuming $\phi(n)$ to get $\phi(n+1)$, you assume $\phi(m)$ for every $m < n$ to get $\phi(n)$. They're morally the same, but strong induction is sometimes needed when your $n$ is somehow built out of many smaller things, rather than just its immediate predecessor. It turns out you can even use induction on things that aren't numbers, but we'll get to that later.

If you want to learn more about Peano Arithmetic, I recommend playing the [natural numbers game](https://adam.math.hhu.de/#/g/leanprover-community/nng4). It's where I learnt about all this and enjoyed it a lot. 

Before ending on too positive of a note, I do want to trash talk the Peano axioms a bit. From a logical point of view, its great news that we have condensed so many numbers into so few rules. But don't you feel a small nagging sense of sadness to watch the weird and wonderful world of numbers being so coldly reduced into an endless sucession of symbolic successors? Well, I certainly do. That's why I present to you my solution: a slightly more complicated set of mechanical manipulations that reduce numbers to some slightly prettier symbols. But you'll have to be patient. We're not even halfway through this rambling introduction.


## Number Bases

In the real world you'll rarely find yourself writing $SSSSSSSSSSS0 + SSSS0 = SSSSSSSSSSSSSSS0$. Instead, we use decimal notation and write $11 + 4 = 15$. Much nicer. Behind the scenes, decimal works by each digit having a position which corresponds to some power of ten. For example, 
\begin{equation*}
124 = 1 \times 10^2 + 2 \times 10^1 + 4 \times 10^0 = 100 + 20 + 4
\end{equation*}

But other than the way our hands are built, there's nothing that special about ten. Computers prefer to work in two's, so represent numbers using binary. This means that each bit (i.e. binary digit) corresponds to some power of two. For example,
\begin{equation*}
1011 = 1 \times 2^3 + 0 \times 2^2 + 1 \times 2^1 + 1 \times 2^0 = 8 + 2 + 1 = 11
\end{equation*}

To distinguish between $11$ meaning eleven in decimal and $11$ meaning three in binary, it helps to add a little subscript to distinguish $11_{10}$ from $11_2$. Of course, $10$ is the most ambiguous number of all, because in base $d$, $10_d$ is always $d$!

Anyway, what's interesting about being able to write numbers in different bases is that it helps you get used to the idea that numbers are not just symbols, but things that happen to be referenced by symbols. The fact that $11_{2}$ and $3_{10}$ refer to the same thing is a reminder that *threeness* is something that goes beyond either symbol. I will be moving around number bases and systems quite freely in this book, so I'd recommend thinking hard about your commitment to threenesses.

So what are the numbers beyond the symbols? In my opinion, the main difference between numerology and number theory hinges on that distinction: numerologists get excited about $777$ but that depends on its decimal form, number theorists get excited about primes but primeness transcends base.

This book sits somewhere between the two. Starting with the following question: can we find a new notation for numbers that enables a new perspective on them?
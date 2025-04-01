(sections:algebra)=
# Algebra


For unrelated reasons, I once came across this thing called group theory. A group is kind of like a set with some cool powers. Groups are part of abstract algebra, which basically studies the idea of plugging stuff together. Hence the abstract. The algebra part means shunting meaningless symbols around, just like the one that scarred you in highschool. 

A group is a set where the cool power gives you the ability to (a) do nothing, (b) undo everything that you can do and (c) something boring called associativity (which I call *chalkboard grease* because it just makes the symbol shunting easier). Wow so cool! But seriously, whenever you find yourself a set that can do those three things, you'd better get excited because it means that your set posseses some incredibly intricate and elegant structure.

$\mathbb{N}$ is nearly a group, but not quite. You can do nothing with it (add zero or times by one), but you can't undo (subtract or divide) because that would take you out of $\mathbb{N}$ (into $\mathbb{Z}$ or $\mathbb{Q}^+$).  But that's OK because $\mathbb{Z}$ and $\mathbb{Q}^+$ both are groups, with the powers of addition and multiplication respectively. 

Equipping a set with an operation makes it possible to view that set in many different lights.  Algebra is really fun because it teaches you to see how things are shaped by their possible interactions (if you choose to accept some abstraction).  Anyway, the upshot of all this is that a set looks extremely different depending on what powers you're studying within it. Since numbers is sets, then numbers look differently depending on whether you're adding them or multiplying them. Let's take a closer look that.

(sections:algebra:additive)=
## Additive Numbers

Given only the power of addition and a single starting number to add with, how many other numbers can you reach?

If you start with $0$, you'll get nowhere. But if you start with $1$, you can get to every other number (except $0$). Any other number will only give you a small (albeit infinite) part of the number line, e.g. $\{2,4,6,8,10,...\}$. So $1$ is very special in the world of addition.

## Multiplicative Numbers

Now what if you only have the power of multiplication?

Starting with $0$ still gets you nowhere. So does starting with $1$. Starting with $2$, you can get $2, 4, 8, 16, ...$ - the powers of $2$. Starting with $3$, you get the powers of $3$. Not only is there no single number that can get you everywhere multiplicatively, there's not even a finite set of numbers that will get you there. Instead you need the (infinite) set of *primes* $\{2, 3, 5, 7, 11, 13, ...\}$. This is precisely why the primes are so important - they are the foundation of multiplicative numbers. 

This is also why I think multiplication is so much more interesting than addition. In add-world, a number is like a single key on an infinitely long piano. But in times-land, a number is like a chord on an infinitely long, infinitely wide guitar.


I will continue to distinguish *additive* and *multiplicative* numbers throughout. At some point, I will also introduce *productive numbers* which are a new thing as well that's inspired by taking the product of prime powers. Typically, multiplying and taking the product mean the same thing, but I distinguish them here because the new numbers need a name so it as well sound cool. I don't have any fun musical metaphors for productive numbers sorry.

## Addiplicative Numbers

What if you're allowed to use addition *and* multiplication?!

The short answer is it depends. If the two numbers are multiples of each other, e.g. $2$ and $4$ then nothing much. But if the two numbers are unrelated, e.g. $2$ and $3$ and you're also allowed to subtract, then you can get to $1$ and then you're off! By the way, the smallest number you can get to is called the greatest common divisor (GCD), which may be familiar. 

Addition and multiplication work very nicely in tandem with each other because of the equation $a \times (b + c) = (a\times b) + (a \times c)$. This is called *distributivity* and you've probably used it your whole life without noticing. Distributivity is nice because it means you can gradually break down complex expressions into simpler ones. It also shows up elsewhere: 
* Sets: $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$ 
* Logic: the statements "the cat is red and (either on the mat or outdoors)" has the same meaning as "either (the cat is red and on the mat) or (the cat is red and outdoors)"


The differences between addition and multiplication go far beyond numbers. You can add or multiply sets, groups, vector spaces and whatever. This isn't a multiplication in the sense of repeated addition, but in the sense of inheriting the abstract properties/vibes of the operations. Typically, abstract addition puts things alongside each other whereas multiplication interweaves them. Interesting things tend to happen when things are combined, so multiplication is almost always the more interesting operation.


That's all the time we have for algebra unfortunately. Main takeaway: numbers are different in add-world and times-land. Add-world is boring. Times-land is cool.
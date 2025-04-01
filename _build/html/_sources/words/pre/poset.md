(sections:pre:order)=
# Orders

People just seem to love putting things in order.

```{figure} ../../imgs/bercow.gif
---
align: center
---
[source](https://giphy.com/gifs/euronews-order-commons-john-bercow-l2AYpTe5FOOMkBZ3I3)
```

Sometimes this can get a bit ridiculous: there's a whole [corner of the internet](https://tiermaker.com/) dedicated to ranking things that realistically cannot be ranked. On the other side, [some people](https://culanth.org/fieldsights/comparison-the-impossible-method) are averse to any form of comparison altogether.

These tensions are reconciled in what mathematicians call a *partial order*. A partial order is one of my favourite math gizmos because it has affected the way I understand not only the mathematical world, but also the real world. The idea behind partial orders can basically be summed up with the slogan:
> Not everything is better or worse. Some things are just different.

Here's an informal example. Suppose you want to buy a smoothie. You want it to be healthy, tasty and cheap. Some smoothies are genuinely better than others: a banana smoothie is healthier, tastier and cheaper than a chocolate and truffle smoothie which is itself slightly tastier but otherwise the same as a chocolate and balsamic vinegar smoothie. On the other hand, a superfood smoothie is tastier and healthier than a banana smoothie, but more expensive. So neither is wholly better than the other, which we will call *incomparable*. We can draw these relationships in what's called a *Hasse Diagram*:
```{image} ../../tikz/smoothie.svg
        :alt: smoothie order
        :height: 200px
        :align: center
```

Remember: Hasse diagrams always go up.

If you disagree about any of the placements, just draw your own version. Hopefully this gives you a sense of how to order things that may be incomparable. Don't worry if this is boringly obvious, partial orders are pretty easy to understand themselves. So let's jump into the details!

## Definition

The formal definition is as follows. Some relation $x \leq y$ is a **partial order** if:
```{math}
:label: refl
    x \leq x \hspace{1cm} \text{(Reflexivity)}
```
```{math}
:label: trans
    x \leq y \land y \leq z \implies x \leq z \hspace{1cm} \text{(Transitivity)}
```
```{math}
:label: asymm
    x \leq y \land y \leq x \implies x = y \hspace{1cm} \text{(Anti-symmetry)}
```

Let's break that definition down:
- Reflexivity just means everything is less than or equal to itself. Not very problematic. Math definitions almost always start with some trivial requirement like this.
- Transitivity is very important. It means you can chain together multiple comparisons into a new one. It also enforces the idea that you are comparing things consistently. For example, the relation of being a synonym is not transitive: 'tangerine' is synonymous with 'orange' and 'orange' is synomyous with 'yellowy-red', but 'tangerine' and 'yellowy-red' are not at all synonymous. The problem is that 'orange' is both a noun and an adjective, and we allowed the meaning of orange to change between comparisons. Similarly, the "is beaten by" relation is not transitive in rock-paper-scissors, but is in poker.
- Anti-symmetry is subtle. I initially wrote it off as chalkboard grease to help prove equality. But I've learned to think of it as enforcing the beautiful idea that x's relationships with everything else determine what x is. For example, the smoothie order I introduced above is not anti-symmetric because two smoothies that have the same taste, cost and healthiness could still be different smoothies. On the other hand, you should be able to guess what number I'm thinking of if I tell you it's both at least as big and at least as small as $2$.

## Examples

By the way, a partially ordered set is often abbreviated as a poset, which is quite a cute name. Let's look at some examples of posets in more detail.


### Additive Numbers

Additive numbers is indeed a poset. You probably think of $x \leq y$ as meaning $x$ comes before $y$ in the number line. But the technical definition is:

```{math}
:label: nleq
    x \leq y \iff \text{ there exists some } z\in \mathbb{N} \text{ such that } x + z = y
```

Here's the Hasse diagram (which in this case is just the number line but rotated).
```{image} ../../tikz/line.svg
        :alt: number line
        :height: 200px
        :align: center
```

I'll call the $z$ in equation {eq}`nleq` the *witness* of $x \leq y$. Remeber that we're talking about $\mathbb{N}$ so all numbers are positive (or $0$). This relation is indeed reflexive: just pick $0$ for the witness and check that $x + 0 = x$ (it does). Proof of other properties in box below.


````{dropdown} Click me for proof of transitivity and anti-symmetry



```{prf:proof} (Proof of transitivity)

Suppose that $x \leq y$. Then there's some $w_1$ such that $x + w_1 = y$. Similarly, assuming $y \leq z$ means there's some $w_2$ such that $y + w_2 = z$. 

Putting these together gives $(x + w_1) + w_2 = z$, which we can rearrange to $x + (w_1 + w_2) = z$, so $w_1 + w_2$ is the witness of $x \leq z$. Done.

```

```{prf:proof} (Proof of anti-symmetry)

Let $w_1$ be the witness for $x \leq y$ and $w_2$ the witness for $y \leq x$. So we have $x + w_1 = y$ and $y + w_2 = x$. 

Plugging the first equation into the second gives $(x + w_1) + w_2 = x$. Taking $x$ away from both sides gives $w_1 + w_2 = 0$. Since $w_1, w_2$ cannot be negative, $w_1 = w_2 = 0$. Therefore $x = y$. Done.

```

````

The order of numbers satisfies one additional property which is solely responsible for making it so boring:
```{math}
:label: total
    x \leq y \lor y \leq x \hspace{1cm} \text{(Totality)}
```
The proof is also boring and uses induction, so I won't bother.

In other words, an order is *total* when everything is comparable. Though technically partial orders include total orders (i.e. *partial* $\leq$ *total* in the order of orders), calling something a partial order usually means it is not total. So let's look at an example of a genuinely partial order.


### Multiplicative Numbers

We can define a very similar relation to {eq}`nleq`, but with multiplication. To avoid confusing notation, this is usually written $x | y$ and read as $x$ *divides* $y$.
```{math}
:label: div
x | y \iff \text{there exists some } z \in \mathbb{N}^+ \text{such that } x \times z = y
```

As before, I'll call $z$ the *witness* of the divisibility of $y$ by $x$. The reason $z$ comes from $\mathbb{N}^+$ rather than $\mathbb{N}$ is because $0$ behaves horribly in times land, so is excluded altogether. 

It's not hard to see that $x | x$ (choose $1$ as witness and check $x \times 1 = x$). Proof of other properties below:


````{dropdown} Click me for proof of transitivity and anti-symmetry

These are extremely similar to the additive proofs. Like I literally copied, pasted and replaced $+$ with $\times$ and a couple of other symbols. Skip unless you really care.


```{prf:proof} (Proof of transitivity)

Suppose that $x | y$. Then there's some $w_1$ such that $x \times w_1 = y$. Similarly, assuming $y | z$ means there's some $w_2$ such that $y \times w_2 = z$. 

Putting these together gives $(x \times w_1) \times w_2 = z$, which we can rearrange to $x \times (w_1 \times w_2) = z$, so $w_1 \times w_2$ is the witness of $x | z$. Done.

```

```{prf:proof} (Proof of anti-symmetry)

Let $w_1$ be the witness for $x | y$ and $w_2$ the witness for $y | x$. So we have $x \times w_1 = y$ and $y \times w_2 = x$. 

Plugging the first equation into the second gives $(x \times w_1) \times w_2 = x$. Dividing by $x$ on both sides gives $w_1 \times w_2 = 1$. Since $w_1, w_2$ are both positive whole numbers, $w_1 = w_2 = 1$. Therefore $x = y$. Done.

```

````



Very crucially, divisibility is not total. For example, $2$ can't divide $3$ and $3$ can't divide $2$. They are just different. This manifests in a far more intricate Hasse diagram than we've seen so far. As a reminder, a line going up from $x$ to $y$ now means $x | y$. 

```{image} ../../tikz/div.svg
        :alt: divisibility lattice
        :height: 300px
        :align: center
        :name: divlatt
```

Unsurprisingly, the primes play a foundational role.

### Subsets

The most interesting and most important example of a partial order is the subset relation $A \subseteq B$ (i.e. $B$ contains all the elements of $A$) that we met back [here](sections:sets:ops). 

As a refresher, notice that $\{a\} \subseteq \{a, b\} \subseteq \{a, b, c\}$.

The conditions are quite easy to check:
- Reflexive: clearly $A \subseteq A$.
- Transitive: if $A \subseteq B$ then $B$ contains all the elements of $A$. If $B \subseteq C$, then $C$ contains all the elements of $B$. So $C$ contains all the elements of $A$ which means $A \subseteq C$.
- Anti-symmetric: if $A \subseteq B$ and $B \subseteq A$, then they each contain all the same elements. By definition, sets that contain the same elements are the same, so $A = B$.

Crucially, $\subseteq$ is not total. For example, the sets $\{a, b, c\}$ and $\{a,c,d\}$ are incomparable.

We are not allowed to talk about the set of all sets, so we cannot define the poset of all sets. However, given a starting set we can look at the poset of all its subsets. Here it is for the set $\{a, b, c\}$, (where a line now means a set is contained in the one above):
```{image} ../../tikz/subset.svg
        :alt: subset lattice
        :height: 250px
        :align: center
        :name: sublatt
```
(yes - the empty set is technically a subset of everything)

```{dropdown} What exactly is a Hasse diagram?
You can draw any (finite) partial order as a Hasse diagram. An vertical line from $x$ to $y$ means $x \leq y$. However, many of the relations are not drawn implicitly so really $x \leq y$ means there is a vertical *path* from $x$ to $y$ in the diagram. How does this match with the definition of a poset?

1. *Reflexivity*: just assume that every element has a path to itself. Drawing circular lines from everything to itself would add clutter, so they're implicit.
2. *Transitivity*: if there's a path from $x$ to $y$ and another path from $y$ to $z$, then just imagine traversing each path separately and you have a path from $x$ to $z$. This isn't drawn explicitly because it would also add clutter.
3. *Anti-symmetry*: this is the reason all lines go up. Without anti-symmetry, you would have to use directed arrows, rather than lines and they could go sideways or even downwards. But with anti-symmetry you know that if something is greater than $x$, then it cannot also be less than $x$ (unless it actually is $x$) and so you can put it above $x$. 

```

### Fun examples

Here are some other examples that can be helpful to think about:
1. **Time** In special relativity, observers can see the same events happening in a different order (e.g. A happens before B for one person, but A happens after B for another person). This forms a partial order - see [here](https://physics.stackexchange.com/questions/227049/is-causality-a-total-order) for more info.
2. **Getting Dressed** A similar, but much simpler, time-based example is how to get dressed. You have to put your T-shirt on before your sweater before your coat, but you could put your socks on before or after any of these. I got this from [here](https://courses.grainger.illinois.edu/cs173/fa2008/lectures/lect_34.pdf), where you can see a few more examples.
3. **Family Trees** People are (transitively) descended from other people. But when we draw family trees, they are not total because people of the same generation or not descended from each other. So its a partial order. In fact, anything that can be drawn as a tree is a partial order.
4. **Privilege** In our society, some groups of people are more privileged than others. Intersectionality is the idea that combining privileges makes things more complicated. [This talk](https://youtu.be/48VqWQ2YbGk?si=9IP_4SZn7q3yxupP&t=2213) explores how partial orders can help clarify some of these complications. 

(sections:pre:lattice)=
# Lattices

I won't say too much about lattices because I still don't fully understand them. The basic idea is you have a poset with some extra structure. The extra structure includes, at the very least, two operations $\land$ and $\lor$. These operations come in handy for finding shared properties of incomparable objects. 

$x \land y$ is the *greatest* element $z$ such that $z \leq x$ and $z \leq y$. This is often called the *greatest lower bound*. In the tree of life, $x \land y$ is like the last common ancestor of $x$ and $y$. 

There are two distinct parts to this definition: firstly that there is at least one element that is less than both $x$ and $y$ and secondly that out of all the ancestors of $x$ and $y$ we can uniquely pick out the one that is closest to $x$ and $y$ (according to $\leq$). The second part is why we can talk of *the* greatest lower bound.

Dually, $x \lor y$ gives the *least* element such that $x \leq z$ and $y \leq z$. This is often called the *least upper bound*. In a world where evolution somehow ultimately merges all species, $x \lor y$ would be the first common *descendent* of $x$ and $y$. The fact that our tree of life lacks this feature is a useful reminder that not every poset is a lattice.


A diagram may help:
```{image} ../../tikz/diamond.svg
        :alt: diamond lattice
        :height: 200px
        :align: center
```

In perhaps the worst clash of notations I've ever seen, $x \land y$ is found at the bottom of the v-shape between $x$ and $y$, while $x \lor y$ is found at the top of the hat *above* $x$ and $y$. Really sorry about that.

The operations do have names: $\land$ is called the *meet* and $\lor$ is called the *join*. But I always get these names mixed up so won't use them that much. 

There's another way of defining lattices that I have no intution for but you can read about on [wikipedia](https://en.wikipedia.org/wiki/Lattice_(order)#As_algebraic_structure) if you want. 

I'll end with some examples of lattices:
- The *Boolean* lattice is just the total order $0 \leq 1$ (interepreted as False and True), where $x \land y$ equals the truth value of $x$ AND $y$, $x \lor y$ the truth value of $x$ OR $y$. Even though this is an extremely boring lattice, it seems to play a very important role and is actually where the $\land,\lor$ symbols come from.   
- The divisibility partial order from above is a lattice. $x \land y$ is defined as the greatest common divisor of $x$ and $y$ and $x \lor y$ is the least common multiple. Not too suprising - if $z$ is a common divisor of $x$ and $y$, then $z | x$ and $z | y$ and it is greatest by definition.
- The subset partial order from above is also a lattice! $\land$ is the intersection $A \cap B$, $\lor$ is the union $A \cup B$. That $A \cap B$ is contained in both $A$ and $B$ is fairly obvious. That it is the greatest such subset is because if it were any bigger, it would contain elements that either weren't in $A$ or weren't in $B$. 


The last two examples are extremely important to keep in mind because in the next chapter because we'll see that productive numbers form a lattice which sort of sits halfway between the divisibility lattice and the subset lattice. In short, $\sqsubseteq \ \cong \ | \ \land \subseteq $[^latref]. 


[^latref]: This is kind of a joke but also not really. There are order-preserving maps (which alas aren't lattice homomorphisms) from productive numbers to both the divisibility order and the subset order. So it's halfway there to being the product in the category of posets, just without the universal property.


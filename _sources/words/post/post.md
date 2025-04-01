(sections:post:summary)=
# Summary

In case you couldn't be bothered to read the whole thing, here's a concise summary.

## Definitions

The set of prods $\mathbb{\Pi}$ is defined as:
1. $0 \in \mathbb{\Pi}$
2. $x_1, ..., x_n \in \mathbb{\Pi} \implies [x_1, ..., x_n] \in \mathbb{\Pi}$
3. $[x_1, ..., x_n, 0] = [x_1, ..., x_n]$

By convention $[]:= [0] = [0, 0, ...]$ and prods are automatically padded to the same length for comparisons.

You can interpret any prod as a natural number by:

\begin{align*}
I(0) &= 0 \\
I([x_1, ..., x_n]) &= \prod_{i=1}^n p_i^{I(x_i)} \text{ , where } p_i \text{ is the ith prime}
\end{align*}

Trees are [useful](sections:prod:examples) for visualizing prods.




The operation $\sqcup: \mathbb{\Pi} \times \mathbb{\Pi} \to \mathbb{\Pi}$, called graft, is defined as:
\begin{align*}
0 \sqcup x &= x = x \sqcup 0 \\
[x_1, ..., x_n] \sqcup [y_1, ..., y_n] &= [x_1 \sqcup y_1, ..., x_n \sqcup y_n]
\end{align*}

The dual operation $\sqcap: \mathbb{\Pi} \times \mathbb{\Pi} \to \mathbb{\Pi}$, called prune, is defined similarly as:
\begin{align*}
0 \sqcap x &= 0 = x \sqcap 0 \\
[x_1, ..., x_n] \sqcap [y_1, ..., y_n] &= [x_1 \sqcap y_1, ..., x_n \sqcap y_n]
\end{align*}

## Results

1. $I: \mathbb{\Pi} \to \mathbb{N}$ is an isomorphism ({prf:ref}`ftpa`).
2. $\sqcap$ induces a partial order equivalent to $x \sqsubseteq y \iff x = 0 \lor (x_1 \sqsubseteq y_1 \land ... \land x_n \sqsubseteq y_n)$ ([this section](sections:lattice:poset))
3. $x \sqsubseteq y \implies I(x) | I(y)$, but not vice-versa ({prf:ref}`leqdiv`)
4. $\mathbb{\Pi}, \sqcup, \sqcap$ form a distributive lattice ([this section](sections:lattice:lattice)).
5. For any $x \in \mathbb{\Pi}$, the downset $\downarrow x := \{y | y \sqsubseteq x\}$ is a Heyting algebra ({prf:ref}`sublatt`).
6. $\downarrow x - \{0\}$ is a Boolean algebra iff $x$'s only components are $0, []$ ({prf:ref}`shallowbool`). The condition is analogous to square-free integers. 
   
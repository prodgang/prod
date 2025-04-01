---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

(sections:draw)=
# Draw

Draw your favourite productive number! Navigate to {fa}`rocket` --> {guilabel}`Live Code`, wait until it says ready and then drag the slider around.



```{code-cell} ipython3
:tags: [thebe-init, hide-input, hide-output]
!pip install networkx matplotlib sympy 
! pip install ipywidgets==7.5.1 ipython_genutils
```

```{code-cell} ipython3
:tags: [thebe-init, hide-input]

import matplotlib.pyplot as plt
import networkx as nx
import ipywidgets as widgets
import matplotlib.pyplot as plt
from IPython.display import display, clear_output
import sympy
from sympy.ntheory import factorint
primes = list(sympy.primerange(1, 100))

def draw_white_dot(G, pos, ax=None):
    node_label = len(G.nodes) + 1
    G.add_node(0, pos=(pos[0], pos[1]))
    nx.draw_networkx_nodes(G, {0:pos}, nodelist=[0], node_color='white', node_size=500, edgecolors='black', ax=ax)
    return node_label

def draw_black_dot(G, pos, ax=None):
    node_label = len(G.nodes) + 1
    G.add_node(node_label, pos=(pos[0], pos[1]))
    nx.draw_networkx_nodes(G, {node_label:pos}, nodelist=[node_label], node_color='black', node_size=500, ax=ax)
    return node_label

def draw_tree(G, tree, pos=None, root_pos=(0, 0), ax=None):
    if pos is None:
        pos = {}
    
    if tree == 0:
        label = draw_white_dot(G, root_pos, ax=ax)
        pos[label] = root_pos
        return label

    n = len(tree)
    root_pos = (root_pos[0] + n/2, root_pos[1])
    root_label = draw_black_dot(G, root_pos,ax=ax)
    pos[root_label] = root_pos
    
    for i, child in enumerate(tree):
        j = (i - (n - 1) / 2) * 2
        child_label = draw_tree(G, child, pos=pos, root_pos=(root_pos[0] + j, root_pos[1]-1), ax=ax)
        nx.draw_networkx_edges(G, pos, edgelist=[(root_label, child_label)],ax=ax)


    return root_label

def p_to_d(ps):
    assert type(ps) == tuple or ps == 0, ("bad input", ps)
    if ps == 0: return 0
    
    x = 1
    for i, p in enumerate(ps):
        x *= primes[i]**p_to_d(p)
    
    return x

def d_to_p(x):
    if x == 0: return 0
    if x == 1: return () # use tuples because can be hashed

    assert x < 2**420, "something tells me this number isnt gonna be worth trying to factor..."
    
    factors = factorint(x)
    
    max_prime = max(factors.keys())
    assert max_prime in primes, "need more primes! Fix me please"
    mp_index = primes.index(max_prime)
    y = [0] * (mp_index + 1)
    
    # key recursive step
    for p, e in factors.items():
        i = primes.index(p)
        y[i] = d_to_p(e)
    
    return tuple(y)

def d2tree(x, ax=None):
    G = nx.Graph()
    draw_tree(G, d_to_p(x), ax=ax)

def update_plot(n):
    #print("updated to ", n)
    
    clear_output(wait=True)

    fig, ax = plt.subplots(figsize=(5, 5))
    d2tree(n, ax=ax)
    plt.show()

```

```{code-cell} ipython3
:tags: [thebe-init]

slider = widgets.IntSlider(value=1, min=1, max=70, step=1, description="n:")
display(widgets.interactive(update_plot, n=slider))

```


This block lets you enter any number:
```{code-cell} ipython3
:tags: [thebe-init, hide-input]

# Edit this line to choose any number you want
n = 24

d2tree(n)
```

(sections:draw:ops)=
## Operations

```{code-cell} ipython3
:tags: [thebe-init, hide-input]

def pad(a, b, pure=True):
    if a == 0 or b == 0:
        return a, b
    
    a = list(a).copy()
    b = list(b).copy()

    # pad 0s
    while len(a) < len(b):
        a += [0]
    while len(b) < len(a):
        b += [0]
    assert len(a) == len(b)
    
    return tuple(a), tuple(b)


def trim(x, pure=True):
    if x == 0:
        return 0
    if pure: x = list(x).copy()
    if x == () or all(x[i] == 0 for i in range(len(x))):
        return ()
    while len(x)> 0 and x[-1] == 0:
        x = x[:-1]
    x = [trim(x[i]) for i in range(len(x))]
    return tuple(x)


def graft(a, b):
    if a == 0:
        return b
    if b == 0:
        return a

    a, b = pad(a, b)
    return tuple([graft(a[i], b[i]) for i in range(len(a))])

def prune(a, b):
    if a == 0 or b == 0:
        return 0
    
    a, b = pad(a, b)
    return tuple([prune(a[i], b[i]) for i in range(len(a))])

def draw_graft(x, y):
    fig, axs=plt.subplots(1,3, figsize=(12, 4))


    px = d_to_p(x)
    py = d_to_p(y)

    print("x =", x)
    draw_tree(nx.Graph(), px, ax=axs[0])

    print("y =", y)
    draw_tree(nx.Graph(), py, ax=axs[1])


    gxy = graft(px, py)
    print("x graft y =", p_to_d(gxy))
    draw_tree(nx.Graph(), gxy, ax=axs[2])

def draw_prune(x, y):
    fig, axs=plt.subplots(1,3, figsize=(12, 4))

    px = d_to_p(x)
    py = d_to_p(y)

    print("x =", x)
    draw_tree(nx.Graph(), px, ax=axs[0])

    print("y =", y)
    draw_tree(nx.Graph(), py, ax=axs[1])

    pxy = trim(prune(px, py))
    print("x prune y =", p_to_d(pxy))
    draw_tree(nx.Graph(), pxy)
```

Use this block to test your grafting:

```{code-cell} ipython3
:tags: [thebe-init]

# INSERT NUMBERS HERE
x, y = 2,3

draw_graft(x, y)
```

Use this block to test your pruning:

```{code-cell} ipython3
:tags: [thebe-init]

# INSERT NUMBERS HERE
x, y = 2,3

draw_prune(x, y)
```
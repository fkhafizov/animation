2026.01.14

# Schreier/coset graph definition and examples

* https://claude.ai/chat/f2f38a9b-5e5d-4020-9897-a1d3289a439c

# Schreier Graphs (Coset Graphs)

## Definition

A **Schreier graph** (or coset graph) is a visual representation of how a group $G$ acts on the cosets of a subgroup $H$ via a generating set $S$.

### Formal Definition

Given:
- A group $G$ with generating set $S = \{s_1, s_2, \ldots, s_k\}$
- A subgroup $H \leq G$

The **Schreier graph** $\Gamma(G, H, S)$ is constructed as follows:

- **Vertices**: The left cosets $\{gH : g \in G\}$
- **Edges**: For each coset $gH$ and generator $s \in S$, draw a directed edge labeled $s$ from $gH$ to $sgH$

## Intuitive Analogy

Think of a Schreier graph like a **metro/subway map**:
- Each **station** (vertex) represents a "position" in the group (a coset)
- Each **train line** (edge color) represents a generator - a specific "move" you can make
- The **network structure** shows all possible journeys by repeatedly taking trains
- The subgroup $H$ determines your "equivalence" - which positions you consider "the same station"

## Key Properties

1. The graph is **regular** if $S$ is symmetric ($s \in S \Rightarrow s^{-1} \in S$)
2. The graph is **connected** if and only if $G = \langle S, H \rangle$
3. The number of vertices equals the index $[G:H]$
4. Closed paths starting at $H$ correspond to elements of $H$

## Examples

### Example 1: $\mathbb{Z}_6$ acting on itself

Let $G = \mathbb{Z}_6 = \{0, 1, 2, 3, 4, 5\}$ with generator $S = \{1\}$ and $H = \{0\}$ (trivial subgroup).

The Schreier graph is simply a **cycle of 6 vertices**:

```
0 --1--> 1 --1--> 2 --1--> 3 --1--> 4 --1--> 5 --1--> 0
```

### Example 2: $\mathbb{Z}$ acting on cosets of $3\mathbb{Z}$

Let $G = \mathbb{Z}$, $S = \{1, -1\}$, and $H = 3\mathbb{Z}$.

The three cosets are: $H$, $1+H$, $2+H$

This gives a **bi-infinite path with period 3**:

```
... <--1-- H --1--> 1+H --1--> 2+H --1--> H --1--> ...
```

### Example 3: Cayley Graph vs Schreier Graph

For $G = S_3$ (symmetric group), $S = \{(12), (123)\}$:

- **Cayley graph** (when $H = \{e\}$): Shows all 6 elements of $S_3$
- **Schreier graph** (when $H = \langle (12) \rangle$): Shows only 3 cosets: $H$, $(123)H$, $(132)H$

Let me create a visualization to illustrate these concepts:## Visual Examples Explained

The visualization shows four different Schreier graphs:

### 1. **Simple Cycle** ($\mathbb{Z}_6$)
When $H$ is trivial (just the identity), you get the full Cayley graph. Here, repeatedly applying generator $+1$ cycles through all elements.

### 2. **Quotient Structure** ($\mathbb{Z}/3\mathbb{Z}$)
The infinite group $\mathbb{Z}$ acting on three cosets of $3\mathbb{Z}$. The blue edges (generator $+1$) move forward, red edges (generator $-1$) move backward. This creates a periodic structure that "wraps around."

### 3. **Bidirectional Cayley Graph** ($\mathbb{Z}_4$)
With generators $\{1, -1\}$, you can move both clockwise and counterclockwise. Each pair of opposite arrows shows that these generators are inverses.

### 4. **Non-Cyclic Structure** (Klein 4-group)
The Klein 4-group $V_4$ has two independent generators of order 2. The graph forms a square, showing that all elements are one or two "steps" from the identity.

## Connection to Random Walks

Schreier graphs are fundamental in studying **random walks on groups**: 
- Each edge represents a possible "step" 
- Uniform random walk on the graph corresponds to multiplying by random generators
- Graph connectivity reveals group structure

## Why This Matters

Schreier graphs appear in:
- **Automata theory**: Recognizing languages with group symmetries
- **Covering spaces**: Fundamental groups acting on universal covers  
- **Cryptography**: Cayley hash functions
- **Geometric group theory**: Visualizing infinite groups

The key insight: **Group structure becomes geometric structure** — abstract algebra becomes visual topology!

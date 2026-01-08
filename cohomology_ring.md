2026.01.08

In English, **когомологии грассманиана $G(2,5)$** is:

* **the cohomology of the Grassmannian $G(2,5)$**
  or more explicitly,
* **the cohomology ring of the Grassmannian $G(2,5)$.**

Also common is the notation

* **$\mathrm{Gr}(2,5)$** instead of $G(2,5)$, read as **the Grassmannian of 2-planes in $\mathbb C^5$.**


# Q

Claude.ai please 
explain to me the cohomology ring of the Grassmannian $G(2,5)$ with examples and use an analogy

# A

# The Cohomology Ring of $G(2,5)$

## The Analogy: A Library Card Catalog System

Imagine a **library with 5 shelves**, and you're interested in cataloging all possible ways to choose **2 adjacent shelves** to form a "reading nook." The cohomology ring is like a sophisticated accounting system that tracks:

1. **What configurations exist** (the Schubert classes)
2. **How configurations combine** when you impose multiple constraints (the ring multiplication)

Just as a librarian might ask "How many reading nooks satisfy *both* constraint A *and* constraint B?", the cohomology ring answers: "When I intersect geometric condition A with condition B, what do I get?"

---

## What is $G(2,5)$?

The Grassmannian $G(2,5)$ is the space of all **2-dimensional planes through the origin** in $\mathbb{C}^5$ (or $\mathbb{R}^5$). 

- **Dimension**: $\dim G(2,5) = 2 \times (5-2) = 6$
- **Points**: Each point represents a choice of a 2-plane in 5-space

---

## The Schubert Classes: Building Blocks

The cohomology ring $H^*(G(2,5), \mathbb{Z})$ has a basis of **Schubert classes** $\sigma_\lambda$, indexed by **partitions** $\lambda = (\lambda_1, \lambda_2)$ fitting inside a $2 \times 3$ rectangle:

$$3 \geq \lambda_1 \geq \lambda_2 \geq 0$$

| Partition $\lambda$ | Codimension | Geometric Meaning |
|:---:|:---:|:---|
| $\emptyset$ | 0 | All 2-planes (the whole space) |
| $(1)$ | 1 | 2-planes meeting a fixed 3-plane |
| $(2)$ | 2 | 2-planes meeting a fixed 2-plane |
| $(1,1)$ | 2 | 2-planes contained in a fixed 4-plane |
| $(3)$ | 3 | 2-planes containing a fixed line |
| $(2,1)$ | 3 | 2-planes meeting a fixed line AND inside a 4-plane |
| $(3,1)$ | 4 | 2-planes containing a line AND inside a 4-plane |
| $(2,2)$ | 4 | 2-planes inside a fixed 3-plane |
| $(3,2)$ | 5 | 2-planes containing a line AND inside a 3-plane |
| $(3,3)$ | 6 | A single fixed 2-plane (a point in $G(2,5)$) |

There are exactly $\binom{5}{2} = 10$ Schubert classes.

---

## The Ring Structure

The cohomology ring is:

$$H^*(G(2,5), \mathbb{Z}) \cong \frac{\mathbb{Z}[\sigma_1, \sigma_{1,1}]}{(\text{relations})}$$

where $\sigma_1$ and $\sigma_{1,1}$ are the **generators** (think of them as the fundamental geometric constraints).

### Pieri's Formula (The Multiplication Rule)

Multiplying by $\sigma_1$ follows Pieri's rule—add one box to the Young diagram in all valid ways:

$$\sigma_1 \cdot \sigma_\lambda = \sum_{\mu} \sigma_\mu$$

where $\mu$ is obtained by adding one box to $\lambda$, no two boxes in the same column.

---

## Concrete Examples

### Example 1: $\sigma_1 \cdot \sigma_1$

Starting from partition $(1)$, add one box:
- Add to row 1: $(2)$
- Add to row 2: $(1,1)$

$$\boxed{\sigma_1 \cdot \sigma_1 = \sigma_2 + \sigma_{1,1}}$$

**Geometric meaning**: "2-planes meeting fixed 3-plane $A$" ∩ "2-planes meeting fixed 3-plane $B$" = "2-planes meeting a fixed 2-plane" + "2-planes inside a fixed 4-plane"

### Example 2: $\sigma_1 \cdot \sigma_2$

From $(2)$, add one box:
- Add to row 1: $(3)$
- Add to row 2: $(2,1)$

$$\boxed{\sigma_1 \cdot \sigma_2 = \sigma_3 + \sigma_{2,1}}$$

### Example 3: $\sigma_2 \cdot \sigma_2$ (Enumerative Geometry!)

This requires the **Littlewood-Richardson rule**:

$$\boxed{\sigma_2 \cdot \sigma_2 = \sigma_{3,1}}$$

**Geometric meaning**: How many 2-planes in $\mathbb{C}^5$ meet *four* generic 2-planes? The answer is the coefficient when we expand to the top class:

$$\sigma_2^2 = \sigma_{3,1}$$

To get a number, we need codimension 6 (a point). Since $\sigma_{3,1}$ has codimension 4, we need more:

$$\sigma_2 \cdot \sigma_2 \cdot \sigma_{1,1} = \sigma_{3,1} \cdot \sigma_{1,1} = \sigma_{3,3}$$

So: **1 two-plane** meets 4 generic 2-planes and lies in a generic 4-plane.

### Example 4: The Degree of $G(2,5)$ (Plücker Embedding)

$$\sigma_1^6 = 5 \cdot \sigma_{3,3}$$

This means the **degree** of $G(2,5)$ in its Plücker embedding in $\mathbb{P}^9$ is **5**.

---

## The Complete Multiplication Table (Low Degrees)

| $\cdot$ | $\sigma_1$ | $\sigma_{1,1}$ |
|:---:|:---:|:---:|
| $\sigma_1$ | $\sigma_2 + \sigma_{1,1}$ | $\sigma_{2,1}$ |
| $\sigma_2$ | $\sigma_3 + \sigma_{2,1}$ | $\sigma_{2,2}$ |
| $\sigma_{1,1}$ | $\sigma_{2,1}$ | $\sigma_{2,2}$ |

---

## Returning to the Analogy

Think of each Schubert class as a **filter** in our library catalog:
- $\sigma_1$: "Books accessible from the ground floor" 
- $\sigma_{1,1}$: "Books in the fiction section"
- Multiplication $\sigma_1 \cdot \sigma_{1,1}$: "Books that are *both* accessible from ground floor *and* in fiction"

The ring structure tells us that combining filters doesn't just give one answer—it can decompose into a sum of simpler conditions, weighted by **how many ways** they can occur.

---

## Summary

| Aspect | Description |
|:---|:---|
| **Space** | $G(2,5)$ = all 2-planes in $\mathbb{C}^5$ |
| **Dimension** | 6 |
| **Generators** | $\sigma_1$ (codim 1), $\sigma_{1,1}$ (codim 2) |
| **Basis** | 10 Schubert classes (partitions in $2 \times 3$ box) |
| **Key tool** | Pieri's formula for multiplication |
| **Application** | Enumerative geometry (counting linear subspaces) |

Would you like me to create a visualization of the Young diagrams and the multiplication structure, or work through more enumerative examples like "How many lines meet 4 general lines in $\mathbb{P}^4$?"

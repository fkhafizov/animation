2026.01.04

# Building the Inversion Vector $\text{Inv}(P_1 \to e)$






The inversion vector $\text{Inv}(P_1 \to e)$ encodes the **bubble sort trace** — it records every swap (1) or no-swap (0) as you transform permutation $P_1$ into the identity $e = [0, 1, 2, 3]$.

## The Analogy
* Think of it like a **flight recorder for bubble sort**.
* Each bit in the vector is a yes/no answer to: "Did we swap at this comparison?"

## The Structure

For $n = 4$ elements, bubble sort performs **3 passes**, each with **3 adjacent comparisons**:

$$\underbrace{(0,1), (1,2), (2,3)}_{\text{Pass 1}}, \underbrace{(0,1), (1,2), (2,3)}_{\text{Pass 2}}, \underbrace{(0,1), (1,2), (2,3)}_{\text{Pass 3}}$$

This gives us $3 \times 3 = 9$ comparison slots — exactly the length of your vector.


**Starting Permutation:** $P_1 = [3, 1, 2, 0]$

**Target (Identity):** $e = [0, 1, 2, 3]$

**Method:** Record each swap (1) or no-swap (0) during bubble sort

> Elements being compared are shown in $\textcolor{red}{\text{red}}$

---

## Pass 1

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | $[\textcolor{red}{3}, \textcolor{red}{1}, 2, 0]$ | 3 > 1 → **Yes** | $[\textcolor{red}{1}, \textcolor{red}{3}, 2, 0]$ | **1** |
| (1,2) | $[1, \textcolor{red}{3}, \textcolor{red}{2}, 0]$ | 3 > 2 → **Yes** | $[1, \textcolor{red}{2}, \textcolor{red}{3}, 0]$ | **1** |
| (2,3) | $[1, 2, \textcolor{red}{3}, \textcolor{red}{0}]$ | 3 > 0 → **Yes** | $[1, 2, \textcolor{red}{0}, \textcolor{red}{3}]$ | **1** |

**Pass 1 bits:** $[1, 1, 1]$

---

## Pass 2

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | $[\textcolor{red}{1}, \textcolor{red}{2}, 0, 3]$ | 1 < 2 → No | $[\textcolor{red}{1}, \textcolor{red}{2}, 0, 3]$ | 0 |
| (1,2) | $[1, \textcolor{red}{2}, \textcolor{red}{0}, 3]$ | 2 > 0 → **Yes** | $[1, \textcolor{red}{0}, \textcolor{red}{2}, 3]$ | **1** |
| (2,3) | $[1, 0, \textcolor{red}{2}, \textcolor{red}{3}]$ | 2 < 3 → No | $[1, 0, \textcolor{red}{2}, \textcolor{red}{3}]$ | 0 |

**Pass 2 bits:** $[0, 1, 0]$

---

## Pass 3

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | $[\textcolor{red}{1}, \textcolor{red}{0}, 2, 3]$ | 1 > 0 → **Yes** | $[\textcolor{red}{0}, \textcolor{red}{1}, 2, 3]$ | **1** |
| (1,2) | $[0, \textcolor{red}{1}, \textcolor{red}{2}, 3]$ | 1 < 2 → No | $[0, \textcolor{red}{1}, \textcolor{red}{2}, 3]$ | 0 |
| (2,3) | $[0, 1, \textcolor{red}{2}, \textcolor{red}{3}]$ | 2 < 3 → No | $[0, 1, \textcolor{red}{2}, \textcolor{red}{3}]$ | 0 |

**Pass 3 bits:** $[1, 0, 0]$

---

## Final Result

$$\text{Inv}(P_1 \to e) = [\underbrace{1, 1, 1}_{\text{Pass 1}}, \underbrace{0, 1, 0}_{\text{Pass 2}}, \underbrace{1, 0, 0}_{\text{Pass 3}}]$$

---

## Kendall Tau Distance

$$\sum \text{Inv}(P_1 \to e) = 1+1+1+0+1+0+1+0+0 = 5$$

This is the **geodesic distance** from $P_1$ to the identity in the permutohedron — the minimum number of adjacent transpositions needed to sort the permutation.




## NOTE
 - for a vector $P \in S_N$ bubble sort will need $(N-1)$ comparisons for each pass and the maximum number of passes is $(N-1)$ for $P=e^{-1}$.
 - OPTIMIZED APPROACH: we will need less comparisons in each consequitive pass.
 - UNOPTIMZAED APPROACH: maximum length of the inversion code in $(N-1)^2$. 
 - OPTIMIZED APPROACH (shrinking range) $(N-1) + (N-2) +\dots +1 = N(N-1)/2$.


-----------------




# Show me how the optimized (shrinkng range) approach would work?


Great question! The optimized bubble sort shrinks the comparison range after each pass because the largest element "bubbles up" to its final position. This reduces total comparisons from $n \times (n-1)$ to $\frac{n(n-1)}{2}$ (triangular number).Here's the key insight:

| Pass | Range | Why |
|:----:|:-----:|:----|
| 1 | indices 0-3 | Full array |
| 2 | indices 0-2 | The $3$ bubbled to position 3 — skip it |
| 3 | indices 0-1 | The $2$ bubbled to position 2 — skip it too |

This gives you a **triangular structure**: $3 + 2 + 1 = 6$ comparisons instead of $3 \times 3 = 9$.

The optimized vector $[1,1,1,0,1,1]$ is more compact but encodes the same 5 inversions. It also maps directly to the **Lehmer code** $(3,1,1,0)$ — each pass's swap count corresponds to how many smaller elements sit to the right of each position.

-----------------
-----------------
-----------------
-----------------
-----------------





# Building the Inversion Vector Inv(P1→e)

The inversion vector $\text{Inv}(P_1 \to e)$ encodes the **bubble sort trace** — it records every swap (1) or no-swap (0) as you transform permutation $P_1$ into the identity $e = [0, 1, 2, 3]$.

## The Analogy

Think of it like a **flight recorder for bubble sort**. Each bit in the vector is a yes/no answer to: "Did we swap at this comparison?"

## The Structure

For $n = 4$ elements, bubble sort performs **3 passes**, each with **3 adjacent comparisons**:

$$\underbrace{(0,1), (1,2), (2,3)}_{\text{Pass 1}}, \underbrace{(0,1), (1,2), (2,3)}_{\text{Pass 2}}, \underbrace{(0,1), (1,2), (2,3)}_{\text{Pass 3}}$$

This gives us $3 \times 3 = 9$ comparison slots — exactly the length of your vector.

## Step-by-Step Trace

Starting with $P_1 = [3, 1, 2, 0]$:

| Pass | Compare | Before | Swap? | After | Bit |
|:----:|:-------:|:------:|:-----:|:-----:|:---:|
| **1** | (0,1) | [**3, 1**, 2, 0] | 3 > 1 → Yes | [1, 3, 2, 0] | **1** |
| **1** | (1,2) | [1, **3, 2**, 0] | 3 > 2 → Yes | [1, 2, 3, 0] | **1** |
| **1** | (2,3) | [1, 2, **3, 0**] | 3 > 0 → Yes | [1, 2, 0, 3] | **1** |
| **2** | (0,1) | [**1, 2**, 0, 3] | 1 < 2 → No | [1, 2, 0, 3] | **0** |
| **2** | (1,2) | [1, **2, 0**, 3] | 2 > 0 → Yes | [1, 0, 2, 3] | **1** |
| **2** | (2,3) | [1, 0, **2, 3**] | 2 < 3 → No | [1, 0, 2, 3] | **0** |
| **3** | (0,1) | [**1, 0**, 2, 3] | 1 > 0 → Yes | [0, 1, 2, 3] | **1** |
| **3** | (1,2) | [0, **1, 2**, 3] | 1 < 2 → No | [0, 1, 2, 3] | **0** |
| **3** | (2,3) | [0, 1, **2, 3**] | 2 < 3 → No | [0, 1, 2, 3] | **0** |

## Result

$$\text{Inv}(P_1 \to e) = [\underbrace{1, 1, 1}_{\text{Pass 1}}, \underbrace{0, 1, 0}_{\text{Pass 2}}, \underbrace{1, 0, 0}_{\text{Pass 3}}]$$

## Key Insight

The **sum** of this vector equals the **Kendall tau distance** (number of inversions):

$$\sum \text{Inv}(P_1 \to e) = 1+1+1+0+1+0+1+0+0 = 5$$

This is exactly how many adjacent transpositions are needed to sort $P_1$ — the geodesic distance in the permutohedron!












-----------------
-----------------
-----------------
-----------------
-----------------
-----------------








## Overview

**Starting Permutation:** $P_1 = [3, 1, 2, 0]$

**Target (Identity):** $e = [0, 1, 2, 3]$

**Method:** Record each swap (1) or no-swap (0) during bubble sort

---

## Pass 1

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | [<span style="color:red">**3**</span>, <span style="color:red">**1**</span>, 2, 0] | 3 > 1 → **Yes** | [1, 3, 2, 0] | **1** |
| (1,2) | [1, <span style="color:red">**3**</span>, <span style="color:red">**2**</span>, 0] | 3 > 2 → **Yes** | [1, 2, 3, 0] | **1** |
| (2,3) | [1, 2, <span style="color:red">**3**</span>, <span style="color:red">**0**</span>] | 3 > 0 → **Yes** | [1, 2, 0, 3] | **1** |

**Pass 1 bits:** $[1, 1, 1]$

---

## Pass 2

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | [<span style="color:red">**1**</span>, <span style="color:red">**2**</span>, 0, 3] | 1 < 2 → No | [1, 2, 0, 3] | 0 |
| (1,2) | [1, <span style="color:red">**2**</span>, <span style="color:red">**0**</span>, 3] | 2 > 0 → **Yes** | [1, 0, 2, 3] | **1** |
| (2,3) | [1, 0, <span style="color:red">**2**</span>, <span style="color:red">**3**</span>] | 2 < 3 → No | [1, 0, 2, 3] | 0 |

**Pass 2 bits:** $[0, 1, 0]$

---

## Pass 3

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | [<span style="color:red">**1**</span>, <span style="color:red">**0**</span>, 2, 3] | 1 > 0 → **Yes** | [0, 1, 2, 3] | **1** |
| (1,2) | [0, <span style="color:red">**1**</span>, <span style="color:red">**2**</span>, 3] | 1 < 2 → No | [0, 1, 2, 3] | 0 |
| (2,3) | [0, 1, <span style="color:red">**2**</span>, <span style="color:red">**3**</span>] | 2 < 3 → No | [0, 1, 2, 3] | 0 |

**Pass 3 bits:** $[1, 0, 0]$

---

## Final Result

$$\text{Inv}(P_1 \to e) = [\underbrace{1, 1, 1}_{\text{Pass 1}}, \underbrace{0, 1, 0}_{\text{Pass 2}}, \underbrace{1, 0, 0}_{\text{Pass 3}}]$$

---

## Kendall Tau Distance

$$\sum \text{Inv}(P_1 \to e) = 1+1+1+0+1+0+1+0+0 = 5$$

This is the **geodesic distance** from $P_1$ to the identity in the permutohedron — the minimum number of adjacent transpositions needed to sort the permutation.




--------


















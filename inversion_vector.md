# Building the Inversion Vector $\text{Inv}(P_1 \to e)$



# Building the Inversion Vector $\text{Inv}(P_1 \to e)$

## Overview

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


















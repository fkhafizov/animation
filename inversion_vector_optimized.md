# Building the Inversion Vector: Optimized (Shrinking Range) Approach

## Overview

**Starting Permutation:** $P_1 = [3, 1, 2, 0]$

**Target (Identity):** $e = [0, 1, 2, 3]$

**Key Insight:** After each pass, the largest unsorted element is guaranteed to be in its final position — no need to compare it again!

---

## Comparison Structure

| Approach | Pass 1 | Pass 2 | Pass 3 | Total Comparisons |
|:---------|:------:|:------:|:------:|:-----------------:|
| Standard | 3 | 3 | 3 | $3 \times 3 = 9$ |
| Optimized | 3 | 2 | 1 | $3 + 2 + 1 = 6$ |

For $n$ elements: Optimized uses $\frac{n(n-1)}{2}$ comparisons (triangular number)

---

## Pass 1 — Compare indices 0, 1, 2, 3

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | $[\textcolor{red}{3}, \textcolor{red}{1}, 2, 0]$ | 3 > 1 → **Yes** | $[\textcolor{red}{1}, \textcolor{red}{3}, 2, 0]$ | **1** |
| (1,2) | $[1, \textcolor{red}{3}, \textcolor{red}{2}, 0]$ | 3 > 2 → **Yes** | $[1, \textcolor{red}{2}, \textcolor{red}{3}, 0]$ | **1** |
| (2,3) | $[1, 2, \textcolor{red}{3}, \textcolor{red}{0}]$ | 3 > 0 → **Yes** | $[1, 2, \textcolor{red}{0}, \textcolor{red}{3}]$ | **1** |

**Pass 1 bits:** $[1, 1, 1]$

**State after Pass 1:** $[1, 2, 0, \boxed{3}]$ — the $3$ is now in its final position!

---

## Pass 2 — Compare indices 0, 1, 2 only (skip index 3)

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | $[\textcolor{red}{1}, \textcolor{red}{2}, 0, \boxed{3}]$ | 1 < 2 → No | $[\textcolor{red}{1}, \textcolor{red}{2}, 0, \boxed{3}]$ | 0 |
| (1,2) | $[1, \textcolor{red}{2}, \textcolor{red}{0}, \boxed{3}]$ | 2 > 0 → **Yes** | $[1, \textcolor{red}{0}, \textcolor{red}{2}, \boxed{3}]$ | **1** |

**Pass 2 bits:** $[0, 1]$

**State after Pass 2:** $[1, 0, \boxed{2}, \boxed{3}]$ — the $2$ is now in its final position!

---

## Pass 3 — Compare indices 0, 1 only (skip indices 2, 3)

| Compare | Before | Swap? | After | Bit |
|:-------:|:------:|:-----:|:-----:|:---:|
| (0,1) | $[\textcolor{red}{1}, \textcolor{red}{0}, \boxed{2}, \boxed{3}]$ | 1 > 0 → **Yes** | $[\textcolor{red}{0}, \textcolor{red}{1}, \boxed{2}, \boxed{3}]$ | **1** |

**Pass 3 bits:** $[1]$

**State after Pass 3:** $[\boxed{0}, \boxed{1}, \boxed{2}, \boxed{3}]$ — sorted!

---

## Final Result

$$\text{Inv}_{\text{opt}}(P_1 \to e) = [\underbrace{1, 1, 1}_{\text{Pass 1}}, \underbrace{0, 1}_{\text{Pass 2}}, \underbrace{1}_{\text{Pass 3}}]$$

**Vector length:** 6 bits (vs. 9 in standard approach)

---

## Comparison of Approaches

| Property | Standard | Optimized |
|:---------|:--------:|:---------:|
| Vector | $[1,1,1,0,1,0,1,0,0]$ | $[1,1,1,0,1,1]$ |
| Length | 9 | 6 |
| Sum (inversions) | 5 | 5 |
| Structure | $(n-1) \times (n-1)$ grid | Triangular |

Both approaches count the same **5 inversions** (Kendall tau distance), but the optimized approach uses fewer comparisons by avoiding redundant checks on already-sorted elements.

---

## The Lehmer Code Connection

The optimized inversion vector has a direct relationship to the **Lehmer code**. Each pass essentially counts how many smaller elements remain to the right of each position — which is exactly what the Lehmer code encodes!

For $P_1 = [3, 1, 2, 0]$:
- Position 0: value 3 has 3 smaller elements to its right → contributes 3 swaps in Pass 1
- Position 1: value 1 has 1 smaller element to its right → contributes 1 swap in Pass 2  
- Position 2: value 2 has 1 smaller element to its right → contributes 1 swap in Pass 3

Lehmer code: $(3, 1, 1, 0)$ — and $3 + 1 + 1 + 0 = 5$ inversions ✓

# dist(P1,P2)

2026.01.03

# Finding Distance Between P1 and P2

Let me compute the distance between these two permutations using the **inversion count** method.

## The Algorithm

In the permutohedron (Cayley graph with adjacent transpositions), the distance between permutations $\pi$ and $\sigma$ is:

$$d(\pi, \sigma) = \text{inversions}(\sigma \circ \pi^{-1})$$

where an **inversion** is a pair $(i,j)$ with $i < j$ but the value at position $i$ is greater than the value at position $j$.

## Step-by-Step Calculation

**Given:**
- P1 = $[3, 2, 1, 0]$
- P2 = $[0, 3, 1, 2]$

**Step 1: Find** $\text{P1}^{-1}$

The inverse tells us "where is each element located?"
- Where is 0? Position 3 → $\text{P1}^{-1}[0] = 3$
- Where is 1? Position 2 → $\text{P1}^{-1}[1] = 2$
- Where is 2? Position 1 → $\text{P1}^{-1}[2] = 1$
- Where is 3? Position 0 → $\text{P1}^{-1}[3] = 0$

So $\text{P1}^{-1} = [3, 2, 1, 0]$ (P1 is **self-inverse**!)

**Step 2: Compute** $\text{P2} \circ \text{P1}^{-1}$

Apply composition: $(\text{P2} \circ \text{P1}^{-1})[i] = \text{P2}[\text{P1}^{-1}[i]]$

- Position 0: $\text{P2}[\text{P1}^{-1}[0]] = \text{P2}[3] = 2$
- Position 1: $\text{P2}[\text{P1}^{-1}[1]] = \text{P2}[2] = 1$
- Position 2: $\text{P2}[\text{P1}^{-1}[2]] = \text{P2}[1] = 3$
- Position 3: $\text{P2}[\text{P1}^{-1}[3]] = \text{P2}[0] = 0$

Result: $[2, 1, 3, 0]$

**Step 3: Count Inversions in** $[2, 1, 3, 0]$

Compare all pairs $(i,j)$ where $i < j$:

| Pair | Values | Inversion? |
|------|--------|------------|
| (0,1) | 2 vs 1 | ✓ (2 > 1) |
| (0,2) | 2 vs 3 | ✗ (2 < 3) |
| (0,3) | 2 vs 0 | ✓ (2 > 0) |
| (1,2) | 1 vs 3 | ✗ (1 < 3) |
| (1,3) | 1 vs 0 | ✓ (1 > 0) |
| (2,3) | 3 vs 0 | ✓ (3 > 0) |

**Total inversions = 4**

## Answer

$$\boxed{d(\text{P1}, \text{P2}) = 4}$$

## Verification with Code

Let me verify this and show you the actual path:

```python
def count_inversions(perm):
    """Count inversions in a permutation."""
    count = 0
    n = len(perm)
    for i in range(n):
        for j in range(i+1, n):
            if perm[i] > perm[j]:
                count += 1
    return count

def permutation_inverse(perm):
    """Find inverse of a permutation."""
    n = len(perm)
    inv = [0] * n
    for i in range(n):
        inv[perm[i]] = i
    return inv

def compose(p1, p2):
    """Compose two permutations: (p1 ∘ p2)[i] = p1[p2[i]]."""
    return [p1[p2[i]] for i in range(len(p1))]

# Define permutations
P1 = [3, 2, 1, 0]
P2 = [0, 3, 1, 2]

# Compute distance
P1_inv = permutation_inverse(P1)
composition = compose(P2, P1_inv)

distance = count_inversions(composition)

print(f"P1 = {P1}")
print(f"P2 = {P2}")
print(f"P1^(-1) = {P1_inv}")
print(f"P2 ∘ P1^(-1) = {composition}")
print(f"Inversions in {composition}: {distance}")
print(f"\nDistance d(P1, P2) = {distance}")
```

Would you like me to also find the actual sequence of 4 adjacent transpositions that transforms P1 into P2?

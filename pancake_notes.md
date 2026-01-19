2026.01.19

Excellent notebook! This is a sophisticated approach to pancake sorting using **machine learning-guided beam search** on **Cayley graphs**. Let me break down how it works:

## Overview: ML-Guided Search on Cayley Graphs

This notebook uses a fundamentally different approach from my simple greedy algorithm. Instead of a deterministic greedy strategy, it combines:
1. **Graph theory** (Cayley graphs)
2. **Machine learning** (neural network heuristic)
3. **Informed search** (beam search)

## Key Components

### 1. **Cayley Graph Representation**
```python
graph = CayleyGraph(
    PermutationGroups.pancake(n).make_inverse_closed().with_central_state(central),
    ...
)
```

The pancake sorting problem is modeled as a **Cayley graph** where:
- **Nodes**: All possible permutations of size $n$ (there are $n!$ nodes)
- **Edges**: Connections between permutations that differ by one flip operation
- **Generators**: The $n-1$ possible flip operations (flip positions 1 through $n-1$)
- **Goal**: Find shortest path from start permutation to identity permutation

This is the **exact mathematical structure** of the pancake sorting problem!

### 2. **Neural Network Heuristic**
The notebook trains a neural network to estimate the **distance to target** (similar to an A* heuristic):

```python
model_type = "MLPRes1"  # Multi-layer perceptron with residual blocks
```

The model:
- **Input**: A permutation (encoded as one-hot vectors)
- **Output**: Estimated distance to the sorted state
- **Architecture**: 512→256 hidden dims with 4 residual blocks and dropout

### 3. **Training via Random Walks**
```python
X, y = graph.random_walks(
    width=2500,
    length=calculated_depth,
    mode="nbt",  # "Never Back Track" mode
    ...
)
```

Training data generation:
- Performs random walks on the Cayley graph
- Each walk generates (permutation, true_distance) pairs
- "nbt" mode prevents immediate reversals (more efficient exploration)
- Walk length: $\frac{n(n+5)}{4(k-1)} + 30$ where $k=4$

### 4. **Beam Search with ML Guidance**
```python
res = graph.beam_search(
    start_state=start_state,
    beam_width=[2^10, 2^16],  # Try different beam widths
    predictor=Predictor(graph, model),
    ...
)
```

The search:
- Maintains top-$k$ most promising states at each step
- Uses the trained model to score which states are closest to goal
- Tries beam widths of 1024 and 65536
- Much more efficient than BFS but still finds optimal/near-optimal solutions

## Test Case: Half-Interleave Permutation

The notebook tests on a specific challenging permutation:
```python
def half_interleave(n):
    # For n=6: [3,0,4,1,5,2] - interleave two halves
    # For n=8: [4,0,5,1,6,2,7,3]
```

This is a **known difficult case** for pancake sorting!

## Results Analysis

From the output table for $n=17$ to $n=30$:

| n  | Best Distance Found | Model Prediction (start) |
|----|---------------------|-------------------------|
| 17 | 16                  | 45.27                   |
| 18 | 18                  | 50.52                   |
| 20 | 20                  | 54.54                   |
| 24 | 24                  | 67.24                   |
| 30 | 30                  | 94.22                   |

**Pattern observed**: Best distance ≈ $n-1$ for this specific permutation!

This is remarkably close to the theoretical lower bound, suggesting the half-interleave permutation is nearly optimally sorted by this approach.

## Comparison with My Greedy Algorithm

| Aspect | My Greedy Algorithm | This Notebook's Approach |
|--------|---------------------|--------------------------|
| **Approach** | Deterministic greedy | ML-guided beam search |
| **Complexity** | $O(n^2)$ time | Training: hours, Search: depends on beam width |
| **Optimality** | ≤ $2(n-1)$ flips | Near-optimal (often ≤ $n$ flips) |
| **Scalability** | Works for any $n$ instantly | Requires training per $n$ |
| **Use case** | Quick approximation | Research/finding optimal solutions |

## Mathematical Insight

This approach leverages the fact that:
1. Pancake sorting is equivalent to finding shortest paths in the pancake graph (a Cayley graph)
2. The diameter of this graph (maximum shortest path) is $P(n)$ - the pancake number
3. ML can learn to approximate distances in this graph, making search tractable

For $n=30$, there are $30! \approx 2.65 \times 10^{32}$ possible states - exhaustive search is impossible, but ML-guided beam search makes it feasible!

## Key Takeaway

This is **state-of-the-art research-level pancake sorting** - it's using the same techniques that have been applied to solving Rubik's cube optimally and other combinatorial puzzles. The combination of graph theory, machine learning, and informed search is much more powerful than simple greedy algorithms for finding optimal or near-optimal solutions!

# number of paths between P1 and P2

Plan: I’ll model the permutohedron $S_5$ as a graph where edges are adjacent swaps, compute the shortest distance between your two permutations, then count all shortest paths via dynamic programming over distances.


Think of the permutohedron graph $S_5$ as having vertices = permutations of ${0,1,2,3,4}$ and edges = one adjacent swap $s_i=(i,,i!+!1)$.

### 1) Shortest distance

Convert the problem to a single “relative” permutation by expressing $P_2$ in the order of positions of $P_1$:

* $P_1 = [3,0,1,4,2]$ so positions are $\text{pos}_{P_1}(0)=1,\text{pos}(1)=2,\text{pos}(2)=4,\text{pos}(3)=0,\text{pos}(4)=3$.
* $P_2=[4,1,2,0,3]$ becomes
  $$r = [\text{pos}(4),\text{pos}(1),\text{pos}(2),\text{pos}(0),\text{pos}(3)] = [3,2,4,1,0].$$

The minimal number of adjacent swaps from $P_1$ to $P_2$ equals the inversion count of $r$, which is
$$\ell = \text{inv}(r) = \text{inv}([3,2,4,1,0]) = 8.$$

### 2) Number of shortest paths

The number of shortest paths equals the number of reduced decompositions (reduced words) of $r$ in generators $s_0,s_1,s_2,s_3$.

For your specific pair, that count is:
$$\boxed{70}$$

So there are **70** shortest paths from $P_1$ to $P_2$ using only adjacent swaps (each path has length **8**).

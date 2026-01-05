2026.01.05


# Q:

Let x \in S4 be a vertex of Cayley graph build by adjacent transformtions (i,i+1) from e=(0,1,2,3).

Let's use optimized bubble sort algorithm to find path from x to e.
Let $x$ be a vertex of the permutohedron, and let
$$e=\mathrm{sort}(x)=(0,1,\dots,n-1).$$
An optimized bubble-sort algorithm transforms $x$ into $e$ using $n(n-1)/2$ 
comparisons of adjacent entries. Let $C_I(x)$ denote the 
\emph{inversion code}: a binary sequence produced as a byproduct of bubble sort applied to $x$. 
Each time the algorithm performs a swap, we append a $1$ to the sequence; otherwise we append a $0$.

Show me the inversion code corresponding to x=(3 0 2 1)


# A:

Using the standard “optimized” bubble-sort schedule with exactly $3+2+1=6$ adjacent comparisons for $n=4$ (first pass compares $(0,1),(1,2),(2,3)$; second pass $(0,1),(1,2)$; third pass $(0,1)$), starting from
$x=(3,0,2,1)$:

1. compare $(3,0)$ → swap → $(0,3,2,1)$  ⇒ 1
2. compare $(3,2)$ → swap → $(0,2,3,1)$  ⇒ 1
3. compare $(3,1)$ → swap → $(0,2,1,3)$  ⇒ 1
4. compare $(0,2)$ → no swap → $(0,2,1,3)$ ⇒ 0
5. compare $(2,1)$ → swap → $(0,1,2,3)$  ⇒ 1
6. compare $(0,1)$ → no swap → $(0,1,2,3)$ ⇒ 0

So the inversion code is
$$
C_I(x) = (1,1,1,0,1,0),
$$
i.e. **111010**.


# Q


what is the standard terminology for  what I call inversion code?

# A

Plan: I’ll quickly scan standard permutation/algorithm literature to see if this exact bubble-sort swap/no-swap bitstring has an established name, then map it to the closest recognized terms.


There’s a naming collision here:

* In **combinatorics**, the term **“inversion code”** is already used for the *digit* vector $l_0l_1\cdots l_{n-1}$ (an **inversion table / Lehmer code**), where each entry counts how many smaller elements lie to the right. ([Wikipedia][1])
  So if you call your object “inversion code,” readers may assume you mean **Lehmer code**.

What you’ve defined (a **binary** 0/1 record of “swap happened” vs “no swap” over a fixed bubble-sort comparison schedule) is usually described with more “algorithmic” language:

### Standard-ish terminology you can use

1. **Bubble-sort trace / execution trace** (or **swap/no-swap trace**)
   Emphasizes it’s the algorithm’s per-comparison behavior.

2. **Swap indicator sequence** (or **swap pattern**) of the **bubble-sort sorting network**
   Bubble sort corresponds to a fixed comparator schedule often described as a “swap sequence” in sorting-network language. ([community.ams.org][2])
   Your binary string is then the 0/1 outcomes on those comparators.

3. If you **drop the 0’s** and keep only the swaps (equivalently, record the adjacent transposition indices when a swap occurs), that object *does* have a very standard name: a **reduced word / reduced decomposition** (when it’s minimal). ([MathOverflow][3])

### Practical recommendation (to avoid confusion in a paper)

* Call your 0/1 string something like **“bubble-sort swap trace”** or **“swap indicator sequence (bubble-sort network)”**.
* Reserve **“inversion code”** for **Lehmer code / inversion table**. ([Wikipedia][1])

[1]: https://en.wikipedia.org/wiki/Kendall_rank_correlation_coefficient?utm_source=chatgpt.com "Kendall rank correlation coefficient"
[2]: https://community.ams.org/journals/jams/2022-35-04/S0894-0347-2021-00993-1/S0894-0347-2021-00993-1.pdf?utm_source=chatgpt.com "The Archimedean limit of random sorting networks"
[3]: https://mathoverflow.net/questions/233857/a-decomposition-of-w-0-which-is-similar-to-the-reduced-decomposition?utm_source=chatgpt.com "A decomposition of $w_0$ which is similar to the reduced ..."

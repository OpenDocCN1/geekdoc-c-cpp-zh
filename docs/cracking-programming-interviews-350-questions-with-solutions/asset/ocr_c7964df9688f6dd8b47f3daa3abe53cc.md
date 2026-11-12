# ## 2.2. Searching in Two Dimensional Sequence

![](bbox=[0.29, 0.06, 0.61, 0.224])

# ### Invariant

Looking at the precondition and postcondition, it is not that difficult to figure out that during the execution of our algorithm, `x` is guaranteed to be confined within some L-shaped region of `a`.

Let us revisit this in light of the invariant which bears that `x` is not in the already-searched rows `a[0..i − 1]` and not in the already-searched columns `a[i, 0..j − 1]` of the current row `i`.

Let us represent this invariant below.

![](bbox=[0.317, 0.438, 0.62, 0.6])

Search space is bounded by L-shaped region. Doesn't it look more like a L-shaped region?

**Invariant:**

`0 ≤ i < m ∧ 0 ≤ j < n ∧`  
`searchable-region is bounded by (m − i) * n − j`

# ### Initialization

Before we develop body of the program, let us re-think about what should be the starting point of search, i.e., what should be the initial values of the counters `i` and `j`?

Let us say it is set to 0 to start with, i.e., `i = 0` and `j = 0`. If this is so then the region marked as `x is not found here` is empty to start with. Fair enough. Invariant still holds true.
**Proof**  Assume that *same_color*(A[j], A[i + 1]) = false. We have to show that j ≥ i + 2. We know from the invariant that j ≥ i + 1. If j = i + 1, then *same_color*(A[j], A[i + 1]) = true. Therefore, j ≠ i + 1. It follows that j ≥ i + 2. ■

Using this observation, we can further simplify the algorithm, and obtain the final algorithm:

```
    Algorithm 53 Find Majority Algorithm Final
    1: i ← 0
    2: j ← 1
    3: while j ≤ n do
    4:   if same_color(A[j], A[i + 1]) == false then
    5:     i ← i + 2
    6:     swap(A[j], A[i])
    7:   end if
    8:   j ← j + 1
    9: end while
    10: return A[i + 1]
```

# ## 2.15 Mode of a Multiset

# ### Problem

Let S = (x₁, x₂, …, xₙ) be a multiset of (not necessarily distinct) elements from a totally ordered set. A *mode* of a multiset is defined as an element that occurs most frequently in the multiset (there may be more than one mode). The number of times an element occurs is called its *multiplicity*. The mode is thus the element with the highest multiplicity.

*Find a mode of a given multiset S.*

# ### Solution

Our goal is to minimize the number of comparisons. One possible way to find the mode is to use sorting. Once the elements are sorted, we can scan the sorted sequence and count the multiplicities (equal elements will be consecutive in the sorted sequence). We will see that sorting is not always necessary. The reason for thinking that sorting may not be required is that finding the majority can be done in linear time, whereas sorting requires *O(n log n)* time. This leads us to suspect that, if the multiplicity of the mode is high, then there may be a fast way of finding it without sorting.
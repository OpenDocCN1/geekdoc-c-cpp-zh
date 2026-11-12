
```cpp
int cref[] = {3, 8, 2, 7, 6};
int c[] = {3, 8, 2, 7, 6};

std::prev_permutation(c, c + 5);
assert(std::equal(c, c + 5, cref));

int dref[] = {8, 3, 6, 6, 4, 1, 1};
int d[] = {8, 3, 4, 4, 1, 1, 2, 6, 6, 6};

std::prev_permutation(std::begin(d),
                      std::end(d));

assert(std::equal(std::begin(d), std::end(d),
                  dref));

std::vector<int> vref
{1,2,3,4,5,6,7,8,4,9,8,7,6,5,4,3,2,1};
std::vector<int> v
{1,2,3,4,5,6,7,8,1,2,3,4,4,6,7,8,9};

std::prev_permutation(v.begin(), v.end());

assert(std::equal(v.begin(), v.end(),
                  vref.begin()));
}
```

*Time Complexity* is at most (last - first)/2 swaps.

## 6.2 Searching in Possibly Empty Two Dimensional Sequence

### Problem

Design an algorithm to search for a given integer \(x\) in a 2-dimensional array \(a[0..m][0..n]\) where \(0 < m\) and \(0 < n\). In case of multiple occurrences, it doesn’t matter which is found. This is similar to the problem discussed earlier except that here the array may be empty, i.e., it may have 0 rows or 0 columns.

### Solution

The algorithm should find the position of a given integer \(x\) in the array \(a\), i.e., the algorithm should find \(i\) and \(j\) such that

- \(x = a[i,j]\) or
- \(i = m\).

Let us treat the input array as some kind of a rectangular region.

![](img/78e1bff64796dccbf49e7c84b8201fb2_262_0.png)

The problem demands that the integer \(x\) does exist somewhere in this region. Let us label this condition as *Input Assertion* or *Precondition*.

```text
Input Assertion|Precondition (aka Input Assertion)
    x ∈ a[0..m - 1, 0..n - 1]
i.e., x is present somewhere in this rectangular region a.
```

![](img/78e1bff64796dccbf49e7c84b8201fb2_262_1.png)

After the program terminates successfully, \(x\) has to be found in a rectangular region of \(a\) where the rectangular region consists of just one row and column. Let us label this condition as *Output Assertion* or *Result Assertion* or *Postcondition*.

```text
Output Assertion|Postcondition (aka Result Assertion)

After the program terminates successfully, then x is in a rectangular region of a where the rectangular region consists of just one row and column, i.e., x is present at i^th row and j^th column of a, or if this is not possible then i = m, i.e., if x is not found in the array, i.e., if x ≠ a[i, j], then i = m.

(0 ≤ i ≤ m - 1 ∧ 0 ≤ j ≤ n - 1
 ∧ x = a[i, j]) ∨ (i = m ∧ x ∉ a)
```

![](img/78e1bff64796dccbf49e7c84b8201fb2_263_0.png)

### Invariant

The invariant states that \(x\) is not in the already-searched rows \(a[0..i − 1]\) and not in the already-searched columns \(a[i, 0..j − 1]\) of the current row \(i\).

![](img/78e1bff64796dccbf49e7c84b8201fb2_263_1.png)

**Invariant:**

`0 ≤ i ≤ m ∧ 0 ≤ j ≤ n ∧`

`searchable-region` is bounded by `(m − i) * n − j + m − i`, i.e., the bound function is the sum of the number of values in the untested section and the number of rows in the untested section represented by `(m − i) * n − j + m − i`.

The extra value `m − i` is required here because `j` can take up the boundary value `n`, i.e., `j = n`. As an astute reader, you must have noticed that now the invariant includes `j ≤ n`, instead of `j < n`. This is required here because the number of columns, `n`, is out of bounds.

Initialization step is same as discussed earlier.

### Condition

Similar to the problem discussed earlier, we can think about `j ← j + 1` and/or `i ← i + 1` to maintain the invariance.

```text
if i ≠ m ∧ (j < n and x ≠ a[i,j]) then j ← j + 1
```

Taking this as a condition, the program can terminate when `i < m ∧ j = n`. If \(x\) is not found in the very first row, then this will terminate.

So we need some suitable condition for handling increase of \(i\) as well. We can try \(i \leftarrow i + 1\) but this is only possible till \(i < m\) and it can maintain the invariant only if the \(x \notin a[i, 0..n]\), so we can think of additional condition being \(j == n \implies j = 0\) to maintain the condition on the \(i^{th}\) row.

### Algorithm 68 Searching in a possibly empty 2D Array

```text
1: i <- 0
2: j <- 0
3: function 2D-SEARCH(a[0..m-1, 0..n-1], x)
4:   while i != m and j != n and x != a[i, j] do
5:     j <- j + 1
6:     if i != m and j == n then
7:       i <- i + 1
8:       j <- 0
9:     end if
10:    end while
11: end function
```

### C++11 Implementation

Program 6.6: Searching 2D Array

```cpp
1:#include <algorithm>
2:#include <array>
3:
4: using Point = std::pair<int, int>;
5:
6: template <int m, int n>
7: using TwoDimArray =
8:     std::array<std::array<int, n>, m>;
9:
10: template <int m, int n>
11: Point search_2darray(TwoDimArray<m, n>& a,
12:                     int x)
13: {
14:     Point p(-1, -1);
15:
16:     int i = 0, j = 0;
17:
18:     while((i != m) && (j != n) && (x != a[i][j]))
19:     {
20:         j += 1;
21:         if((i != m) && (j == n))
22:         {
23:             i += 1;
24:             j = 0;
25:         }
26:     }
27:
28:     p.first = i;
    p.second = j;
    return p;
}
```

### Usage

Program 6.7: Search for 6: yields a 2 2

```cpp
#include "2darray_search_contd.hpp"
#include <iostream>

int main()
{
    TwoDimArray<4, 4> a = {
        12, 2, 83, 5,
        30, 14, 15, 16,
        13, 5, 6, 81,
        23, 6, 7, 19
    };

    Point p = search_2darray<4, 4>(a, 6);

    std::cout << "6 is found at: " << p.first << "]["
              << p.second << "]";
    std::cout << std::endl;
}
```

### Time Complexity

It is \(O(mn)\) because it ends up traversing the entire region \(m \times n\) as far as comparison is concerned.

### Correctness

As discussed in the previous section earlier, let us try proving correctness of the program developed by proving the veracity of Postcondition upon termination, i.e.,

> > Invariant ∧ Condition ⟶ Complement ⟶ Postcondition

Please note that the algorithm has 2 conditions namely

- 1. \(i \ne m \land j \ne n\). If this is false ⇒ \(i = m\) may be true. In this case, the invariant implies that \(x \ne a\), i.e., \(x \ne a[i, j]\).
- 2. \(i \ne m \land j == n\). (If this is false and \(i \ne m\)) ⇒ \(j \ne n\).

Therefore the first condition being false ⇒ \(x = a[i, j]\).

$$(i == m) \lor (i \ne m \land j \ne n \land x = a[i,j])$$

Complement of this condition in conjunction with invariant $\Rightarrow$ the result assertion, which proves correctness of our program developed above.

## 6.3 Matching Nuts and Bolts Optimally

### Problem Description

There is a bag full of \(n\) nuts and \(n\) bolts, each of distinct sizes, such that there is one-to-one correspondence between the nuts and the bolts, i.e., for every nut, there is a bolt and vice versa. Nuts cannot be compared to nuts and bolts cannot be compared to bolts directly, but nuts can be compared to bolts by trying to fit one into the other. Design and implement an optimal algorithm for fitting all nuts to bolts. By optimal we mean to minimize the number of comparisons involved in the algorithm.

### Solution

The same problem can be posed to a computer scientist as follows:

Given two sets \(B : \{b_1, \ldots, b_n\}\) and \(N : \{n_1, \ldots, n_n\}\), where \(B\) is a set of distinct real numbers (representing the sizes of the bolts) and \(N\) is a permutation of \(B\), we wish to find efficiently the unique permutation \(\sigma \in S_n\) such that \(b_i = n_{\sigma(i)}\), based on queries of the form *compare* \(b_i\) and \(n_j\). The answer to each such query is either:

- 1. \(b_i > n_j\)
- 2. \(b_i = n_j\)
- 3. \(b_i < n_j\)

Since there are \(n!\) possibilities for \(\sigma\), the obvious information theoretic lower bound shows that any bounded degree decision tree that solves the problem has depth at least \(\log_3(n!)\).

Using Stirling’s approximation:

$$\log_3(n!) \approx \Theta(n \log_3 n)$$

Similar to comparison-based sorting, it can be analyzed using decision tree. Please note that we can model any algorithm for matching nuts and bolts as a decision tree.

The tree will be a *ternary tree*, since every comparison has three possible outcomes:

- 1. *less than,*

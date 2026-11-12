
element is within \(k\) slots of its proper position. We therefore provide a lower bound on the number of possible permutations that satisfy this condition.

First, break the array of size \(n\) into \(\lfloor n/k \rfloor\) blocks, each of size \(k\), and the remainder of size \(n \bmod k\). For each block, there exist \(k!\) permutations, resulting in at least \((k!)^{\lfloor n/k \rfloor}\) total permutations of the entire array. None of these permutations move an element more than \(k\) slots.

Notice that this undercounts the total number of permutations, since no element moves from one \(k\)-element block to another, and we ignore permutations of elements in the remainder block.

We therefore conclude that the decision tree has at least \((k!)^{\lfloor n/k \rfloor}\) leaves. Since the decision tree is a binary tree, we can then conclude that the height of the decision tree is

$$
\begin{aligned}
&\ge \log\left((k!)^{\lfloor n/k \rfloor}\right)\\
&\ge \left\lfloor\frac{n}{k}\right\rfloor \log(k!)\\
&\ge \left\lfloor\frac{n}{k}\right\rfloor(c_1 k\log k)\\
&\ge c_1(n-k)\log k\\
&\ge \frac{c_1 n\log k}{2}\\
&= \Omega(n\log k)
\end{aligned}
$$

(The last step follows because of our assumption that \(k \le n/2\).)

4. For the solution to this problem, we are going to use a heap. We assume that we have a heap with the following subroutines:

- **MAKE-HEAP()** returns a new empty heap.
- **INSERT(H, key, value)** inserts the key/value pair into the heap.
- **EXTRACT-MIN(H)** removes the key/value pair with the smallest key from the heap, returning the value.

First, consider the problem of merging \(t\) sorted lists. Assume we have lists \(A_1,\ldots,A_t\), each of which is sorted. We use the following strategy (pseudocode below):

- a) Make a new heap, \(H\).
- b) For each of the \(t\) lists, insert the first element into the heap. For list \(i\), perform \(\operatorname{INSERT}(H, A_i[1], i)\).
- c) Repeat \(n\) times:
  - i. Remove the smallest element from the heap using \(\operatorname{EXTRACT-MIN}(H)\). Let \(v\) be the value returned, which is the identity of the list.
  - ii. Put the extracted element from list \(v\) in order in a new array.
  - iii. Insert the next element from the list \(v\).

The key invariant is to show that after every iteration of the loop, the heap contains the smallest element in every list. (We omit a formal induction proof, as the question only asked you to devise an algorithm.) Notice that each EXTRACT-MIN and INSERT operation requires \(O(\log k)\) time, since there are never more than \(2k\) elements in the heap. The loop requires only a constant amount of other work, and is repeated \(n\) times, resulting in \(O(n\log k)\) running time.

In order to apply this to our problem, we consider \(A\) as a set of sorted lists. In particular, notice that \(A[i] < A[i + 2k + 1]\), for all \(i \le n - 2k - 1\): the element at slot \(i\) can at most move forwards during sorting to slot \(i + k\) and the element at slot \(i + 2k + 1\) can at most move backwards during sorting to slot \(i + k + 1\).

For the moment, assume that \(n\) is divisible by \(2k\). We consider the \(t = 2k\) lists defined as follows:

$$
\begin{aligned}
A_1 &= A[1], A[2k+1], A[4k+1], \ldots, A[n-(2k-1)] \\
A_2 &= A[2], A[2k+2], A[4k+2], \ldots, A[n-(2k-2)] \\
&\vdots \\
A_t &= A[2k], A[4k], A[6k], \ldots, A[n]
\end{aligned}
$$

Each of these lists is sorted, and each of them is of size \(\le n\). Therefore, we can sort these lists in \(O(n\log k)\) time using the procedure above.

We now present the more precise pseudocode:

```text
Algorithm 13 Sort Almost Sorted Algorithm
1: function SORT-ALMOST-SORTED(A, n, k)        ▷ Sort A if every element is within k slots of its proper position
2:     H ← MAKE-HEAP()
3:     for i ← 1 to 2k do
4:         INSERT(H, A[i], i)
5:     end for
6:     for i ← 1 to n do
7:         j ← EXTRACT-MIN(H)
8:         B[i] ← A[j]
9:         if j + 2k ≤ n then
10:            INSERT(H, A[j + 2k], j)
11:        end if
12:    end for
13:    return B
14: end function
```

Recall that a heap is generally used to store a key and its associated value, even though we often ignore the value when describing the heap operations. In this case, the value is an index \(j\), while the key is the element \(A[j]\). As a result, the heap returns the index of the next smallest element in the array.

Correctness and performance follow from the argument above.

Notice that there is a second way of solving this problem. Recall that we already know how to merge two sorted lists that (jointly) contain \(n\) elements in \(O(n)\) time. It is possible, then, to merge the lists in a tournament. We give an example for \(k = 8\), where \(A+B\) means to merge lists \(A\) and \(B\):

- Round 1: \((A_1 + A_2), (A_3 + A_4), (A_5 + A_6), (A_7 + A_8)\)
- Round 2: \((A_1 + A_2 + A_3 + A_4), (A_5 + A_6 + A_7 + A_8)\)
- Round 3: \((A_1 + A_2 + A_3 + A_4 + A_5 + A_6 + A_7 + A_8)\)

Notice that there are \(\log k\) merge steps, each of which merges \(n\) elements (dispersed through up to \(k\) lists) and hence has a cost of \(O(n)\). This leads to the desired running time of \(O(n \log k)\).

## 1.8 The Longest Upsequence Problem

### Problem Description

Consider a sequence of values \((v_0, v_1, \ldots, v_{n-1})\). If one deletes \(i\) (not necessarily adjacent) values from the list, one has a subsequence of length \(n-i\). This subsequence is called an *upsequence* if its values are in non-decreasing order. For example, the list \((1, 3, 4, 6, 2, 4)\) has a subsequence \((1, 3, 2)\), which is not an upsequence, and another subsequence \((1, 3, 6)\), which is an upsequence.

Write a program that, given a sequence in \(b[0..n-1]\), where \(n > 0\), calculates the length of the longest upsequence of \(b[0..n-1]\).

### Solution

As an abbreviation, let us use the notation \(lup(s)\) to mean:

\(lup(s) =\) the length of the longest upsequence of sequence \(s\).

Thus using a variable \(k\) to contain the answer, the program has the precondition and postcondition as

\(Q : n > 0\)  
\(R : k = lup(b[0..n-1])\)

Note that a change in any one value of a sequence could change its longest upsequence, and this means that possibly every value of a sequence \(s\) must be interrogated to determine \(lup(s)\). This suggests a loop. Let us begin by writing a possible invariant and an outline of the loop.

The loop will interrogate the values of \(b[0..n-1]\) in some order. Since \(lup(b[0..0])\) is 1, a possible invariant can be derived by replacing the constant \(n\) of \(R\) by a variable:

$$
P : 1 \leq i \leq n \wedge k = lup(b[0..i-1])
$$

The loop itself will have the form

```text
1: i <- 1
2: k <- 1
3: while i != n do
4:     increase i, maintaining P
5: end while
```

Increasing \(i\) extends the sequence \(b[0..i-1]\) for which \(k\) is the length of a longest upsequence, and hence may call for an increase in \(k\). Whether \(k\) is to be increased depends on whether \(b[i]\) is at least as large as a value that ends a longest upsequence of \(b[0..i-1]\), there may be more than one longest upsequence. It makes sense to maintain information in other variables so that such a test can be efficiently made. What is the minimum information needed to ascertain whether \(k\) should be increased?

The *smallest* value, say \(m\), that ends an upsequence of length \(k\) of \(b[0..i-1]\) must be known, for then \(b[0..i]\) has an upsequence of length \(k+1\) if and only if \(b[i] \ge m\). Therefore, we revise invariant \(P\) to include \(m\):

$$
P : 1 \leq i \leq n \wedge k = lup(b[0..i-1]) \wedge m \text{ is the smallest value in } b[0..i-1] \text{ that ends an upsequence of length } k.
$$

In the case \(b[i] \ge m\), \(k\) can be increased and \(m\) set to \(b[i]\), so that the program thus far looks like

```text
1: i <- 1
2: k <- 1
3: m <- b[0]                                 ▷ P
4: while i != n do
5:     if b[i] >= m then
6:         k <- k + 1
7:         m <- b[i]
8:     else if b[i] < m then
9:         ?
10:    end if
11:    i <- i + 1
12: end while
```

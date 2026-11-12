
## 4.3. Max Sub-Array Problem

It prints

```text
Printing Prefix Array with Value and Original Index
8:0 5:1 7:2 8:3 4:4 14:5 9:6
Printing Value Sorted Prefix Array
4:4 5:1 7:2 8:0 8:3 9:6 14:5
Printing Pairwise Value Differences with
original indices
(1:4:1) (2:1:2) (1:2:0) (0:0:3) (1:3:6) (5:6:5)
Subarray with sum closest to zero is
-3 2 1

Printing Prefix Array with Value and Original Index
-3:0 -1:1 3:2 -3:3 -11:4 -1:5 10:6
Printing Value Sorted Prefix Array
-11:4 -3:0 -3:3 -1:1 -1:5 3:2 10:6
Printing Pairwise Value Differences with
original indices
(8:4:0) (0:0:3) (2:3:1) (0:1:5) (4:5:2) (7:2:6)
Subarray with sum closest to zero is
2 4 -6

Printing Prefix Array with Value and Original Index
10:0 8:1 1:2
Printing Value Sorted Prefix Array
1:2 8:1 10:0
Printing Pairwise Value Differences with
original indices
(7:2:1) (2:1:0)
Subarray with sum closest to zero is
10 -2 -7
```

### Find subarray with sum closest to k

### Problem

Find a sub-array whose sum is closest to an integer s.

As can be seen from the previous problem that the sum of a[l..k] =
prefixa[k] - prefixa[l - 1] = s

Hence in order to find the sub-array with sum closest to zero, all we need to find is to locate 2 elements in the prefix array which are closest with respect to k-distance.

Rest of the exercise is left for the reader to work out.

### Maximum 2D subarray problem

### Problem

Design and implement an efficient program to find a contiguous 2D sub-array within a two-dimensional array of integers which has the largest sum.

Bentley has given a nice algorithm based on Kadane’s one dimensional algorithm to solve this problem in two-dimensional array thus making it look like Kadane’s 2D algorithm.

It applies Kadane’s algorithm to every possible row interval, summing over the rows in each interval to produce one dimensional array for Kadane’s algorithm to find the optimal column sum. One of the central idea of Bentley’s algorithm is the *prefix sum*, which aims to avoid repeating summations when processing subsequent row intervals.

The 1D Kadane’s algorithm is run on the elements of each row of the array (*row₁, row₂ … rowₘ*) considered as a 1D stream, then on the sum of each pair of rows (*row₁ + row₂, row₁ + row₃ … row₁ + rowₘ*). The solution is given by the maximal sum produced by the 1D Kadane’s algorithm on these cases. If *x₁* and *x₂* are the pointers to the beginning and end of the maximal sub-stream, and *Rowᵢ* and *Rowⱼ* are the two added rows for which the sum is maximal, then the solution is delimited by the rectangle given by the upper-left (*Rowᵢ, x₁*) and the lower-right corners (*Rowⱼ, x₂*). This algorithm can be summarized as below:

- 1. Compute the *prefix array* in the dimension of length m. This requires *O(mn)* computations.
- 2. If the maximum sub-array is between *Rowᵢ* and *Rowⱼ*, inclusive, then there are \(\frac{m(m+1)}{2}\) such pairs.
- 3. The sum of elements in the array between *Rowᵢ* and *Rowⱼ* for a given column is already computed as a part of our prefix sum. So each column sum looks like a single element of a one dimensional array across all columns, i.e., it looks like a one dimensional array with one row and *n* columns.
- 4. Apply Kadane’s 1D algorithm on such pairs to get the maximum sub-array as described above. Thus total time complexity is *O(m²n²)*.

Let us formalize the algorithm as follows:

- 1. Let us denote the input array as *a[0..m, 0..n]*, i.e., it has m rows and n columns. Let *aᵢ* denote the *iᵗʰ* row of this array.
- 2. Let us denote $i^{th}$ row of the prefix array as $prefixa_i$, which stands for $a_1 + a_2 ... a_i$.
- 3. Please note that $prefixa_i = prefixa_{i-1} + a_i$, where $i \in 1..m$. As described earlier, the computation of prefix array requires $mn$ additions. Hence
  $a_i = prefixa_i - prefixa_{i-1}$
- 4. It is easy to see that the sum over the rows $l$ and $k$, i.e. $a[l..k]$ can be computed as $a_l + a_{l+1} + \cdots + a_{k-1} + a_k =$
  $prefixa_l - prefixa_{l-1} +$
  $prefixa_{l+1} - prefixa_l +$
  $\vdots$
  $prefixa_{k-1} - prefixa_{k-2} +$
  $prefixa_k - prefixa_{k-1} =$
  $prefixa_k - prefixa_{l-1}$
  These consist of $m(m+1)/2$ pairs.
- 5. Kadane's 1D algorithm is applied on $prefixa_k - prefixa_{l-1}$ for each interval $[l,k]$ to find the maximum sum. Thus overall time complexity is $O(m^2 n)$.

We leave the coding exercise in C++ to the reader.

### K-Maximum Sub-array problem

### Problem

Design and implement an efficient program to find the $K$ subarrays with largest sums. Please note that the maximum subarray problem for a one- or two-dimensional array is to find the array portion that maximizes the sum of array elements in it.

Let us revisit our prefix array concept as $a[l..k] = prefixa[k] - prefixa[l - 1]$. To find the maximum sub-array $a[l..k]$, we have to find the indices $l$ and $k$ which maximizes sum of the entries $a[l..k]$. Let us denote $minprefixa[i]$ as a minimum prefix array for the sub-array $a[0..i - 1]$. $max(a[l..k]) = max(prefixa[k] - prefixa[l - 1]) = max(prefixa[k] - minprefixa[k])$. So to compute the maximum sub-array all we need to do is to accumulate the prefix sums along with maintaining minimum of the preceding prefix sums which could be subtracted from the accumulated prefix sums to get the maximum sum so far.

### Algorithm 65 Maximum sub-array sum using prefix array

```text
1: function MAXSUBARRAY(a[0..n − 1])
2:     minprefixsum ← 0
3:     currmaxsum ← 0
4:     prefix[0] ← 0
5:     for i ← 0, n − 1 do
6:         prefix[i] ← prefix[i − 1] + a[i]
7:         cand ← prefix[i] − minprefixsum
8:         currmaxsum ← max(currmaxsum, cand)
9:         minprefixsum ← min(minprefixsum, prefix[i])
10:    end for
11:    return max_so_far
12: end function
```

Based on the above algorithm, we can easily extend it to find K-maximum subarray in one dimensional case. Instead of having a single variable that safeguards the minimum prefix sum, we maintain a list of K minimum prefix sums, sorted in non-decreasing order. The merged list of two sorted sequences x and y are denoted by merge(x, y).

### Algorithm 66 K-Maximum sub-array sum using prefix array

```text
1: function KMAXSUBARRAY(a[0..n − 1])
2:     for k ← 1, K do
3:         min[k] ← −∞
4:         M[k] ← −∞
5:     end for
6:     sum[0] ← 0
7:     min[1] ← 0
8:     M[1] ← 0
9:     for i ← 1, n do
10:        sum[i] ← sum[i − 1] + a[i]
11:        for k ← 1, K do
12:            cand[k] ← sum[i] − min[k]
13:        end for
14:        M ← K largest elements of merge(M, cand)
15:        insert sum[i] into min
16:    end for
17: end function
```

As we need to perform n iterations, the total time complexity is O(Kn). When K = 1, result is comparable to O(n) time of Kadane’s algorithm and prefix array.

## Chapter 5: Graphs

### 5.1 Reliable distribution

### Problem

A communication network consists of a set $V$ of nodes and a set $E \subset V \times V$ of directed edges (communication links). Each edge $e \in E$ has a weight $w(e) \geq 0$ representing the cost of using $e$. A distribution from a given source $s \in V$ is a set of directed $|V|-1$ paths from $s$ to each of the other $|V|-1$ vertices in $V-\{s\}$. The cost of a distribution is the sum of the weights of its constituent paths. (Thus, some edges may be counted more than once in the cost of the distribution.)

- 1. Give an efficient algorithm to determine the cheapest distribution from a given source $s \in V$. You may assume all nodes $V$ are reachable from $s$.
- 2. One of the edges in the communication network may fail, but we don't know which one. Give an efficient algorithm to determine the maximum amount by which the cost of the cheapest distribution from $s$ might increase if an adversary removes an edge from $E$. (The cost is infinite if the adversary can make a vertex unreachable from $s$.)

### Solution

- 1. This problem can be modeled as a single-source shortest paths problem. A distribution is a tree of paths from $s$ to every other vertex in the graph. Since the cost of a distribution is the sum of the lengths of its paths, a minimum cost distribution is a set of shortest paths. Since the edge weights are non-negative, we can use Dijkstra's algorithm. The running time of Dijkstra's algorithm can be improved from $O(|V|^2)$ to $O((|V|+|E|)\log |V|)$ using a binary heap.

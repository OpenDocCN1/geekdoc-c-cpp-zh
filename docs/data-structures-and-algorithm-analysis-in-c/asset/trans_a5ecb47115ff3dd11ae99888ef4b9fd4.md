

![](img/e449061a0cac9cafaefd979fab665b33_376_0.png)

![](img/e449061a0cac9cafaefd979fab665b33_376_1.png)

the size of its tree. Thus, initially the array representation of the tree is all -1s. When a union is performed, check the sizes; the new size is the sum of the old. Thus, union-by-size is not at all difficult to implement and requires no extra space. It is also fast, on average. For virtually all reasonable models, it has been shown that a sequence of M operations requires O(M) average time if union-by-size is used. This is because when random unions are performed, generally very small (usually one-element) sets are merged with large sets throughout the algorithm.

An alternative implementation, which also guarantees that all the trees will have depth at most O(log N), is union-by-height. We keep track of the height, instead of the size, of each tree and perform unions by making the shallow tree a subtree of the deeper tree. This is an easy algorithm, since the height of a tree increases only when two equally deep trees are joined (and then the height goes up by one). Thus, union-by-height is a trivial modification of union-by-size. Since heights of zero would not be negative, we actually store the negative of height, minus an additional 1. Initially, all entries are -1.

![](img/e449061a0cac9cafaefd979fab665b33_377_0.png)

| -1 | -1 | -1 | 4 | -5 | 4 | 4 | 6 |
|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

| -1 | -1 | -1 | 4 | -3 | 4 | 4 | 6 |
|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

Figure 8.13 Forest with implicit representation for union-by-size and union-by-height

```
/**
 * Union two disjoint sets.
 * For simplicity, we assume root1 and root2 are distinct
 * and represent set names.
 * root1 is the root of set 1.
 * root2 is the root of set 2.
 */
void DisjSets::unionSets( int root1, int root2 )
{
    if( s[ root2 ] < s[ root1 ] )  // root2 is deeper
        s[ root1 ] = root2;        // Make root2 new root
    else
    {
        if( s[ root1 ] == s[ root2 ] )
            --s[ root1 ];          // Update height if same
        s[ root2 ] = root1;        // Make root1 new root
    }
}
```

Figure 8.14 Code for union-by-height (rank)

## 8.5 Path Compression

The union/find algorithm, as described so far, is quite acceptable for most cases. It is very simple and linear on average for a sequence of M instructions (under all models). However, the worst case of O(M log N) can occur fairly easily and naturally. For instance, if we put all the sets on a queue and repeatedly dequeue the first two sets and enqueue the union, the worst case occurs. If there are many more finds than unions, this running time is worse than that of the quick-find algorithm. Moreover, it should be clear that there are probably no more improvements possible for the union algorithm. This is based on the observation that any method to perform the unions will yield the same worst-case trees, since it must break ties arbitrarily. Therefore, the only way to speed the algorithm up, without reworking the data structure entirely, is to do something clever on the find operation.

The clever operation is known as path compression. Path compression is performed during a find operation and is independent of the strategy used to perform unions. Suppose the operation is find(x). Then the effect of path compression is that every node on the path from x to the root has its parent changed to the root. Figure 8.15 shows the effect of path compression after find(14) on the generic worst tree of Figure 8.12.

The effect of path compression is that with an extra two link changes, nodes 12 and 13 are now one position closer to the root and nodes 14 and 15 are now two positions closer. Thus, the last future accesses on these nodes will pay (we hope) for the extra work to do the path compression.

As the code in Figure 8.16 shows, path compression is a trivial change to the basic find algorithm. The only change to the find routine (besides the fact that it is no longer a const member function) is that s[x] is made equal to the value returned by find; thus, after the root of the set is found recursively, x's parent link references it. This occurs recursively to every node on the path to the root, so this implements path compression.

When unions are done arbitrarily, path compression is a good idea, because there is an absence of deep nodes and these are brought near the root by path compression. It has been proven that when path compression is done in this case, a sequence of M

![](img/e449061a0cac9cafaefd979fab665b33_378_0.png)

Figure 8.15 An example of path compression

```
1 /**
2  * Perform a find with path compression.
3  * Error checks omitted again for simplicity.
4  * Return the set containing x.
5  */
6
7 int DisjSets::find( int x )
8 {
9   if( s[ x ] < 0 )
10    return x;
11  else
12    return s[ x ] = find( s[ x ] );
13 }
```

Figure 8.16 Code for disjoint sets find with path compression

operations requires at most O(M log N) time. It is still an open problem to determine what the average-case behavior is in this situation.

Path compression is perfectly compatible with union-by-size, and thus both routines can be implemented at the same time. Since doing union-by-size by itself is expected to execute a sequence of M operations in linear time, it is not clear that the extra pass involved in path compression is worthwhile on average. Indeed, this problem is still open. However, as we shall see later, the combination of path compression and a smart union rule guarantees a very efficient algorithm in all cases.

Path compression is not entirely compatible with union-by-height, because path compression can change the heights of the trees. It is not at all clear how to recompute them efficiently. The answer is do not! Then the heights stored for each tree become estimated heights (sometimes known as ranks), but it turns out that union-by-rank (which is what this has now become) is just as efficient in theory as union-by-size. Furthermore, heights are updated less often than sizes. As with union-by-size, it is not clear whether path compression is worthwhile on average. What we will show in the next section is that with either union heuristic, path compression significantly reduces the worst-case running time.

## 8.6 Worst Case for Union-by-Rank and Path Compression

When both heuristics are used, the algorithm is almost linear in the worst case. Specifically, the time required in the worst case is Θ(Mα(M, N)) (provided M ≥ N), where α(M, N) is an incredibly slowly growing function that for all intents and purposes is at most 5 for any problem instance. However, α(M, N) is not a constant, so the running time is not linear.

In the remainder of this section, we first look at some very slow-growing functions, and then in Sections 8.6.2 to 8.6.4, we establish a bound on the worst case for a sequence of at most N - 1 unions and M find operations in an N-element universe in which union is by rank and finds use path compression. The same bound holds if union-by-rank is replaced with union-by-size.

### 8.6.1 Slowly Growing Functions

Consider the recurrence

```
T(N) = \begin{cases} 0 & N \le 1 \\ T(f(N)) + 1 & N > 1 \end{cases} (8.1)
```

In this equation, T(N) represents the number of times, starting at N, that we must iteratively apply f(N) until we reach 1 (or less). We assume that f(N) is a nicely defined function that reduces N. Call the solution to the equation f*(N).

We have already encountered this recurrence when analyzing binary search. There, f(N) = N/2; each step halves N. We know that this can happen at most log N times until N reaches 1; hence we have f*(N) = log N (we ignore low-order terms, etc.). Observe that in this case, f*(N) is much less than f(N).

Figure 8.17 shows the solution for T(N) for various f(N). In our case, we are most interested in f(N) = log N. The solution T(N) = log* N is known as the iterated logarithm. The iterated logarithm, which represents the number of times the logarithm needs to be iteratively applied until we reach one, is a very slowly growing function. Observe that log* 2 = 1, log* 4 = 2, log* 16 = 3, log* 65536 = 4, and log* 2^65536 = 5. But keep in mind that 2^65536 is a 20,000-digit number. So while log* N is a growing function, for all intents and purposes, it is at most 5. But we can still produce even more slowly growing functions. For instance, if f(N) = log* N, then T(N) = log** N. In fact, we can add stars at will to produce functions that grow slower and slower.

| f(N) | f*(N) |
|---|---|
| N-1 | N-1 |
| N-2 | N/2 |
| N-c | N/c |
| N/2 | log N |
| N/c | log_c N |
| \sqrt{N} | log log N |
| log N | log* N |
| log* N | log** N |
| log** N | log*** N |

Figure 8.17 Different values of the iterated function

### 8.6.2 An Analysis by Recursive Decomposition

We now establish a tight bound on the running time of a sequence of M = \Omega(N) union/find operations. The unions and finds may occur in any order, but unions are done by rank and finds are done with path compression.



| | Left=1 | Left=2 | Left=3 | Left=4 | Left=5 | Left=6 | Left=7 |
|---|---|---|---|---|---|---|---|
| Iteration=1 | a.a .22 | am.am .18 | and.and .20 | egg.egg .05 | if.if .25 | the.the .02 | two.two .08 |
| Iteration=2 | .am .58 | am.and .56 | and.egg .30 | egg.if .35 | if.the .19 | the.two .12 | |
| Iteration=3 | .and .102 | am.egg .66 | and.if .80 | egg.the .39 | if.two .47 | | |
| Iteration=4 | a.egg 1.17 | am.if 1.21 | and.the .84 | egg.two .57 | | | |
| Iteration=5 | a.if 1.83 | am.the 1.27 | and.two 1.02 | | | | |
| Iteration=6 | a.the 1.89 | am.two 1.53 | | | | | |
| Iteration=7 | a.two 2.15 | | | | | | |

Figure 10.51 Computation of the optimal binary search tree for sample input

Figure 10.51 shows the table that will be produced by the algorithm. For each subrange of words, the cost and root of the optimal binary search tree are maintained. The bottommost entry computes the optimal binary search tree for the entire set of words in the input. The optimal tree is the third tree shown in Figure 10.48.

The precise computation for the optimal binary search tree for a particular subrange, namely, am, if, is shown in Figure 10.52. It is obtained by computing the minimum-cost tree obtained by placing am, and, egg, and if at the root. For instance, when and is placed at the root, the left subtree contains am, am (of cost 0.18, via previous calculation), the right subtree contains egg, if (of cost 0.35), and p_am + p_and + p_egg + p_if = 0.68, for a total cost of 1.21.

The running time of this algorithm is O(n^3), because when it is implemented, we obtain a triple loop. An O(n^2) algorithm for the problem is sketched in the exercises.

## 10.3.4 All-Pairs Shortest Path

Our third and final dynamic programming application is an algorithm to compute shortest weighted paths between every pair of points in a directed graph, G = (V, E). In Chapter 9, we saw an algorithm for the single-source shortest-path problem, which finds the shortest path from some arbitrary vertex, s, to all others. That algorithm (Dijkstra's) runs in O(|V|^2) time on dense graphs, but substantially faster on sparse graphs. We will give a short algorithm to solve the all-pairs problem for dense graphs. The running time of the algorithm is O(|V|^3), which is not an asymptotic improvement over |V| iterations of Dijkstra's algorithm but could be faster on a very dense graph, because its loops are tighter. The algorithm also performs correctly if there are negative edge costs but no negative-cost cycles; Dijkstra's algorithm fails in this case.

![](img/e449061a0cac9cafaefd979fab665b33_510_0.png)

Figure 10.52 Computation of table entry (1.21, and for am..if

Let us recall the important details of Dijkstra's algorithm (the reader may wish to review Section 9.3). Dijkstra's algorithm starts at a vertex, s, and works in stages. Each vertex in the graph is eventually selected as an intermediate vertex. If the current selected vertex is v, then for each w ∈ V, we set dw = min(dw, dv + cv,w). This formula says that the best distance to w (from s) is either the previously known distance to w from s, or the result of going from s to v (optimally) and then directly from v to w.

Dijkstra's algorithm provides the idea for the dynamic programming algorithm: We select the vertices in sequential order. We will define Dk,i,j to be the weight of the shortest path from vi to vj that uses only v1, v2, ..., vk as intermediates. By this definition, D0,i,j = ci,j, where ci,j is ∞ if (vi, vj) is not an edge in the graph. Also, by definition, D|V|,i,j is the shortest path from vi to vj in the graph.

As Figure 10.53 shows, when k > 0 we can write a simple formula for Dk,i,j. The shortest path from vi to vj that uses only v1, v2, ..., vk as intermediates is the shortest path that either does not use vk as an intermediate at all, or consists of the merging of the two paths vi → vk and vk → vj, each of which uses only the first k − 1 vertices as intermediates. This leads to the formula

```
D_{k,i,j} = \min\{D_{k-1,i,j}, D_{k-1,i,k} + D_{k-1,k,j}\}
```

The time requirement is once again O(|V|^3). Unlike the two previous dynamic programming examples, this time bound has not been substantially lowered by another approach.

/**
 * Compute all-shortest paths.
 * a contains the adjacency matrix with
 * a[ i ][ i ] presumed to be zero.
 * d contains the values of the shortest path.
 * Vertices are numbered starting at 0; all arrays
 * have equal dimension. A negative cycle exists if
 * d [ i ][ i ] is set to a negative value.
 * Actual path can be computed using path [ ][ ].
 * NOT_A_VERTEX is -1
 */
void allPairs( const matrix< int > & a, matrix< int > & d, matrix< int > & path )
{
    int n = a.numrows( );

    // Initialize d and path
    for( int i = 0; i < n; ++i )
        for( int j = 0; j < n; ++j )
        {
            d[ i ][ j ] = a[ i ][ j ];
            path[ i ][ j ] = NOT_A_VERTEX;
        }

    for( int k = 0; k < n; ++k )
        // Consider each vertex as an intermediate
        for( int i = 0; i < n; ++i )
            for( int j = 0; j < n; ++j )
                if( d[ i ][ k ] + d[ k ][ j ] < d[ i ][ j ] )
                {
                    d[ i ][ j ] = d[ i ][ k ] + d[ k ][ j ];
                    path[ i ][ j ] = k;
                }
}

Figure 10.53 All-pairs shortest path

Because the kth stage depends only on the (k - 1)th stage, it appears that only two |V| × |V| matrices need to be maintained. However, using k as an intermediate vertex on a path that starts or finishes with k does not improve the result unless there is a negative cycle. Thus, only one matrix is necessary, because D_{k-1,j,k} = D_{k,j,k} and D_{k-1,k,j} = D_{k,k,j}, which implies that none of the terms on the right change values and need to be saved. This observation leads to the simple program in Figure 10.53, which numbers vertices starting at zero to conform with C++'s conventions.

On a complete graph, where every pair of vertices is connected (in both directions), this algorithm is almost certain to be faster than |V| iterations of Dijkstra's algorithm, because the loops are so tight. Lines 17 to 21 can be executed in parallel, as can lines 26 to 33. Thus, this algorithm seems to be well suited for parallel computation.

Dynamic programming is a powerful algorithm design technique, which provides a starting point for a solution. It is essentially the divide-and-conquer paradigm of solving simpler problems first, with the important difference being that the simpler problems are not a clear division of the original. Because subproblems are repeatedly solved, it is important to record their solutions in a table rather than recompute them. In some cases, the solution can be improved (although it is certainly not always obvious and frequently difficult), and in other cases, the dynamic programming technique is the best approach known.

In some sense, if you have seen one dynamic programming problem, you have seen them all. More examples of dynamic programming can be found in the exercises and references.

## 10.4 Randomized Algorithms

Suppose you are a professor who is giving weekly programming assignments. You want to make sure that the students are doing their own programs or, at the very least, understand the code they are submitting. One solution is to give a quiz on the day that each program is due. On the other hand, these quizzes take time out of class, so it might only be practical to do this for roughly half of the programs. Your problem is to decide when to give the quizzes.

Of course, if the quizzes are announced in advance, that could be interpreted as an implicit license to cheat for the 50 percent of the programs that will not get a quiz. One could adopt the unannounced strategy of giving quizzes on alternate programs, but students would figure out the strategy before too long. Another possibility is to give quizzes on what seem like the important programs, but this would likely lead to similar quiz patterns from semester to semester. Student grapevines being what they are, this strategy would probably be worthless after a semester.

One method that seems to eliminate these problems is to use a coin. A quiz is made for every program (making quizzes is not nearly as time-consuming as grading them), and at the start of class, the professor will flip a coin to decide whether the quiz is to be given. This way, it is impossible to know before class whether or not the quiz will occur, and these patterns do not repeat from semester to semester. Thus, the students will have to expect that a quiz will occur with 50 percent probability, regardless of previous quiz patterns. The disadvantage is that it is possible that there is no quiz for an entire semester. This is not a likely occurrence, unless the coin is suspect. Each semester, the expected number of quizzes is half the number of programs, and with high probability, the number of quizzes will not deviate much from this.

This example illustrates what we call randomized algorithms. At least once during the algorithm, a random number is used to make a decision. The running time of the algorithm depends not only on the particular input, but also on the random numbers that occur.

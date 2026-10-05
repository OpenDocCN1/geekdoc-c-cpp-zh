
## 16.2 Randomized Algorithms

```cpp
// Floyd's all-pairs shortest paths algorithm
// Store the pair-wise distances in "D"
void Floyd(Graph* G) {
    for (int i=0; i<G->n(); i++) // Initialize D with weights
        for (int j=0; j<G->n(); j++)
            if (G->weight(i, j) < D[i][j]) D[i][j] = G->weight(i, j);
    for (int k=0; k<G->n(); k++) // Compute all k paths
        for (int i=0; i<G->n(); i++)
            for (int j=0; j<G->n(); j++)
                if (D[i][j] > D[i][k] + D[k][j])
                    D[i][j] = D[i][k] + D[k][j];
}
```

Clearly this algorithm requires $\Theta(|V|^3)$ running time, and it is the best choice for dense graphs because it is (relatively) fast and easy to implement.

In this section, we will consider how introducing randomness into our algorithms might speed up, although at the expense of accuracy. But often we can reduce the potential for error to be as low as we like, while still speeding up the algorithm.

### 16.2.1 Randomized algorithms for finding large values

In Section 15.1 we demonstrated that the lower cost of finding the maximum value in an unsorted list is $\Omega(n)$. This is the least time needed to be certain that we have found the maximum value. But what if we are willing to relax our requirement for certainty? The first question is: What do we mean by this? There are many aspects to "certainty" and we might relax the requirement in various ways.

There are several possible guarantees that we might require from an algorithm that produces $X$ as the maximum value, the true maximum is $Y$. So far we have assumed that we require $X = Y$. This is known as an exact or deterministic algorithm to solve the problem. We could relax this and require only $X$'s rank is "close" to $Y$'s rank (within a fixed distance or percentage). This is known as an approximation algorithm. We could require that $X$ is "usually" $Y$. This is known as a probabilistic algorithm. Finally, we could require only that $X$'s rank is "usually" "close" to $Y$'s rank. This is known as a heuristic algorithm.

There are also different ways that we might choose to sacrifice reliability for speed. These types of algorithms also have names.

- 1. **Las Vegas Algorithms:** We always find the maximum value, and "usually" find it fast. Such algorithms have a guaranteed result, but do not guarantee fast running time.
- 2. **Monte Carlo Algorithms:** Find the maximum value fast, or we don't get an answer at all (but fast). While such algorithms have good running time, result is not guaranteed.

Here is an example of an algorithm for finding a large value that gives up guarantee of getting the best value in exchange for an improved running time. This is an example of a probabilistic algorithm, since it includes steps that are affected by random events. Choose $m$ elements at random, and pick the best one of those as the answer. For large $n$, if $m \approx \log n$, the answer is pretty good. The cost is $m-1$ compares (since we must find the maximum of $m$ values). But we don't know for sure what we get. However, we can estimate that the rank will be about $n/m$. For example, if $n=1,000$ and $m=\log n=20$, then we expect that of the 20 randomly selected values be among the top 5% of the $n$ values.

Next, a slightly different problem where the goal is to pick a number in the upper half of $n$ values. We would pick the maximum from among the first $n+1$ for a cost of $n/2$ comparisons. Can we do better than this? If we are willing to want guarantee the correct answer. But if we are willing to accept near certainty of absolute certainty, we can gain a lot in terms of speed.

As an alternative, consider this probabilistic algorithm. Pick 2 numbers and choose the greater. This will be in the upper half with probability 3/4 (since it is not in the upper half when both numbers choose it is chosen to be in the lower half). A probability of 3/4 is not good enough? Then we pick more numbers! For $k$ numbers, the greatest is in upper half with probability $1-1/2$, regardless of number $n$ that we pick from, so long as $n$ is much larger than $k$ (otherwise the changes might become even better). If we pick ten numbers, then the chance of failure is only one in $2^{10}=1024$. What if we really wanted to be sure, because $l$ depends on drawing a number from the upper half? If we pick 30 numbers, we can fail only one time in a billion. If we pick enough numbers, then the chance of picking a small number is less than the chance of the power failing during the computation. Picking 100 numbers means that we can fail only one time in $10^{100}$ which is less than any disaster that we can imagine the process.

### 16.2.2 Skip Lists

This section presents a probabilistic search structure called the Skip List. Like BSTs, Skip Lists are designed to overcome a basic limitation of array-based and linked lists: search or update operations require time. The Skip List is an example of a probabilistic data structure, because it makes some of its decisions at random.

Skip Lists provide an alternative to the BST and related tree structures. The primary problem with the BST is that it may easily become unbalanced. The 2-3 tree of Chapter 10 is guaranteed to remain balanced regardless of the order in which data values are inserted, but it is rather complicated to implement. Chapter 13 presents the AVL tree and the splay tree, which are also guaranteed to provide good performance, but at the cost of added complexity compared to the BST. The Skip List is easier to implement than known balanced tree structures. The Skip List is not guaranteed to provide good performance (where good performance is defined as $\Theta(\log n)$ search, insertion, and deletion time), but it will provide good performance with extremely high probability (the BST has a good chance of performing poorly). As it represents a good compromise between difficulty of implementation and performance.

Figure 16.2 illustrates the concept behind the Skip List. Figure 16.2(a) shows a simple linked list whose nodes are ordered by key. To search a sorted list requires more than one value, visiting $\Theta(n)$ nodes in the average case. What if we add a pointer to every other node that lets us skip nodes, as shown in Figure 16.2(b)? Define nodes with single pointer as 0 Skip List nodes, and nodes with two pointers as 1 Skip List nodes. To search, follow the level 1 pointers until a value greater than the search has been found, go back to the previous level 1 node, then revert to the level 0 pointer to travel one more. This effectively cuts the work in half. We can continue adding pointers to selected nodes in this way — give a pointer to every fourth node, a fourth pointer to every eighth node, and so on — until we reach the limit of $\log n$ pointers as illustrated in Figure 16.2(c). To search, start with the bottom-most row of pointers, going as far as possible and skipping many nodes at a time. Then, shift up to shorter and shorter steps as required. With this arrangement, the worst-case number of accesses is $\Theta(\log n)$.

We will store each Skip List an array forward that stores the pointers as shown in Figure 16.2(c). Position forward[0] stores a level 0 pointer, and so on. The Skip object includes data member level that stores the highest level for any node in the Skip List. The Skip List stores a header node head with level pointers. The find function is shown in Figure 16.3.

Searching for a node with value 62 in the Skip List of Figure 16.2(c) begins at the header node. Follow the header node's pointer at level, which in this example is 2. This points to the node with value 31. Because 31 is less than 62, we try the next pointer for forward[2] of 31's node to reach 69. Because 69 is greater than 62, we cannot go forward but instead decrement the current level counter to 1. We try to follow forward[1] of 31 to reach the node with value 58. Because 58 is smaller than 62, we follow 58's forward{1} pointer to 69. Because 69 is too big, follow 58's level 0 pointer to 62. Because 62 is not less than 62, we fall out of the while loop and move one step forward to the node with value 62.

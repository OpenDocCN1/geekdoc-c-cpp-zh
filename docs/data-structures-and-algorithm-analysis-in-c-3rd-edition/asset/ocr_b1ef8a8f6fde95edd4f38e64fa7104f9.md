```
// Floyd’s all-pairs shortest paths algorithm
// Store the pair-wise distances in "D"
void Floyd(Graph* G) {
    for (int i=0; i<G->n(); i++) // Initialize D with weights
        for (int j=0; j<G->n(); j++)
            if (G->weight(i, j) != 0) D[i][j] = G->weight(i, j);
    for (int k=0; k<G->n(); k++) // Compute all k paths
        for (int i=0; i<G->n(); i++)
            for (int j=0; j<G->n(); j++)
                if (D[i][j] > (D[i][k] + D[k][j]))
                    D[i][j] = D[i][k] + D[k][j];
}
```

Clearly this algorithm requires Θ(|V|³) running time, and it is the best choice for dense graphs because it is (relatively) fast and easy to implement.

# 16.2 Randomized Algorithms

In this section, we will consider how introducing randomness into our algorithms might speed things up, although perhaps at the expense of accuracy. But often we can reduce the possibility for error to be as low as we like, while still speeding up the algorithm.

# 16.2.1 Randomized algorithms for finding large values

In Section 15.1 we determined that the lower bound cost of finding the maximum value in an unsorted list is Ω(n). This is the least time needed to be certain that we have found the maximum value. But what if we are willing to relax our requirement for certainty? The first question is: What do we mean by this? There are many aspects to “certainty” and we might relax the requirement in various ways.

There are several possible guarantees that we might require from an algorithm that produces X as the maximum value, when the true maximum is Y. So far we have assumed that we require X to equal Y. This is known as an exact or deterministic algorithm to solve the problem. We could relax this and require only that X’s rank is “close to” Y’s rank (perhaps within a fixed distance or percentage). This is known as an approximation algorithm. We could require that X is “usually” Y. This is known as a probabilistic algorithm. Finally, we could require only that X’s rank is “usually” “close” to Y’s rank. This is known as a heuristic algorithm.

There are also different ways that we might choose to sacrifice reliability for speed. These types of algorithms also have names.

+   1. Las Vegas Algorithms: We always find the maximum value, and “usually” we find it fast. Such algorithms have a guaranteed result, but do not guarantee fast running time.
nearest cluster center, providing the best solution. The current population is evaluated, and each individual has a new fitness value, updated using the SSE criterion. The fitness function is defined as the inverse of the SSE metric. A new population is selected and replaces the previous one.

The pseudocode of CGA_SSE is as follows:

```
CGA_SSE Input: X, set of N patterns with d dimensions;
K: number of centroids; Tp: population size;
Pc: crossover rate; Pm: mutation rate;
Ng: maximum number of generations;

Output: Best solution found S*
//the initialization
t=0, Set the initial population P(t) with size Tp, Evaluate P(t)
S = select_best_individual(P(t)), S* = S
SSE = SSE computed with the solution S*
Pp = ∅
//the main part
while (t < Ng ) {
t= t +1 //for next population
select Pp(t) from P(t-1) with crossover rate Pc
P(t) = crossover Pp(t)
apply mutation P(t) with mutation rate Pm
//Local Search
for all Ii ∈P(t)
{ apply K-Means, - LocalSearch(Ii),
calculate cluster centers.
reassign each data point to the nearest cluster center}
//GA steps
evaluate P(t)
S' = select_best_individual (P(t))
S' SSE = SSE computed with the solution S', -fitness function
find the minimum S' SSE (S*)
from minimum S' SSE define the set of clusters (the best
solution, S*).
}//end while
return S*
```

The process is repeated until there is no change in k cluster centers. This can be achieved by minimizing the objective function of SSE. Hence, the minimum SSE defines an optimum set of clusters. The time complexity of GCA_SSE is O(t_m * p * n * k * d) where t_m = maximum number of iterations, p = population size, n = number of points, k = number of clusters, and d = dimension of data. The GA with the selection and mutation operations may take time to converge because the initial assignments are arbitrary. For improvement purposes, a K-means algorithm is used. The K-means calculates cluster centers and
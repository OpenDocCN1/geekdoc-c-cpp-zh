15. A connected component of the undirected graph G with vertices V and edges E is a set of vertices such that any vertex in the component is connected to all other vertices in the same component. Assume an adjacency list representation for G. Write an algorithm to find the number of connected components in G. What is its order (in terms of |V| and |E|)?

16. The following formula is useful in algorithms analysis:

$$\sum_{i=1}^n i=n(n+1)/2$$

Use this, if necessary, to analyze the order of these code fragments:

+   a. for (i = 1; i<n; i++)

   for (j = 1; j < 6; j++)
   if (a[i,j] == 0) ZeroCount++;
   else if (a[i.j] < 0) NegativeCount++;
   else PositiveCount++;

b. for (i = 1; i<5; i++)

   for (j = 1; j < 6; j++)
   if (a[i,j] == 0) ZeroCount++;
   else if (a[i.j] < 0) NegativeCount++;
   else PositiveCount++;

c. for (i = 1; i<n; i++)

   for (j = 1; j < n; j++)
   if (a[i,j] == 0) ZeroCount++;
   else if (a[i.j] < 0) NegativeCount++;
   else PositiveCount++;

d. for (i = 1; i<n; i++)

   for (j = 1; j < i; j++)
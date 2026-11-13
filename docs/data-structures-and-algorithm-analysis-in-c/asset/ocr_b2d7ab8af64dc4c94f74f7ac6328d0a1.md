```
void Graph::topsort( )
{
   Queue<Vertex> q;
   int counter = 0;

   q.makeEmpty( );
   for each Vertex v
      if ( v.indegree == 0 )
         q.enqueue( v );

   while ( !q.isEmpty( ) )
   {
      Vertex v = q.dequeue( );
      v.topnum = ++counter;  // Assign next number

      for each Vertex w adjacent to v
         if ( --w.indegree == 0 )
            q.enqueue( w );
   }

   if( counter != NUM_VERTICES )
      throw CycleFoundException( );
}
```

# Figure 9.7 Pseudocode to perform topological sort

A pseudocode implementation of this algorithm is given in Figure 9.7. As before, we will assume that the graph is already read into an adjacency list and that the indegrees are computed and stored with the vertices. We also assume each vertex has a named data member, topnum, in which to place its topological numbering.

The time to perform this algorithm is O(|E| + |V|) if adjacency lists are used. This is apparent when one realizes that the body of the for loop is executed at most once per edge. Computing the indegrees can be done with the following code; this same logic shows that the cost of this computation is O(|E| + |V|), even though there are nested loops.

```
for each Vertex v
   v.indegree = 0;

for each Vertex v
   for each Vertex w adjacent to v
      w.indegree++;
```

The queue operations are done at most once per vertex, and the other initialization steps, including the computation of indegrees, also take time proportional to the size of the graph.
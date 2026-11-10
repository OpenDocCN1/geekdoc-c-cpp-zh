![](bbox=[0.143, 0.109, 0.856, 0.291])

**Figure 6.7**  
Vertex array and corresponding index array.

two triangles forming a square region above and to its right, as shown earlier in Figure 6.3. The processing is thus organized into nested loops, as follows:

```
for each horizontal slice i in the sphere (i ranges from 0 through all the slices in the sphere)
{
    for each vertex j in slice i (j ranges from 0 through all the vertices in the slice)
    {
        calculate indices for two triangles which point to neighboring vertices to the right,
        above, and to the above-right of vertex j
    }
}
```

For example, consider the “red” vertex from Figure 6.3 (repeated in Figure 6.8). The vertex in question is at the lower left of the yellow triangles shown in Figure 6.8, and given the loops just described, would be indexed by i*n+j, where i is the slice currently being processed (the outer loop), j is the vertex currently being processed within that slice (the inner loop), and n is the number of vertices per slice. Figure 6.8 shows this vertex (in red) along with its three relevant neighboring vertices, each with formulas showing how they would be indexed.

These four vertices are then used to build the two triangles (shown in yellow) generated for this (red) vertex. The six entries in the index table for these two triangles are indicated in the figure in the order shown by the numbers 1 through 6. Note that entries 3 and 6 both refer to the same vertex, which is also the case for entries 2

![](bbox=[0.513, 0.693, 0.861, 0.861])

**Figure 6.8**  
Indices generated for the jth vertex in the ith slice (n = number of vertices per slice).
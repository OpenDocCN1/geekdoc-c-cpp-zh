![](bbox=[0.225, 0.115, 0.905, 0.305])

Figure 5.12. Topological states of a quad cell (marching squares algorithm). Red indicates “inside” vertices. Bold indices mark ambiguous cases.

table (see Figure 5.12) that holds optimized code for every topological state. Optimizations include performing the edge-isovalue intersection computations (see Equation (5.5)) only on those edges that are known to be intersected for a specific topological state. The states 0101 and 1010 in the case table represent the ambiguous situations described previously for the example in Figure 5.11. That is, the method implementation can choose whether to create the full lines or the dashed ones.

Putting it all together, we obtain the marching squares implementation shown in Listing 5.2.

The marching squares algorithm constructs independent line segments for each cell, which are stored in an unstructured dataset type, given that isolines have no regular structure with respect to the grid they are computed on. An useful postprocessing step is to merge the coincident end points of line segments originating from neighbor grid cells that share an edge. Besides decreasing the

```
for each cell ci of the dataset
{
    int index = 0;
    for (each vertex vj of ci)
        store the inside/outside state of vj in bit j of index;
    select the optimized code from the case table using index;
    for (all edges ej of the selected case)
        intersect ej with isovalue v using Equation “(5.3);
    construct line segments from these intersections;
}
```

Listing 5.2. Marching squares pseudocode.
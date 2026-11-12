# FIGURE 20-26 Checking weight[u] by examining the graph: (a) weight[2] in step 2; (b) weight[1] in step 3; (c) weight[3] in step 3; (d) weight[3] in step 4

![](bbox=[0.25, 0.15, 0.6, 0.72])

Step 2. The path 0-4-2 is shorter than 0-2

Step 3. The path 0-4-2-1 is shorter than 0-1

Step 3 continued. The path 0-4-2-3 is shorter than 0-3

Step 4. The path 0-4-2-3 is shorter than 0-4-2-1-3

include vertex 4 in the path. However, for vertex 2 notice that weight[2] = ∞ > weight[4] + matrix[4][2] = 4 + 1 = 5. Therefore, replace weight[2] with 5. You can also verify this conclusion by examining the graph directly, as Figure 20-26a shows. Step 3. weight[2] = 5 is the smallest value in weight, ignoring weight[0] and weight[4] because 0 and 4 are in vertexSet. Thus, v = 2, so add 2 to vertexSet. For vertices not in vertexSet—that is, for u = 1 and 3—check whether it is shorter to go from 0 to 2 and then along an edge to u instead of directly from 0 to u along an edge. (See Figures 20-26b and 20-26c.)
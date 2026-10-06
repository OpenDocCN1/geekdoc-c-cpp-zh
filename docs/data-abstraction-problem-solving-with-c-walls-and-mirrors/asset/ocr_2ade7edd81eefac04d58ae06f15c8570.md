# FIGURE 20-26 Checking weight[u] by examining the graph: (a) weight[2] in step 2;
(b) weight[1] in step 3; (c) weight[3] in step 3; (d) weight[3] in step 4

![](bbox=[0.286, 0.155, 0.856, 0.706])

include vertex 4 in the path. However, for vertex 2 notice that weight[2] = ∞ > weight[4]
matrix[4][2] = 4 + 1 = 5. Therefore, replace weight[2] with 5. You can also see that
conclusion by examining the graph directly, as Figure 20-26a.
Step 3. weight[2] = 5 is the smallest value in weight, ignoring weight[0] and weight[4] because
0 and 4 are in vertexSet. Thus, v = 2, add 2 to vertexSet. For vertices not in vertex-Set—that is, for u = 1 and 3—check whether it is shorter to go from 0 to 2 and then
al along an edge u instead of directly from 0 to u along an edge. (See Figures 20-26b
 20-26c.)
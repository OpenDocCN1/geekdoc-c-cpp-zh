+   3. Again, calculate the in-degrees of the remaining nodes, as follows:
+   
+      - V₂ = 2
+      - V₄ = 0
+      - V₅ = 1
+      - V₆ = 2
+   
+      In this case, V₄ has the in-degree 0. Therefore, V₄ and all its outgoing edges {V₄, V₂}, {V₄, V₅} are deleted from the graph. After this process, the resultant graph would be as follows:

![](bbox=[0.369, 0.283, 0.655, 0.409])

+   4. Calculate the in-degrees of the remaining graph nodes, as follows:
+   
+      - V₂ = 1
+      - V₅ = 0
+      - V₆ = 2
+   
+      In this case, V₅ has the in-degree 0. Therefore, V₅ and all its outgoing edges {V₅, V₂}, {V₅, V₆} are deleted from the graph. After this process, the resultant graph would be as follows:

![](bbox=[0.369, 0.513, 0.655, 0.593])

+   5. In this step, the in-degrees of the remaining graph nodes are as follows:
+   
+      - V₂ = 0
+      - V₆ = 1
+   
+      In this case, V₂ has the in-degree 0. Therefore, V₂ and its outgoing edge {V₂, V₆} are deleted from the graph. After this process, the resultant graph will have only one node left, shown as follows:

![](bbox=[0.479, 0.686, 0.545, 0.729])

+   6. In the last step, as the in-degree of V₆ is 0, we delete the node. At the end of this step, the linear ordering of the node would be as follows:
+   
+      {V₁, V₃, V₄, V₅, V₂, V₆}
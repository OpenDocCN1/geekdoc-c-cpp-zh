![](bbox=[0.275, 0.085, 0.845, 0.445])

Figure 9.9 The Santa Fe trail. Each black square represents a pellet of food.

+   1. Decide on the terminal set T. The terminal set contains the actions the ant can take. That is,
+   
+   T = {right, left, move}.

+   2. Decide on the function set F. The function set is as follows:
+   
+   (a) if_food_ahead(instruction1, instruction2);
+   (b) do2(instruction1, instruction2);
+   (c) d03(instruction1, instruction2, instruction3);

The first function executes instruction1 if food_ahead is true; otherwise it executes instruction2. The second function unconditionally executes instruction1 and instruction2. The third function unconditionally executes instruction1, instruction2, and instruction3. For example,

```
do2(right, move)
```

causes the ant to turn right and then move ahead.

+   3. Decide on how many individuals make up a population. The population size is 500.
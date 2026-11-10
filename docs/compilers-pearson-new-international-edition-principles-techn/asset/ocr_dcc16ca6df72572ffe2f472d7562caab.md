At this point, we could apply rule (5) to reduce the subtree

![](bbox=[0.463, 0.201, 0.555, 0.263])

to a single node labeled, say, $R_1$. We could also use rule (6) to reduce the larger subtree

![](bbox=[0.422, 0.309, 0.571, 0.385])

to a single node labeled $R_0$ and generate the instruction `ADD R0, R0, i(SP)`. Assuming that it is more efficient to use a single instruction to compute the larger subtree rather than the smaller one, we choose rule (6) to get

![](bbox=[0.412, 0.459, 0.579, 0.509])

In the right subtree, rule (2) applies to the leaf $M_b$. It generates an instruction to load b into register R1, say. Now, using rule (8) we can match the subtree

![](bbox=[0.455, 0.561, 0.538, 0.598])

and generate the increment instruction `INC R1`. At this point, the input tree has been reduced to

![](bbox=[0.455, 0.647, 0.543, 0.704])

This remaining tree is matched by rule (4), which reduces the tree to a single node and generates the instruction `ST *R0,R1`. We generate the following code sequence:

```
```text
LD   R0, #a
ADD  R0, R0, SP
ADD  R0, R0, i(SP)
LD   R1, b
INC  R1
ST   *R0, R1
```
```
At this point, we could apply rule (5) to reduce the subtree

![](bbox=[0.465, 0.202, 0.555, 0.263])

to a single node labeled, say, `R₁`. We could also use rule (6) to reduce the larger subtree

![](bbox=[0.422, 0.308, 0.579, 0.389])

to a single node labeled `R₀` and generate the instruction `ADD R0, R0, i(SP)`. Assuming that it is more efficient to use a single instruction to compute the larger subtree rather than the smaller one, we choose rule (6) to get

![](bbox=[0.411, 0.454, 0.582, 0.51])

In the right subtree, rule (2) applies to the leaf `M_b`. It generates an instruction to load `b` into register `R₁`, say. Now, using rule (8) we can match the subtree

![](bbox=[0.454, 0.562, 0.544, 0.594])

and generate the increment instruction `INC R1`. At this point, the input tree has been reduced to

![](bbox=[0.452, 0.647, 0.548, 0.7])

This remaining tree is matched by rule (4), which reduces the tree to a single node and generates the instruction `ST *R0, R1`. We generate the following code sequence:

```
LD   R0, #a
ADD  R0, R0, SP
ADD  R0, R0, i(SP)
LD   R1, b
INC  R1
ST   *R0, R1
```
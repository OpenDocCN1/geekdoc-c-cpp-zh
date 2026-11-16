# Step 3: x = info(p)

![](bbox=[0.246, 0.135, 0.845, 0.285])

X = 10

# Step 4: freeNode(p)

![](bbox=[0.246, 0.465, 0.845, 0.535])

X = 10

Put together, we have an algorithm for deleting a node from the front of a linear linked list:

```
p = list
list = next(p)
x = info(p)
freeNode(p)
```
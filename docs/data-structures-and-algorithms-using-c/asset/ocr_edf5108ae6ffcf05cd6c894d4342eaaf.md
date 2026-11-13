# Deletion Operation

Deletion is also a more than one step process. We shall learn with pictorial representation. First, locate the target node to be removed, by using searching algorithms.

![](bbox=[0.05, 0.15, 0.8, 0.21])

(previous) node of the target node now should point to the next node of the target node – LeftNode.next -> TargetNode.next;

![](bbox=[0.05, 0.28, 0.8, 0.36])

This will remove the link that was pointing to the target node. Now, using the following code, we will remove what the target node is pointing at.

```
TargetNode.next -> NULL;
```

![](bbox=[0.05, 0.46, 0.8, 0.52])

the deleted node. We can keep that in memory otherwise we can simply deallocate memory and wipe off the target node completely.

![](bbox=[0.05, 0.6, 0.6, 0.66])
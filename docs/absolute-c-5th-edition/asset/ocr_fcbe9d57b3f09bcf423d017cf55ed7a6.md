# 746 CHAPTER 17 Linked Data Structures

Display 17.7 Removing a Node

![](bbox=[0.137, 0.137, 0.853, 0.737])

This is sufficient to remove the node from the linked list. However, if you are not using this node for something else, you should destroy the node and return the memory it uses for recycling; you can do this with a call to `delete` as follows:

```
delete discard;
```
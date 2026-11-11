Figure 11.20 shows the result. Now you can collapse the entire tree into the root node.

![](bbox=[0.419, 0.197, 0.797, 0.391])

**Figure 11.20** A tree with a root handle

Conversely, you can hide the root altogether. You will thus display a *forest*—a set of trees, each with its own root. You still must join all trees in the forest to a common root; then, hide the root with the instruction

```
```java
tree.setRootVisible(false);
```
```

Look at Figure 11.21. There appear to be two roots, labeled “USA” and “Germany.” The actual root that joins the two is made invisible.

![](bbox=[0.344, 0.597, 0.743, 0.8])

**Figure 11.21** A forest

Let’s turn from the root to the leaves of the tree. Note that the leaves have an icon different from the other nodes (see Figure 11.22).
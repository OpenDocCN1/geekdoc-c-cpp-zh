In this pseudocode, how do we “fix the root of the entire tree so that it no longer has zero entries?” For example, we might have a tree that looks like this:

![](bbox=[0.332, 0.203, 0.762, 0.302])

Our solution for this problem is to first set a temporary pointer that points to the only child. Next, copy everything from the only child up to the root node. Finally, delete the original child. After this rearrangement, our tree will be one level shorter, as shown here:

![](bbox=[0.332, 0.392, 0.762, 0.461])

This shrinking at the root (within the remove member function) is the only point where a B-tree loses height. Now we are left with the task of designing the loose erase function.

# The Loose Erase from a B-Tree

The private loose_erase function starts in the same way as the count and insert functions, by finding the first index i such that data[i] is not less than the target. Once we have found this index, there are four possibilities, shown here:

```
// Removing a target entry from a set (loose erase)
1. Make a local variable, i, equal to the first index such that data[i] is not less than target. If there is no such index, then i equal to data_count, indicating that all of the entries are less than the target.
2. Deal with one of these four possibilities:
2a.The root has no children, and we did not find the target: In this case, there is no work to do, since the target is not in the set (return false).
2b.The root has no children, and we found the target: In this case, remove the target from the data array, and return true.
2c.The root has children, and we did not find the target (see following).
2d.The root has children, and we found the target (see following).
```

Cases 2c and 2d require further development.
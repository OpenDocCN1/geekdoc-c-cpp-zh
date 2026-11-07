![](bbox=[0.379, 0.089, 0.784, 0.401])

Insertion at the end is a special case of insertion at the middle in which the *cur* pointer should move to the last node. The new node is inserted after the last node. We leave this as an exercise.

**Erasure**  Erasure is applied to a specific node. If the list is not empty, we have three cases: erasure of the first node, erasure of a middle node, or erasure of the last node. Erasure of the first node is very simple and can be done as shown in Figure 18.8.

The erasure of a middle node is more involved. We must have a *cur* pointer to point to the node before the one to be deleted. We can then use another pointer, *del*, to point to the node to be erased. We can then erase the node. Figure 18.9 shows the operations involved in erasing a middle node.

Erasure at the end involves a similar process, but we must move the *cur* pointer to the node before the last node.

![](bbox=[0.297, 0.747, 0.866, 0.892])
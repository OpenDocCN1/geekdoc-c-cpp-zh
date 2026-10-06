# FIGURE 12-2 Places to insert strings into a sorted chain of linked nodes

![](bbox=[0.125, 0.131, 0.653, 0.246])

**The method insertSorted.** Adding an entry to a sorted list requires that you find where in the list the new entry belongs. Since the entries are sorted, you compare the new entry with the entries in the sorted list until you reach an entry that is not smaller than the new entry. Figure 12-2 depicts a chain of linked nodes, each containing a string alphabetically sorted. The figure shows where the additional strings "Ally","Cathy","Luke," and "Tom" would be inserted into the chain and the comparisons that would have to occur at those locations.

You can see from the figure that, in simple comparison, Ally is less than Bob, and so it would be inserted at the beginning of the chain. To Sue, you would find that Luke is greater than Bob and Jill but less than Mike. Thus, Luke belongs before Mike. On the other hand, Sue is one of the nodes. You would find Sue is greater than Bob, Jill, and Mike but not greater than Sue. So you would insert the new entry just before the existing entry. Finally, Tom is greater than all the names in the list, so you would add it to the end of the chain.

> Note: Given a sorted list with entries in ascending order, you insert a new entry before the first entry that is not smaller than the new entry.

Recall from earlier chapters that you add a new node to the beginning of a chain differently than at other points in the chain. Adding to the beginning is easy, since headPtr references the first node in the chain. To add anywhere else, you need a pointer to the node that will ultimately occur before the new node. Thus, while you traverse the chain of linked nodes to discover where the new entry belongs, you must retain a reference to the node prior to the one under consideration.

The following high-level algorithm describes our strategy:

```
// Adds a new entry to the sorted list.
add(newEntry)
Allocate a new node containing newEntrynSearch the chain until you find a node containing newEntry or you pass
t point where it should be
 prevPtr point to the node before the insertion point
 (head is empty or the new node belongs at the beginning of the chain)
    Add the new node to the beginning of the chain\else
Insert the new node after the node referenced by prevPtrnIncrement the length of the sorted list
```
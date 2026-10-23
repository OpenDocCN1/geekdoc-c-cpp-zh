The inner and outer loops are now complete. However, ‘L’ may still contain more items that should be placed at the end of the current linked list. Fortunately, "runner" and "Lrunner" were defined before the loops started, so they still exist. In fact, at this stage, "runner" points to the last item in the current linked list, and "Lrunner" points to the remaining items in ‘L’, if any. These items are appended to the current linked list as follows:

```
if (Lrunner && (Lrunner->item == runner->item)) {
    runner->item += Lrunner->item;
    Lrunner = Lrunner->next;
}
if (Lrunner) runner->next = new linkedList<T>(*Lrunner);
return *this;
} // merge two linked lists while preserving order
```

This completes the merging of ‘L’ into the current linked list while preserving order, as required.

# 3.9 The Ordering Problem

The ordering problem is as follows: find an efficient algorithm to order a given disordered list of items. Naturally, this algorithm requires changing the order in the original list. Thus, the linked list implemented above, which easily accepts every required change, is the obvious candidate for the data structure for the required algorithm.

![](bbox=[0.22, 0.68, 0.78, 0.82])

Figure 3.4. The "order()" function that orders a disordered linked list: the original list is split into two sublists, which are ordered recursively and merged (while preserving order).

Here, we use the "+=" operator that merges two ordered linked lists to define the "order()" template function that orders a disordered linked list (see Figure 3.4). The algorithm for doing this uses recursion as follows. Divide the disordered linked list into two sublists. Apply the "order()" function separately to each of these sublists. Then, merge them into a single, well-ordered list using the above "+=" operator.
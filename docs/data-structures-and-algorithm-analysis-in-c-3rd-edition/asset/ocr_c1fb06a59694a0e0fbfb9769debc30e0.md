ber of accesses required by the **optimal static ordering** for $n$ records when at least $n$ searches are performed. In other words, if we had known the series of (at least $n$) searches in advance and had stored the records in order of frequency so as to minimize the total cost for these accesses, this cost would be at least half the cost required by the move-to-front heuristic. (This will be proved using amortized analysis in Section 14.3.) Finally, move-to-front responds well to local changes in frequency of access, in that if a record is frequently accessed for a brief period of time it will be near the front of the list during that period of access. Move-to-front does poorly when the records are processed in sequential order, especially if that sequential order is then repeated multiple times.

+   3. Swap any record found with the record immediately preceding it in the list. This heuristic is called **transpose**. Transpose is good for list implementations based on either linked lists or arrays. Frequently used records will, over time, move to the front of the list. Records that were once frequently accessed but are no longer used will slowly drift toward the back. Thus, it appears to have good properties with respect to changing frequency of access. Unfortunately, there are some pathological sequences of access that can make transpose perform poorly. Consider the case where the last record of the list (call it $X$) is accessed. This record is then swapped with the next-to-last record (call it $Y$), making $Y$ the last record. If $Y$ is now accessed, it swaps with $X$. A repeated series of accesses alternating between $X$ and $Y$ will continually search to the end of the list, because neither record will ever make progress toward the front. However, such pathological cases are unusual in practice. A variation on transpose would be to move the accessed record forward in the list by some fixed number of steps.

# **Example 9.4** Assume that we have eight records, with key values $A$ to $H$, and that they are initially placed in alphabetical order. Now, consider the result of applying the following access pattern:

$F\ D\ F\ G\ E\ G\ F\ A\ D\ F\ G\ E.$

Assume that when a record’s frequency count goes up, it moves forward in the list to become the last record with that value for its frequency count. After the first two accesses, $F$ will be the first record and $D$ will be the second. The final list resulting from these accesses will be

$F\ G\ D\ E\ A\ B\ C\ H,$

and the total cost for the twelve accesses will be 45 comparisons.

If the list is organized by the move-to-front heuristic, then the final list will be

$E\ G\ F\ D\ A\ B\ C\ H,$
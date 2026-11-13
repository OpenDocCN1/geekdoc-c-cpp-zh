minimum and splitting the original binomial queue into two binomial queues, which are then merged. A less terse explanation of these operations is given in Chapter 6.

We consider a very simple problem first. Suppose we want to build a binomial queue of N elements. We know that building a binary heap of N elements can be done in O(N), so we expect a similar bound for binomial queues.

# Claim

A binomial queue of N elements can be built by N successive insertions in O(N) time.

The claim, if true, would give an extremely simple algorithm. Since the worst-case time for each insertion is O(log N), it is not obvious that the claim is true. Recall that if this algorithm were applied to binary heaps, the running time would be O(N log N).

To prove the claim, we could do a direct calculation. To measure the running time, we define the cost of each insertion to be one time unit plus an extra unit for each linking step. Summing this cost over all insertions gives the total running time. This total is N units plus the total number of linking steps. The 1st, 3rd, 5th, and all odd-numbered steps require no linking steps, since there is no B0 tree present at the time of insertion. Thus, half the insertions require no linking steps. A quarter of the insertions require only one linking step (2nd, 6th, 10th, and so on). An eighth requires two, and so on. We could add this all up and bound the number of linking steps by N, proving the claim. This brute-force calculation will not help when we try to analyze a sequence of operations that include more than just insertions, so we will use another approach to prove this result.

Consider the result of an insertion. If there is no B0 tree present at the time of the insertion, then the insertion costs a total of one unit, using the same accounting as above. The result of the insertion is that there is now a B0 tree, and thus we have added one tree to the forest of binomial trees. If there is a B0 tree but no B1 tree, then the insertion costs two units. The new forest will have a B1 tree but will no longer have a B0 tree, so the number of trees in the forest is unchanged. An insertion that costs three units will create a B2 tree but destroy a B0 and B1 tree, yielding a net loss of one tree in the forest. In fact, it is easy to see that, in general, an insertion that costs c units results in a net increase of 2 - c trees in the forest, because a B<sub>c-1</sub> tree is created but all B<sub>i</sub> trees 0 <= i < c - 1 are removed. Thus, expensive insertions remove trees, while cheap insertions create trees.

Let C<sub>i</sub> be the cost of the ith insertion. Let T<sub>i</sub> be the number of trees after the ith insertion. T<sub>0</sub> = 0 is the number of trees initially. Then we have the invariant

```
C<sub>i</sub> + (T<sub>i</sub> - T<sub>i-1</sub>) = 2   (11.1)
```

We then have

```
C<sub>1</sub> + (T<sub>1</sub> - T<sub>0</sub>) = 2
C<sub>2</sub> + (T<sub>2</sub> - T<sub>1</sub>) = 2
...
C<sub>N-1</sub> + (T<sub>N-1</sub> - T<sub>N-2</sub>) = 2
C<sub>N</sub> + (T<sub>N</sub> - T<sub>N-1</sub>) = 2
```
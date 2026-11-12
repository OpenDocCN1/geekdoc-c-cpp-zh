RANDOMIZED-KTH-MIN-SELECT differs from RANDOMIZED-QUICKSORT because it recurses on one side of the partition only. After the call to RANDOMIZED-PARTITION, the sequence a[l..r] is partitioned into two sub-sequences a[l..p - 1] and a[p + 1..r], along with a pivot element a[p]:

+   * The elements of sub-sequence a[l..p - 1] are all ≤ a[p].
+   * The elements of sub-sequence a[p + 1..r] are all > a[p].
+   * The pivot element is the pdist<sup>th</sup> element of the sub-sequence a[l..r], where pdist = p-l + 1.
+   * If the pivot element is the k<sup>th</sup> smallest element (i.e., k = pdist), return A[p].
+   * Otherwise, recurse on the sub-sequence containing the k<sup>th</sup> smallest element.
+     - If k < pdist, this sub-sequence is a[l..p - 1] and we want the k<sup>th</sup> smallest element.
+     - If k > pdist, this sub-sequence is a[p + 1..r] and, since there are pdist elements in a[l..r] that precede a[p + 1..r], we want the (k - pdist)<sup>th</sup> smallest element of this sub-sequence.

It resembles a *partial quicksort*, generating and partitioning only O(n) of its O(n) partitions. This simple algorithm has expected linear performance, and, like quicksort, has quite good performance in practice. It is also an *in-place* algorithm, requiring only constant memory overhead, since the tail recursion can be eliminated with an equivalent iterative version as shown in the next section. In a *tail recursion*, the call is always the last action in an algorithm. A tail-recursive algorithm can always be transformed into an equivalent iterative algorithm with a *while* loop as shown ahead.
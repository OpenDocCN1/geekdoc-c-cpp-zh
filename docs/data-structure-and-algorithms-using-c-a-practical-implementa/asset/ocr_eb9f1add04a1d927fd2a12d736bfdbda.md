# ALGORITHM INCREASE-KEY(A,i,key))

+   1. if key < A[i]
+   2. then write "key is smaller than the current key"
+   3. A[i] <- key
+   4. while i > 1 and A[PARENT(i)] < A[i]
+   5. do exchange A[i] <-> A[PARENT(i)]
+   6. i <- Parent(i)

# ALGORITHM INSERT(A,key)

+   1. heapsize[A] <- heapsize[A] + 1
+   2. A[heapsize[A]] <- -∞
+   3. INCREASE-KEY(A, heapsize[A], key)

The running time of INSERT on an n-element heap is O(lgn)
A heap can support any priority-queue operation on a set of size n in O(lgn) time.

# OPERATIONS FOR MIN PRIORITY QUEUE

# ALGORITHM MINIMUM(A,X)

+   2. return A[1]

# ALGORITHM EXTRACT-MIN(A)

+   8. If heapsize[A] < 1
+   9. then Write : "Heap Underflow"
+   10. Max <- A[1]
+   11. A[1] <- A[heapsize[A]]
+   12. heapsize[A] <- heapsize[A] - 1
+   13. Max_Heap(A, 1)
+   14. retrun Min

# ALGORITHM DECREASE-KEY(A,i,key))

+   7. if key > A[i]
+   8. then write "key is greater than the current key"
+   9. A[i] <- key
+   10. while i > 1 and A[PARENT(i)] > A[i]
Moreover, each sublist can also be divided into two sublists of the same size. Each call to the function `recMergeSort` makes two recursive calls to the function `recMergeSort`, and each call divides the sublist into two sublists of the same size. Suppose that $m = 3$, that is, $n = 2^3 = 8$. So the length of the original list is 8. The first call to the function `recMergeSort` divides the original list into two sublists, each of size 4. The first call then makes two recursive calls to the function `recMergeSort`. Each of these recursive calls divides each sublist, of size 4, into two sublists, each of size 2. We now have 4 sublists, each of size 2. The next set of recursive calls divides each sublist, of size 2, into sublists of size 1. So we now have 8 sublists, each of size 1. It follows that the exponent 3 in $2^3$ indicates the level of the recursion (see Figure 18-38).

![](bbox=[0.183, 0.289, 0.91, 0.63])

Figure 18-38  Levels of recursion to `recMergeSort` for a list of length 8

Let us consider the general case when $n = 2^m$. Note that the number of recursion levels is $m$. Also, note that to merge a sorted list of size $s$ with a sorted list of size $t$, the maximum number of comparisons is $s + t - 1$.

Consider the function `mergeList`, which merges two sorted lists into a sorted list. Note that this is where the actual work (comparisons and assignments) is done. The initial call to the function `recMergeSort`, at level 0, produces two sublists, each of the size $n / 2$. To merge these two lists, after they are sorted, the maximum number of comparisons is

$$\frac{n}{2} + \frac{n}{2} - 1 = n - 1 = O(n).$$

At level 1, we merge two sets of sorted lists, where each sublist is of the size $n / 4$. To merge two sorted sublists, each of the size $n / 4$, we need at most

$$\frac{n}{4} + \frac{n}{4} - 1 = \frac{n}{2} - 1$$
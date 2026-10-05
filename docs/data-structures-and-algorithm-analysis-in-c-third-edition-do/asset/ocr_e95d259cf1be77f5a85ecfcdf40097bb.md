7.18 Which of the following operations are best implemented by first sorting the list of numbers? For each operation, briefly describe an algorithm to implement it, and state the algorithm's asymptotic complexity.

+   (a) Find the minimum value.
(b) Find the maximum value.
(c) Compute the arithmetic mean.
(d) Find the median (i.e., the middle value).
(e) Find the mode (i.e., the value that appears the most times).

7.19 Consider a recursive Mergesort implementation that calls Insertion Sort on sublists smaller than some threshold. How many calls will there be to Insertion Sort? Why?

7.20 Implement Mergesort for the case where the input is a linked list.
7.21 Counting sort (assuming the input are integers in the range 0 to $m-1$) works by counting the number of records with each value in the first pass, and then uses this to place the records in order in a second pass. Write an implementation of counting sort (see the implementation for some details). What can we say about the relative values of $m$ and $n$ for this to be effective? If $m < n$, what is the running time of this algorithm?

7.22 Use an argument similar to that given in Section 7.9 to prove that $\log n$ is a worst-case lower bound for the problem of searching for a value in a sorted array containing elements.

7.23 A simple way to do the Quicksort partition step is to set index `split` to the position of the first value greater than the pivot. Then move `split+1` index `curr` to the right until it finds a value less than the pivot. Swap the values at `split` and `next`, and increment `split`. Continue this way, swapping the smaller values to the left side. When `curr` reaches the end of the subarray, `split` will be at the split point between the two partitions. Unfortunately, this approach requires more swaps than the version presented in Section 7.5, resulting in a slower implementation. Give an example and explain why.

# Projects

7.1 One possible improvement for Bubble Sort would be to add a flag variable and a test that determines if an exchange was made during the current iteration. If no exchange was made, then the list is sorted and the algorithm can stop early. This makes the best case performance O(n) (because if the list is already sorted, no iterations will take place on the first pass, and the sort will stop right there).
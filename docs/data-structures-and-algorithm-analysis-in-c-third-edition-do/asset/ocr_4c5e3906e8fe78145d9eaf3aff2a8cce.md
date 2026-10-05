can you qualitatively observe the rate of increase in expected cost as the probability of unsuccessful search growth?

9.2 Modify the binary search routine of Section 3.5 to implement interpolation search. Assume that keys are in the range 1 to 10,000, and that all key values within the range are equally likely to occur.

9.3 Write an algorithm to find the $k$-th smallest value in an unsorted array ($k \le n$). Your algorithm should run $\Theta(n)$ time in the average case. Your algorithm should look similar to Quicksort.

9.4 Example 9.9.3 discusses a distribution where the relative frequencies of the records match the second record as often as the third, and so on. For every occurrence of the first record, the second record will appear as often as the third, the fourth one quarter as often. The actual probability for the $i$-th record was defined to be $1/H_n$. Explain why this is correct.

9.5 Graph the equations $T(n) = \log_2 n$ and $T(n) = n/\log_n n$. Which gives the better performance, binary search on a sorted list, or sequential search on a list ordered by frequency where the frequency conforms to a Zipf distribution? Characterize the difference in running times.

9.6 Assume that the $A$ through $H$ are stored in a self-organizing list, in descending order. Consider the three self-organizing list heuristics: count, move-to-front, and transpose. For count, assume that the record is moved ahead in the list passing over any other record that is count greater than. For each, show the resulting list and the total number of comparisons required from the following sequences of accesses:

D H H G E G H G H E C E H E G,

9.7 For each of the three self-organizing list heuristics (move-to-front, and transpose), describe a series of record accesses for which it would require the greatest number of comparisons of the three.

9.8 Write an algorithm to implement the frequency count self-organizing list heuristic, assuming that the list is implemented using an array. In particular, write a function `FreqCount` that takes as input a value to be searched for and which adjusts the list appropriately. If the value is not already in the list, add it to the end of the list with a frequency count of one.

9.9 Write an algorithm to implement the move-to-front self-organizing list heuristic, assuming that the list is implemented using an array. In particular, write a function `MoveToFront` that takes as input a value to be searched for and which adjusts the list appropriately. If the value is not already in the list, add it to the beginning of the list.

9.10 Write an algorithm to implement the transpose self-organizing heuristic, assuming that the list is implemented using an array. In particular, write
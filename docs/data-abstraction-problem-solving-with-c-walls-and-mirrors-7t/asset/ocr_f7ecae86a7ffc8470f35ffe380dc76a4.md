**Analysis.** As was noted earlier, the bubble sort requires at most n - 1 passes through the array. Pass 1 requires n - 1 comparisons and at most n - 1 exchanges; pass 2 requires n - 2 comparisons and at most n - 2 exchanges. In general, pass i requires n - i comparisons and at most n - i exchanges. Therefore, in the worst case, a bubble sort will require a total of (n - 1) + (n - 2) + ... + 1 = n x (n - 1)/2 comparisons and the same number of exchanges. Recall that each exchange requires three data moves. Thus, altogether there are 2 x n x (n - 1) = 2 x n^2 - 2 x n major operations in the worst case. Therefore, the bubble sort algorithm is O(n^2) in the worst case. The best case occurs when the original data is already sorted: bubbleSort uses one pass, during which n - 1 comparisons and no exchanges occur. Thus, the bubble sort is O(n) in the best case.

Bubble sort: Worst case: O(n^2) Best case: O(n)

# 11.1.3 The Insertion Sort

Imagine once again arranging a hand of cards, but now you pick up one card at a time and insert it into its proper position; in this case, you are performing an **insertion sort**. Chapter 8 introduced the insertion sort algorithm in the context of a list of alphabetical names. In that example, we repeatedly called the method `insert` to add a string into its proper sorted order in a list.

You can use the insertion sort strategy to sort items that reside in an array. This version of the insertion sort partitions the array into two regions: sorted and unsorted, as Figure 11-3 depicts. Initially, the entire array is the unsorted region, just as the cards dealt to you sit in an unsorted pile on the table. At each step, the insertion sort takes the first item of the unsorted region and places it into its correct position in the sorted region. This step is analogous to taking a card from the table and inserting it into its proper position in your hand. The first step, however, is trivial: Moving `theArray[0]` from the unsorted region to the sorted region really does not require moving data. Therefore, you can omit this first step by considering the initial sorted region to be `theArray[0]` and the initial unsorted region to be `theArray[1 . . n - 1]`. The fact that the items in the sorted region are sorted among themselves is an assertion of the algorithm. Because at each step the size of the sorted region grows by 1 and the size of the unsorted region shrinks by 1, the entire array will be sorted when the algorithm terminates.

Take each item from the unsorted region and insert it into its correct order in the sorted region

Figure 11-4 illustrates an insertion sort of an array of five integers. Initially, the sorted region is theArray[0], which is 29, and the unsorted region is the rest of the array. You take the first item in the unsorted region—the 10—and insert it into its proper position in the sorted region. This insertion

# FIGURE 11-3 An insertion sort partitions the array into two regions

![](bbox=[0.2, 0.76, 0.65, 0.85])
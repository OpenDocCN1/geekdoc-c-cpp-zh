# 15.7 Sorts

In chapter 13 we used loops to make our iteration. We only used recursion when working with Lists, and the sorts were longer than the imperative versions. We could also write those sorts recursively using Arrays, but then the use of recursion is only a change in presentation. It not really affects how the sorts run or how efficient they are. The recursion in these functions is only used for iteration, nothing more. However, recursion also opens the door to more efficient sorts. The next two subsections describe of these.

# 15.7.1 Divide and Conquer Sorts

Recursion that calls itself multiple times opens up a new style of problem solving called DIVIDE AND CONQUER. The idea is exactly what name sounds like. You take a big problem, divide it up, conquer/solve the pieces, then build a solution to the larger problem from the solutions to the pieces. The divide and conquer approach is very general and can be applied to many types of problems. In this section, we will look at two different algorithms that are all merge

# 15.7.1.1 Merge Sort

The first sort that we consider is the MERGE SORT. The general idea of a merge sort is that we have a collection that we break into two roughly equal pieces. Each of those pieces is sorted individually and the sorted results are merged back together.

This is a fast algorithm because the merge operation is O(n). The reason for this is when you find the lowest element from each collection, you do not have to go through all the elements, you only need to consider the elements at the low ends of the two collections. We then do only one comparison. To find the next lowest element you go again and make a sort of n elements from two smaller sorted collections with only n - 1 comparisons. The fact that you are repeatedly cutting the collection in half means that you get down to a single element in log(n) cuts. This gives an overall performance of O(n log(n)). For large values of n, this is much better than the O(n^2) performance of the sorts considered earlier.

There is one problem with the merge sort: it cannot be in-place. Recall that being done in-place means modifying the original collection without the additional memory. Merge sort requires additional memory proportional to n to complete the sort. A crafted merge sort can get everything with one additional Array of length n. Getting the memory usage to do that is a bit complex so it is not presented in this book. In this chapter, we will use the inability to do the sort-place as an excuse for using Lists, which requires extra space anywhere they are immutable.

The first solution that we will look at is all recursive. It has a recursive mergeSort function that takes a List [Int] and returns a List [Int]. The sort function uses a second recursive called merge to put the pieces together.

> Such an implementation is presented in Object-Orientation, Abstraction, and Data Structures Using Scala.

> Recall that unlike sorts with Arrays, using a List must return a new List as the original one cannot be altered.
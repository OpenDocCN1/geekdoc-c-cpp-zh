# Chapter 7 Searching

Interpolation search works well for arrays of any size that you can reason fit on a computer. It can search an array containing 1 trillion items in only five steps. In fact, an array would need to hold more than 1x10¹¹⁴ items before interpolation search would require an expected number of steps greater than nine.

However, the exact number of steps for interpolation search depends on the distribution of the values. Sometimes the algorithm gets lucky and finds the target in one or two steps, and other times it might need four or five. On average, however, it is extremely fast.

# Exercises

If you don't know what recursion is, skip exercises 2, 5, and 7 and come back to them after you read Chapter 8, which introduces recursion.

+   1. Write a program that implements linear search.
2. Write a program that implements linear search recursively. Does this version have any advantages or disadvantages compared to the nonrecursive version?
3. Write a program that implements linear search with sorted lists.
4. Write a program that implements binary search.
5. Write a program that implements binary search recursively. Does this version have any advantages or disadvantages compared to the nonrecursive version?
6. Write a program that implements interpolation search.
7. Write a program that implements interpolation search recursively. Does this version have any advantages or disadvantages compared to the nonrecursive version?
8. Which sorting algorithm described in Chapter 6 uses a technique reminiscent of the technique used by interpolation search?
9. If an array contains duplicates, the binary search and interpolation search algorithms described in this chapter don't guarantee they return the first instance of the target item. How could you modify them to return the first occurrence of the target item? What is the run time for the modified version?
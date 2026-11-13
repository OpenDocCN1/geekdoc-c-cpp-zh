# Appendix B Further Big-O Notation

# Formal Definition of Big-O

Throughout the text, we analyze the running times of algorithms in terms of the size of an algorithm's input. For example, in Section 12.1 we developed a binary search algorithm to search an array of n elements, looking for a specified target. On page 593, we saw that the maximum number of operations for the binary search is given by the formula:

```
T(n) = the maximum number of operations to search an n-element array
= 18(⌊log₂ n⌋ + 1) + 2
```

Big-O notation is a way of analyzing a function such as T(n). The analysis throws away some information about the function, but keeps other information that is most relevant to determining algorithm performance. In an informal way, you know enough to examine the function T(n) for the binary search; you can “throw out the constants” and conclude that T(n) is an O(log n) function.

In general, when we examine a function, such as T(n), the big-O analysis results in some simpler expression, such as log n. The simpler expression is also a function of n. If we call this F(n), then a typical big-O analysis provides a result of the form “T(n) is an O(F(n)) function.” In mathematical terms, this kind of result has a precise definition, as follows:

When we say that “T(n) is an O(F(n)) function,” we mean that there is some fixed number that we call the threshold, and some constant multiplier that we call c, such that

Whenever n ≥ threshold, then T(n) ≤ cF(n).

For example, consider the function T(n) = 3n² + 9n. Some arithmetic shows that whenever n ≥ 5, then 3n² + 9n ≤ 4n². Therefore, using a threshold of 5, and a constant multiplier of 4, we can see that

3n² + 9n is an O(n²) function.

The graph at the top of the next page illustrates the meaning of a big-O expression. Notice that before the threshold, either of the two functions may be larger; anything can happen before this threshold value. But once n exceeds the threshold, the function cF(n) is always greater than T(n). Also notice that it is c multiplied by F(n), and not simply F(n), that we are comparing to T(n). So, the graph illustrates the fact that “T(n) is an O(F(n)) function.”
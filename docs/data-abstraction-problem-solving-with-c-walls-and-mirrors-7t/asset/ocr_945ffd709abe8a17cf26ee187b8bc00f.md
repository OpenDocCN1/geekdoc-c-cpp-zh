# FIGURE 2-12 Recursive solution to the largest-value problem

![](bbox=[0.15, 0.14, 0.65, 0.26])

# FIGURE 2-13 The recursive calls that maxArray(<1, 6, 8, 3>) generates

![](bbox=[0.06, 0.34, 0.85, 0.66])

The previous two examples presented recursive techniques for finding the largest value in an arbitrary array and for finding an arbitrary value in a sorted array. This example describes a recursive solution for finding the kth smallest value in an arbitrary array anArray. Would you ever be interested in such a value? Statisticians often want the median value in a collection of data. The median value in an ordered collection of data occurs in the middle of the collection. In an unordered collection of data, the number of values that are smaller than the median value is about the same as the number of values that are larger. Thus, if you have 49 values, the 25th smallest value is the median value. Obviously, you could solve this problem by sorting the array. Then the kth smallest value would be anArray[k-1]. Although this approach is a legitimate solution, it does more than the problem requires; a more efficient solution is possible. The solution outlined here finds the kth smallest value without completely sorting the array. By now, you know that you solve a problem recursively by writing its solution in terms of one or more smaller problems of the same type in such a way that this notion of smaller ensures that you will always reach a base case. For all of the earlier recursive solutions, the reduction in problem size
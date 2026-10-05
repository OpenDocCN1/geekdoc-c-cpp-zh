78

Chap. 3 Algorithm Analysis

cost. There cannot be a growth rate for a single point, such as a particular value of n. The growth rate applies to the change in cost as a change in input size occurs. Likewise, the lower bound is not the same as the best case for a given n.

Another misconception is thinking that the best case for an algorithm occurs when the input size is as small as possible, or that the worst case occurs when the input size is as large as possible. What is correct that best- and worst instances exist for each possible size of input. That is, for all inputs of a given size, say i, one (or more) of the inputs of size i is the best and one (or more) of the inputs of size i is the worst. Often (but not always!), we can characterize the best input case for an arbitrary size, and we can determine the growth rate for the characterized best, worst, and average cases as the input size grows.

**Example 3.14** \u2013d What is the growth rate of the best case for sequential search? For any array of size n, the best case occurs when the value we are looking for the first position of the array. This is true-less of the size of the array. Thus, the best case (for arbitrary size n) occurs when the desired value is in the first position of n positions, and its cost is 1. It is not correct to say that the best case occurs when n=1.

**Example 3.15** Imagine drawing a graph to show the cost of finding the maximum value among n values

Now, imagine the graph showing the cost for each instance of the problem of finding the maximum value among 20 elements in an array. The first position on the x axis of the graph might correspond to having the maximum element in the first position of the array. The second position on the x axis of the graph might correspond to having the maximum element in the second position of the array, and so on. Of course, the cost is always 20. Therefore, the graph would be a horizontal line with value 20. You should sketch this graph for yourself.

Now us switch to the problem of doing a sequential search for a given value in an array. Think about the graph showing all the problem instances of size 20. The first instance might be when the value we search for is in the first position of the array. This has cost 1. The second problem instance might be when the value we search for is in the second position of the array. This has cost 2. And so on. If we arrange the problem instances of size 20 from least expensive on the left to most expensive on
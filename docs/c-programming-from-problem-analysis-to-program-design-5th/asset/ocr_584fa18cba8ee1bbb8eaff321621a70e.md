Let us demonstrate how this algorithm works with an example. Suppose the array `sales` is as given in Figure 9-6.

|  | [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| sales | 12.50 | 8.35 | 19.60 | 25.00 | 14.00 | 39.43 | 35.90 | 98.23 | 66.65 | 35.64 |

**FIGURE 9-6**  Array `sales`

Here, we determine the largest element in the array `sales`. Before the `for` loop begins, `maxIndex` is initialized to 0, and the `for` loop initializes `index` to 1. In the following, we show the values of `maxIndex`, `index`, and certain array elements during each iteration of the `for` loop.

| index | maxIndex | sales[maxIndex] | sales[index] | sales[maxIndex] < sales[index] |
|---:|---:|---:|---:|---|
| 1 | 0 | 12.50 | 8.35 | 12.50 < 8.35 is **false** |
| 2 | 0 | 12.50 | 19.60 | 12.50 < 19.60 is **true**; maxIndex = 2 |
| 3 | 2 | 19.60 | 25.00 | 19.60 < 25.00 is **true**; maxIndex = 3 |
| 4 | 3 | 25.00 | 14.00 | 25.00 < 14.00 is **false** |
| 5 | 3 | 25.00 | 39.43 | 25.00 < 39.43 is **true**; maxIndex = 5 |
| 6 | 5 | 39.43 | 35.90 | 39.43 < 35.90 is **false** |
| 7 | 5 | 39.43 | 98.23 | 39.43 < 98.23 is **true**; maxIndex = 7 |
| 8 | 7 | 98.23 | 66.65 | 98.23 < 66.65 is **false** |
| 9 | 7 | 98.23 | 35.64 | 98.23 < 35.64 is **false** |

After the `for` loop executes, `maxIndex = 7`, giving the index of the largest element in the array `sales`. Thus, `largestSale = sales[maxIndex] = 98.23`.

> **NOTE**  You can write an algorithm to find the smallest element in the array that is similar to the algorithm for finding the largest element in an array. (See Programming Exercise 2 at the end of this chapter.)

Now that we know how to declare and process arrays, let us rewrite the program that we discussed in the beginning of this chapter. Recall that this program reads five numbers, finds the sum, and prints the numbers in reverse order.
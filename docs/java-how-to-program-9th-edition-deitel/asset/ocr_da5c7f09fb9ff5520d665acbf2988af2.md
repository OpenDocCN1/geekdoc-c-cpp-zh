call to merge requires, at worst, n-1 comparisons to fill the original array, which is O(n). (Recall that each element in the array can be chosen by comparing one element from each of the subarrays.) The two calls to sortArray result in four more recursive calls to sortArray, each with a subarray approximately a quarter the size of the original array along with two calls to method merge. These two calls to method merge each require, at worst, n/2 – 1 comparisons, for a total number of comparisons of O(n). This process continues, each call to sortArray generating two additional calls to sortArray and a call to merge, until the algorithm has split the array into one-element subarrays. At each level, O(n) comparisons are required to merge the subarrays. Each level splits the size of the arrays in half, so doubling the array size requires one more level. Quadrupling the array size requires two more levels. This pattern is logarithmic and results in log2n levels. This results in a total efficiency of O(n log n).

Figure 19.12 summarizes the searching and sorting algorithms covered in this chapter with the Big O for each. Figure 19.13 lists the Big O values we’ve covered in this chapter along with a number of values for n to highlight the differences in the growth rates.

Fig. 19.12 | Searching and sorting algorithms with Big O values.
| Algorithm | Location | Big O |
|---|---|---|
|Searching Algorithms:|||
|Linear search|Section 19.2.1|O(n)|
|Binary search|Section 19.2.2|O(log n)|
|Recursive linear search|Exercise 19.8|O(n)|
|Recursive binary search|Exercise 19.9|O(log n)|
|Sorting Algorithms:|||
|Selection sort|Section 19.3.1|O(n²)|
|Insertion sort|Section 19.3.2|O(n²)|
|Merge sort|Section 19.3.3|O(n log n)|
|Bubble sort|Exercises 19.5 and 19.6|O(n²)|

Fig. 19.13 | Number of comparisons for common Big O notations.
| n = | O(log n) | O(n) | O(n log n) | O(n²) |
|---|---|---|---|---|
|1|0|1|0|1|
|2|1|2|2|4|
|3|1|3|3|9|
|4|1|4|4|16|
|5|1|5|5|25|
|10|1|10|10|100|
|100|2|100|200|10,000|
|1,000|3|1,000|3,000|10^6|
|1,000,000|6|1,000,000|6,000,000|10^12|
|1,000,000,000|9|1,000,000,000|9,000,000,000|10^18|
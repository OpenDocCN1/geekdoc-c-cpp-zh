# ## ANSWERS TO SELF-CHECK QUESTIONS

+   1. 1 | 5 4 3 2 6, 1 2 | 4 3 5 6, 1 2 3 4 5 6
+   2. In each step, find the maximum of the remaining elements and swap it with the current element (or see Self Check 3).
+   3. The modified algorithm sorts the array in descending order.
+   4. Dropping the temp variable would not work. Then a[i] and a[j] would end up being the same value.
+   5. Four times as long as 40,000 values, or about 50 seconds.
+   6. A parabola.
+   7. It takes about 100 times longer.
+   8. If n is 4, then 1/2 n² is 8 and 5/2 n – 3 is 7.
+   9. The first algorithm requires one visit, to store the new element. The second algorithm requires T(p) = 2 × (n – p – 1) visits, where p is the location at which the element is removed. We don’t know where that element is, but if elements are removed at random locations, on average, half of the removals will be above the middle and half below, so we can assume an average p of n / 2 and T(n) = 2 × (n – n / 2 – 1) = n – 2.
+   10. The first algorithm is O(1), the second O(n).
+   11. Let n be the length of the array. In the kth step, we need k visits to find the minimum. To remove it, we need an average of k – 2 visits (see Self Check 9). One additional visit is required to add t to the end. Thus, the kth step requires 2k – 1 visits. Because k goes from n to 2, the total number of visits is
+       2n – 1 + 2(n – 1) – 1 + ... + 2 · 3 – 1 + 2 · 2 – 1
+       = 2(n + (n – 1) + ... + 3 + 2 + 1) – (n – 1)
+       = n(n + 1) – 2 – n + 1 (because 1 + 2 + 3 + ... + (n – 1) + n = n(n + 1)/2)
+       = n² – 3
+       Therefore, the total number of visits is O(n²).
+   12. When the preceding while loop ends, the loop condition must be false, that is, i1 > mid (in which case the first loop isn’t executed), or i2 > to (in which case the second loop isn’t executed).
+   13. First sort 8 7 6 5. Recursively, first sort 8 7. Recursively, first sort 8. It’s sorted. Sort 7. It’s sorted. Merge them: 7 8. Do the same with 6 5 to get 5 6. Merge them to 5 6 7 8. Do the same with 4 3 2 1: Sort 4 3 by sorting 4 and 3 and merging them to 3 4. Sort 2 1 by sorting 2 and 1 and merging them to 1 2. Merge 3 4 and 1 2 to 1 2 3 4. Finally, merge 5 6 7 8 and 1 2 3 4 to 1 2 3 4 5 6 7 8.
+   14. If the array size is 1, return its only element as the sum. Otherwise, recursively compute the sum of the first and second subarray and return the sum of these two values.
+   15. Approximately (100,000 · log(100,000)) / (50,000 · log(50,000)) = (2 · 5) / 4.7 = 2.13 times the time required for 50,000 values. That’s 2.13 · 97 milliseconds or approximately 207 milliseconds.
+   16. (2n log(2n)) / (n log(n)) = (2(1 + log(2))) / log(n). For n > 2, this is a value < 3.
+   17. On average, you’d make 500,000 comparisons.
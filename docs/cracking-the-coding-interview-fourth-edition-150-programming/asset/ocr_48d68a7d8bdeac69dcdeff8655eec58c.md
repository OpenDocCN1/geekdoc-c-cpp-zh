# Solutions to Chapter 19 | Moderate

19.7 You are given an array of integers (both positive and negative). Find the continuous sequence with the largest sum. Return the sum.

EXAMPLE

Input: {2, -8, 3, -2, -10}
Output: 5 {(3, -2, 4)}

# SOLUTION

A simple linear algorithm will work by keeping track of the current subsequence sum. If that sum drops below zero, that subsequence will not contribute to the subsequent maximal subsequence since it would reduce it by adding the negative sum.

```
public static int maxSum(int[] a) {
    int maxsum = 0;
    int sum = 0;
    for (int i = 0; i < a.length; i++) {
        sum += a[i];
        if (maxsum < sum)
            maxsum = sum;
        } else if (sum < 0) {
            sum = 0;
        }
    }
    return maxsum;
}
```

NOTE: If the array is all negative numbers, what is the correct behavior? Consider this simple array a good argument that the maximum sum is: (A) -3 (if you assume the subsequence can't be empty) (B) 0 (the subsequence has length 0) or (C) MAXIMUM_INT (essentially the error case). We went with option B (max sum = 0), but there is no "correct" answer. This is a great thing to discuss with your interviewer to show how careful you are.
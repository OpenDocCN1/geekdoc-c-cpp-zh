Although the solution is conceptually sound, you must consider several details before you can implement the algorithm:

# 1. How will you pass half of anArray to the recursive calls to binarySearch? You can pass the entire array at each call but have binarySearch search only anArray[first..last], that is, the portion anArray[first] through anArray[last]. Thus, you would also pass the integers first and last to binarySearch:

```
binarySearch(anArray, first, last, target)
```

With this convention, the new midpoint is given by

```
mid = (first + last) / 2
```

Then binarySearch( first half of anArray, target ) becomes

```
binarySearch(anArray, first, mid - 1, target)
```

and binarySearch( second half of anArray, target ) becomes

```
binarySearch(anArray, mid + 1, last, target)
```

The array halves are anArray[first..mid-1] and anArray[mid+1..last]; neither half contains anArray[mid]

# 2. How do you determine which half of the array contains target? One possible implementation of

```
if (target is in the first half of anArray)
```

is

```
if (target < anArray[mid])
```

Determine whether anArray[mid] is the target you seek

However, there is no test for equality between target and anArray[mid]. This omission can cause the algorithm to miss target. After the previous halving algorithm splits anArray into halves, anArray[mid] is not in either half of the array. (In this case, two halves do not make a whole!) Therefore, you must determine whether anArray[mid] is the value you seek now; because later it will not be in the remaining half of the array. The interaction between halving criterion and the termination condition (the base case) is subtle and is often a source of error. We need to rethink the base case.

# 3. What should the base case(s) be? As it is written, binarySearch terminates only when an array of size 1 occurs; this is the only base case. By changing the halving process so that anArray[mid] remains in one of the halves, it is possible to implement the binary search correctly so that it has only this single base case. However, it can be clearer to have two distinct base cases as follows:

+   • first > last. You will reach this base case when target is not in the original array.

+   • target == anArray[mid]. You will reach this base case when target is in the original array.

These base cases are a bit different from any you have encountered previously. In a sense, the algorithm determines the answer to the problem from the base case it reaches. Many search problems have this flavor.

# 4. How will binarySearch indicate the result of the search? If binarySearch successfully locates target in the array, it could return the index of the array value that is equal to target. Because this index would never be negative, binarySearch could return a negative value if it does not find target in the array.

The C++ function binarySearch that follows implements these ideas. The two recursive calls to binarySearch are labeled as X and Y for use in a later box trace of this function.
# Thinking Recursively

The indexes of the array a are the integers 0 through finalIndex. To make the task of searching the array easier, we will assume that the array is sorted. Hence, we know the following:

```
a[0] <= a[2] <= ... a[finalIndex]
```

When searching an array, you are likely to know both whether the value is in the list, and if it is, where it is. For example, if we are searching for a credit number card, then the array may serve as a record number. Another array indexed by these same indices may hold a phone number or other information to use for reporting the suspicious candidate. Hence, if the sought-after value is in the array, we will want our function to tell what value is in the array.

Now let us proceed to produce an algorithm to solve this task. It will help to visualize the problem in very concrete terms. Suppose the list is so long that it takes a book to list them all. This is how invalid credit card numbers are distributed to stores that have no access to computers. If you are a clerk and are handed a credit card, you must check if it is on the list and hence invalid. How would you proceed? Open the book to the middle and see if the number is. If it is not and it is smaller than the middle number, then work toward the middle number. If the number is larger than the middle number, work your way toward the end of the book. This produces our first draft of an algorithm:

![](bbox=[0.039, 0.497, 0.149, 0.526])

```
found = false;// so far.
mid = approximate midpoint between 0 and finalIndex;
if (key == a[mid]) {
    found = true;
    location = mid;
} else if (key < a[mid]) {
    search[0] through a[mid - 1];
} else if (key > a[mid]) {
    search[mid + 1] through a[finalIndex];
}
```

Since the searches of the shorter lists are smaller versions of the task we are designing the algorithm to perform, this algorithm naturally lends itself to the use of recursion. The smaller lists can be searched with recursive calls to the algorithm itself.

Our pseudocode is a bit too imprecise to be easily translated to C++ code. The problem has to deal with the recursive calls. We have two recursive calls shown:

```
search[0] through a[mid - 1];
```

and

```
search[mid + 1] through a[finalIndex];
```

To implement these recursive calls, we need two parameters. A recursive call specifies that a subrange of the array is to be searched. In one case, it is the elements indexed by 0 through mid - 1. In the other case, it is the elements indexed by mid + 1
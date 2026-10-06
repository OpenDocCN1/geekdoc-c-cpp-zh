# Sorting and Searching

| n | ~log₂ n |
|---||
| 1,000 | 10 |
| 1,000,000 | 20 |
| 1,000,000,000 | 30 |
| 1,000,000,000,000 | 40 |

**Table 13.1:** Table of approximate values of $\log_2 n$ as a function of $n$. We use the approximation that $2^{10} \approx 10^3$. The reality is $2^{10} = 1024$, but this approximation is rather close and is a good one to keep in your head for quick approximations.

two extras. The normal way to get around that is to provide a wrapper function that only has two arguments and have it call this version. An appropriate wrapper could be written this.

```
def binarySearch(a:Array[Int],value:Int):Int =
    binarySearchRecur(a, value, 0, a.length)
```

The logic of the recursive function is identical to the iterative version. Only the approach has changed.
Now we have to do a binary search, it is interesting to ask what this function is. We again say that the array has $n$ elements in. The worst case is the situation when the element is not found, and we get down to one element in the range we are looking for. So we need to figure out how many comparisons have to narrow the range down from $n$ to 1. After one comparison the range is cut to $n/2$. After two comparisons t, there are roughly $n/2^t$ elements left in the range.$^9$ In general, after $t$ comparisons. We have enough information to find the maximum number of comparisons.

$n/2^t = 1
n = 2^t
t = \log_2 n$

This is typically $O(\log n)$ as the difference between logs of different bases is simply a constant multiplier. This order is generally considered to be quite fast, as it grows slowly as the input gets bigger.

To get a feel for this, let us look at a few examples of how $\log_2 n$ scales with $n$. A list of approximate values for this is given in table 13.1. To really put this in perspective, consider that the first number is the worst case for a sequential search, and the second number is the worst case for a binary search. When $n$ is small, the difference is not all significant. However, as $n$ gets larger the cost savings of a binary search become quite apparent. The last two values of $n$ are large enough to pose them a problem even for computers, despite their speed.

Of course, you can only use a binary search on sorted data and attempting an $O(n^2)$ sort on even a million items can be time consuming. The real power of this $O(\log n)$ scaling is purely academic until we discuss some other ways to sort.

> $^9This is only exact if $n$ is a power of two. Otherwise, some rounding will occur, but that is a detail we can ignore when talking about the order.
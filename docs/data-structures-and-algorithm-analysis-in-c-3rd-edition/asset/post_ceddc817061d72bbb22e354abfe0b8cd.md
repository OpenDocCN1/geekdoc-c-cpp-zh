
```cpp
// Return the minimum and maximum values in A
// between positions l and r
template <typename E>
void MinMax(E A[], int l, int r, E& Min, E& Max) {
    if (l == r) {        // n=1
        Min = A[r];
        Max = A[r];
    }
    else if (l+1 == r) { // n=2
        Min = min(A[l], A[r]);
        Max = max(A[l], A[r]);
    }
    else {              // n>2
        int Min1, Min2, Max1, Max2;
        int mid = (l + r)/2;
        MinMax(A, l, mid, Min1, Max1);
        MinMax(A, mid+1, r, Min2, Max2);
        Min = min(Min1, Min2);
        Max = max(Max1, Max2);
    }
}
```

**Figure 15.3** Recursive algorithm for finding the minimum and maximum values in an array.

For example, what if we have six items in the list? If we break the list into two sublists of three elements, the cost would be 8. If we break the list into a sublist of size two and another of size four, then the cost would only be 7.

With divide and conquer, the best algorithm is the one that minimizes the work, not necessarily the one that balances the input sizes. One lesson to learn from this example is that it can be important to pay attention to what happens for small sizes of n, because any division of the list will eventually produce many small lists.

We can model all possible divide-and-conquer strategies for this problem with the following recurrence.

```
T(n) = { 0                     n = 1
         1                     n = 2
         min_{1 ≤ k ≤ n-1} { T(k) + T(n - k) } + 2   n > 2 }
```

That is, we want to find a way to break up the list that will minimize the total work. If we examine various ways of breaking up small lists, we will eventually recognize that breaking the list into a sublist of size 2 and a sublist of size n − 2 will always produce results as good as any other division. This strategy yields the following recurrence.

```
T(n) = { 0          n = 1
         1          n = 2
         T(n - 2) + 3   n > 2 }
```

This recurrence (and the corresponding algorithm) yields T(n) = ⌈3n/2⌉ − 2 comparisons. Is this optimal? We now introduce yet another tool to our collection of lower bounds proof techniques: The state space proof.

We will model our algorithm by defining a state that the algorithm must be in at any given instant. We can then define the start state, the end state, and the transitions between states that any algorithm can support. From this, we will reason about the minimum number of states that the algorithm must go through to get from the start to the end, to reach a state space lower bound.

At any given instant, we can track the following four categories of elements:

- Untested: Elements that have not been tested.
- Winners: Elements that have won at least once, and never lost.
- Losers: Elements that have lost at least once, and never won.
- Middle: Elements that have both won and lost at least once.

We define the current state to be a vector of four values, (U, W, L, M) for untested, winners, losers, and middles, respectively. For a set of n elements, the initial state of the algorithm is (n, 0, 0, 0) and the end state is (0, 1, 1, n − 2). Thus, every run for any algorithm must go from state (n, 0, 0, 0) to state (0, 1, 1, n − 2). We also observe that once an element is identified to be a middle, it can then be ignored because it can neither be the minimum nor the maximum.

Given that there are four types of elements, there are 10 types of comparison. Comparing with a middle cannot be more efficient than other comparisons, so we should ignore those, leaving six comparisons of interest. We can enumerate the effects of each comparison type as follows. If we are in state (i, j, k, l) and we have a comparison, then the state changes are as follows.

| Comparison | State change (i, j, k, l) |
|---|---|
| U : U | (i − 2, j + 1, k + 1, l) |
| W : W | (i, j − 1, k, l + 1) |
| L : L | (i, j, k − 1, l + 1) |
| L : U | (i − 1, j + 1, k, l) or (i − 1, j, k, l + 1) |
| W : U | (i − 1, j, k + 1, l) or (i − 1, j, k, l + 1) |
| W : L | (i, j, k, l) or (i, j − 1, k − 1, l + 2) |

Now, let us consider what an adversary will do for the various comparisons. The adversary will make sure that each comparison does the least possible amount of work in taking the algorithm toward the goal state. For example, comparing a winner to a loser is of no value because the worst case result is always to learn nothing new (the winner remains a winner and the loser remains a loser). Thus, only the following five transitions are of interest:

| Comparison | State change (i, j, k, l) |
|---|---|
| U : U | (i − 2, j + 1, k + 1, l) |
| L : U | (i − 1, j + 1, k, l) |
| W : U | (i − 1, j, k + 1, l) |
| W : W | (i, j − 1, k, l + 1) |
| L : L | (i, j, k − 1, l + 1) |

Only the last two transition types increase the number of middles, so there must be n − 2 of these. The number of untested elements must go to 0, and the first transition is the most efficient way to do this. Thus, ⌈n/2⌉ of these are required. Our conclusion is that the minimum possible number of transitions (comparisons) is n + ⌈n/2⌉ − 2. Thus, our algorithm is optimal.

## 15.6 Finding the i th Best Element

We now tackle the problem of finding the i th best element in a list. As observed earlier, one solution is to sort the list and simply look in the i th position. However, this process provides considerably more information than we need to solve the problem. The minimum amount of information that we actually need to know can be visualized as shown in Figure 15.4.

![](img/7ea3c39173f146f675b63b146d1535f3_525_0.png)

**Figure 15.4** The poset that represents the minimum information necessary to determine the i th element in a list. We need to know which element has i − 1 values less and n − i values more, but we do not need to know the relationships among the elements with values less or greater than the i th element.

That is, all we need to know is the i − 1 items less than our desired value, and the n − i items greater. We do not care about the relative order within the upper and lower groups. So can we find the required information faster than by first sorting? Looking at the lower bound, can we tighten that beyond the trivial lower bound of n comparisons? We will focus on the specific question of finding the median element (i.e., the element with rank n/2), because the resulting algorithm can easily be modified to find the i th largest value for any i.

Looking at the Quicksort algorithm might give us some insight into solving the median problem. Recall that Quicksort works by selecting a pivot value, partitioning the array into those elements less than the pivot and those greater than the pivot, and moving the pivot to its proper location in the array. If the pivot is in position i, then we are done. If not, we can solve the subproblem recursively by only considering one of the sublists. That is, if the pivot ends up in position k > i, then we simply solve by finding the ith best element in the left partition. If the pivot is at position k < i, then we wish to find the i − kth element in the right partition.

What is the worst case cost of this algorithm? As with Quicksort, we get bad performance if the pivot is the first or last element in the array. This would lead to possibly O(n²) performance. However, if the pivot were to always cut the array in half, then our cost would be modeled by the recurrence T(n) = T(n/2) + n = 2n or O(n) cost.

Finding the average cost requires us to use a recurrence with full history, similar to the one we used to model the cost of Quicksort. If we do this, we will find that T(n) is in O(n) in the average case.

Is it possible to modify our algorithm to get worst-case linear time? To do this, we need to pick a pivot that is guaranteed to discard a fixed fraction of the elements. We cannot just choose a pivot at random, because doing so will not meet this guarantee. The ideal situation would be if we could pick the median value for the pivot each time. But that is essentially the same problem that we are trying to solve to begin with.

Notice, however, that if we choose any constant c, and then if we pick the median from a sample of size n/c, then we can guarantee that we will discard at least n/2c elements. Actually, we can do better than this by selecting small subsets of a constant size (so we can find the median of each in constant time), and then taking the median of these medians. Figure 15.5 illustrates this idea.

![](img/7ea3c39173f146f675b63b146d1535f3_526_0.png)

![](img/7ea3c39173f146f675b63b146d1535f3_526_1.png)

**Figure 15.5** A method for finding a pivot for partitioning a list that guarantees at least a fixed fraction of the list will be in each partition. We divide the list into groups of five elements, and find the median for each group. We then recursively find the median of these n/5 medians. The median of five elements is guaranteed to have at least two in each partition. The median of three medians from a collection of 15 elements is guaranteed to have at least five elements in each partition.

This observation leads directly to the following algorithm.

- Choose the n/5 medians for groups of five elements from the list. Choosing the median of five items can be done in constant time.
- Recursively, select M, the median of the n/5 medians-of-fives.
- Partition the list into those elements larger and smaller than M.

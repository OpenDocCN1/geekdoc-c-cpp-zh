# Solutions to Chapter 8 | Recursion

8.3 Write a method that returns all subsets of a set.

# SOLUTION

We should first have some reasonable expectations of our time and space complexity. How many subsets of a set are there? We can compute this by realizing that when we generate a subset, each element has the "choice" of being in or not that. For the first element, there are 2 choices. For the second, there are two, etc. So, doing 2 * ... * n times gives us 2^n subsets. We will not be able to do better than this in time or space complexity.

Approach #1: Recursion

This is a great problem to implement with recursion since we can build subsets of a smaller set. Specifically, given a set S, we can do the following recursively:

+   - Let first=S(0). Let smallerSet=S(1, ... n).

+   - Compute all subsets of smallerSet and put them in subsets

+   - For each subset in subsetslist, clone it and add first to the subset.

The following code implements this algorithm:

```
1 ArrayList<ArrayList<Integer>> getSubsets(ArrayList<Integer> set,
2                                int index) {
3     ArrayList<Integer> subsets;
4     if (set.size() == index) {
5         subsets = new ArrayList<ArrayList<Integer>>();
6         subsets.add(new ArrayList<Integer>()); // Empty set
7     } else {
8         subsets = getSubsets(index, index + 1);
9         int item = set.get(index);
10    ArrayList<Integer> moresubsets = =
11        new ArrayList<ArrayList<Integer>>();
12    for (ArrayList<Integer> subset : subsets) {
13        ArrayList<Integer> newsubset = new ArrayList<Integer>();
14        newsubset.addAll(subset); //
15        newsubset.add(item);
16        moresubsets.add(newsubset);
17    }
18    subsets.addAll(moresubsets);
19    }
20    return subsets;
21 }
```

Approach #2: Combinatorics

+   - When we're generating a set, we have two choices for each element: (1) the element is
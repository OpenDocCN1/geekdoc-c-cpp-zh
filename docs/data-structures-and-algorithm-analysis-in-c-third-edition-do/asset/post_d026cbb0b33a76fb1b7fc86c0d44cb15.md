
# 513

things by assuming that each game takes less than an hour, and each team
can be scheduled for a game every hour if necessary. (Note that everything
said about basketball courts is also true about processors in a parallel
algorithm to solve the maximum-finding problem).

- (a) How many basketball courts do we need to insure that every team can
play whenever we want to minimize the total tournament time?
- (b) How long will the tournament be in this case?
- (c) What is the total number of "court-hours" available? How many total
hours are being used? How many total court-hours are unused?
- (d) Modify the algorithm in such a way as to reduce the total number of
courts needed, by perhaps not letting every team play whenever possible. This will increase the total hours of the tournament, but try to keep to increase as low as possible. For your new algorithm, how many total court-hours
are, how many court-hours are used, and how many unused?

**15.3** Explain the cost of splitting a list of six into two lists to find the
minimum and maximum elements requires eight comparisons, while splitting-
the list into a list of two and a list of four only seven comparisons.

**15.4** Write a table showing the number of comparisons required to find the
minimum and maximum for divisions for all values of $n \le 13$.

**15.5** Present an adversary argument as a lower bounds proof to show that $n-1$
comparisons are necessary to find the maximum of $n$ values in the worst case.

**15.6** Present an adversary argument as a lower bounds proof to show that $n$ comparisons are necessary in the worst case when searching for an element
from $x$ (if one exists) from $n$ elements.

**15.7** Section 16 claims that by picking a pivot that always discards at least
a fraction of the remaining array, the resulting algorithm will be linear.
Explain why this is true. Hint: The Master Theorem (Theorem 14.1) might
help you.

**15.8** Show that any comparison-based algorithm for finding the median must use
at least $n-1$ comparisons.

**15.9** Show that any comparison-based algorithm for finding the second-smallest
of $n$ values can be extended to find the smallest value, without requiring
more comparisons to be performed.

**15.10** Show that any comparison-based algorithm for sorting can be modified
to remove all duplicates without requiring any more comparisons to per-formed.

**15.11** Show that any comparison-based algorithm for removing duplicates from a
list of values must use $\Omega(n \log n)$ comparisons.

**15.12** Given a list of $n$ elements, an element of the list is a *majority* if it appears
more than $n/2$ times.

- (a) Assume that the input is a list of integers. Design an algorithm that is linear in the number of integer-integer comparisons in the worst case that will find and report the majority if one exists, and report that there is no majority if no such element exists in the list.

- (b) Assume that the input is a list of elements that have no relative ordering, such as colors or fruit. So all that you can do when you compare two elements is if they are the same or not. Design an algorithm that is linear in the number of element-element comparisons in the worst case that will find a majority if one exists, and report that there is no majority element exists in the list.

**15.13** Given an undirected graph G, the problem is to determine whether or not is connected. Use an adversary argument to prove that it is necessary to look at all $(n^2 - n)/2$ potential edges in the worst case.

**15.14** Write an equation that describes the average cost for finding the median.

- (b) Solve your equation from part (a).

- (a) Write an equation that describes the average cost for finding the-smallest value in an array. This will be a function of both $n$ and $i$, **T(n, i).**

- (b) Solve your equation from part (a).

**15.16** Suppose that you have $n$ objects that have identical weight, except for one that is a bit heavier than the others. You have a balance scale. You can place objects on each side of the scale and see which collection is heavier. Your goal is to find the heavier object, with the minimum number of weights. Find and prove matching upper and lower bounds for this problem.

**15.17** Imagine that you are organizing a basketball tournament for 10 teams. Know the merge sort will give you a full ranking of the 10 teams with the minimum number of games played. Assume that each game can be played in less than an hour, and that each team can play as many games in a row as necessary. Show a schedule for this tournament that also attempts to minimize the total of hours and the number of courts used. If you have to make a tradeoff between the two, then attempt to minimize the total number of hours that basketball courts are idle.

**15.18** Write the complete algorithm for the merge sort sketched out in Sec-15.7.

**15.19** Here is a suggestion for what might be a truly optimal sorting algorithm. Pick the best set of comparisons for input lists of size 2. Pick the best set of comparisons for size 3, size 4, size 5, and so on. Combine them together one program with a big case statement. Is this an algorithm?

# 15.10 Projects

15.1 Implement the median-finding algorithm of Section 15.6. Then, modify this algorithm to allow finding the $i$th element for any value $i < n$.

# Patterns of Algorithms

This chapter presents several fundamental topics to the theory of algorithms. Included are dynamic programming (Section 16.1), randomized algorithms (Section 16.2), and the concept of a transform (Section 16.3.5). Each of these can be viewed as an example of an "algorithmic pattern" that is commonly used for a wide variety of applications. In addition, Section 16.3 presents a number of numerical algorithms. Section 16.2 on randomized algorithms includes the Skip List (Section 16.2.2). The Skip List is a probabilistic data structure that can be used to implement the dynamic ADT. The Skip List is no more complicated than the BST. Yet it outperforms the BST because the Skip List's efficiency is not tied to the values or insertion order of the dataset being used.

# 16.1 Dynamic Programming

```c
long fibr(int n) { // Recursive Fibonacci generator
// fibr(46) is largest value that fits in a long
assert(n > 0 && (n < 47), "Input out of range");
if (n == 1 || (n == 2)) return 1; // Base cases
    return fibr(n-1) + fibr(n-2);
} // Recursion
```

The cost of this algorithm (in terms of calls) is the size of the nth Fibonacci number itself, which our analysis of Section 14.2 shows to be exponential (approximately $n^{1.62}$). Why is this expensive? Primarily two recursive calls are made by the function, and the work that they do is largely redundant. That is, each of the two calls is recomputing most of the series, as is each sub-call, and so on. The smaller the values of the function being recomputed a huge number of times. If we could eliminate this redundancy, the cost would be greatly reduced. The approach that we will use improve any algorithm that spends most of time recomputing subproblems.

One way to accomplish this goal is to keep a table of values, and first check the table to see if the computation can be avoided. Here is a straightforward example of doing so.

```c
int Fib(int n, int Values[]) {
    // Values has at least n slots, and all
    // slots are initialized to 0
    if (n <= 1) return 1; // Base case
    if (Values[n] == 0)
        Values[n] = Fib(n-1, Values) + Fib(n-2, Values);
    return Values[n];
}
```

This version of the algorithm will not compute a value more than once, so its cost could be linear. Of course we didn't actually need to use a table storing all values, since future computations not need access to all subproblems. Instead, we could build the value by working from 0 and 1 up to n rather than backwards from n down to 1.

```c
long fibi(int n) { // Iterative Fibonacci generator
    if (n < 46) // largest value that fits in a long
        assert((n > 0) && (n < 47), "Input out of range");
        long past, prev, curr; // Store temporary values
        prev = curr = 1; // Initialize
        for (int i=3; i<=n; i++) { // past holds fibi(i-2)
            past = prev;
            prev = curr; // prev holds fibi(i-1)
            curr = past + prev; // curr now holds fibi(i)
        }
    return curr;
}
```

Practice It Now you can try these exercises at the end of the chapter: R6.14, P6.8, P6.12.

> Special Topic 6.4

![](bbox=[0.14, 0.16, 0.23, 0.23])

# Constant Array Parameters

When a function doesn't modify an array parameter, it is considered good style to add the const reserved word, like this:

```
double sum(const double values[], int size)
```

The const reserved word helps the reader of the code, making it clear that the function keeps the array elements unchanged. If the implementation of the function tries to modify the array, the compiler issues a warning.

# 6.4 Problem Solving: Adapting Algorithms

> By combining fundamental algorithms, you can solve complex programming tasks.

In Section 6.2, you were introduced to a number of fundamental array algorithms. These algorithms form the building blocks for many programs that process arrays. In general, it is a good problem-solving strategy to have a repertoire of fundamental algorithms that you can combine and adapt.

Consider this example problem: You are given the quiz scores of a student. You are to compute the final quiz score, which is the sum of all scores after dropping the lowest one. For example, if the scores are

```
8  7  8.5  9.5  7  4  10
```

then the final score is 50.

We do not have a ready-made algorithm for this situation. Instead, consider which algorithms may be related. These include:

+   - Calculating the sum (Section 6.2.3)
+   - Finding the minimum value (Section 6.2.4)
+   - Removing an element (Section 6.2.7)

Now we can formulate a plan of attack that combines these algorithms.

```
Find the minimum.
Remove it from the array.
Calculate the sum.
```

Let's try it out with our example. The minimum of

| [0] | [1] | [2] | [3] | [4] | [5] | [6] |
|---|---|---|---|---|---|---|
| 8 | 7 | 8.5 | 9.5 | 7 | 4 | 10 |

is 4. How do we remove it?

Now we have a problem. The removal algorithm in Section 6.2.7 locates the element to be removed by using the position of the element, not the value.

But we have another algorithm for that:

+   - Linear search (Section 6.2.6)
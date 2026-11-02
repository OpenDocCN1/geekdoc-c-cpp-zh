# Program Run

```
Please enter values, 0 to quit:
12 25 20 0
24, 50, 40
```

# Special Topic 6.4

# Constant Array Parameters

When a function doesn't modify an array parameter, it is considered good style to add the const reserved word, like this:

```
double sum(const double values[], int size)
```

The const reserved word helps the reader of the code, making it clear that the function keeps the array elements unchanged. If the implementation of the function tries to modify the array, the compiler issues a warning.

# 6.4 Problem Solving: Adapting Algorithms

By combining fundamental algorithms, you can solve complex programming tasks.

In Section 6.2, you were introduced to a number of fundamental array algorithms. These algorithms form the building blocks for many programs that process arrays. In general, it is a good problem-solving strategy to have a repertoire of fundamental algorithms that you can combine and adapt.

Consider this example problem: You are given the quiz scores of a student. You are to compute the final quiz score, which is the sum of all scores after dropping the lowest one. For example, if the scores are
8 7 8.5 9.5 7 4 10
then the final score is 50.

We do not have a ready-made algorithm for this situation. Instead, consider which algorithms may be related. These include:

+   - Calculating the sum (Section 6.2.3)
+   - Finding the minimum value (Section 6.2.4)
+   - Removing an element (Section 6.2.8)

![](bbox=[0.45, 0.88, 0.8, 0.95])

is 4. How do we remove it? Now we have a problem. The removal algorithm in Section 6.2.8 locates the element to be removed by using the position of the element, not the value. But we have another algorithm for that:

+   - Linear search (Section 6.2.7)
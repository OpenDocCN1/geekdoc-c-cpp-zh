![](bbox=[0.077, 0.091, 0.228, 0.182])

+   5. Approximately how many seconds would it take to sort a data set of 80,000 values?
+   6. Look at the graph in Figure 1. What mathematical shape does it resemble?

**Practice It**  Now you can try these exercises at the end of the chapter: P12.3.

# 12.3 Analyzing the Performance of the Selection Sort Algorithm

Let us count the number of operations that a program must carry out to sort an array using the selection sort algorithm. Actually, we don’t know how many machine operations are generated for each C++ instruction or which of those instructions are more time-consuming than others, but we can make a simplification. Simply count how often an element is visited. Each visit requires about the same amount of work by other operations, such as incrementing subscripts and comparing values.

Let *n* be the size of the array. First, you must find the smallest of *n* numbers. To achieve this, you must visit *n* elements. Then swap the elements, which takes two visits. (You may argue that there is a certain probability that you don’t need to swap the values. That is true, and one can refine the computation to reflect that observation. As we will soon see, doing so would not affect the overall conclusion.) In the next step, you need to visit only *n* − 1 elements to find the minimum and then visit two of them to swap them. In the following step, *n* − 2 elements are visited to find the minimum. The last run visits two elements to find the minimum and requires two visits to swap the elements. Therefore, the total number of visits is

$$n + 2 + (n - 1) + 2 + \cdots + 2 + 2 = n + (n - 1) + \cdots + 2 + (n - 1) \cdot 2$$
$$= 2 + (n - 1) + n + (n - 1) \cdot 2$$
$$= \frac{n(n+1)}{2} - 1 + (n - 1) \cdot 2$$

because

$$1 + 2 + \cdots + (n - 1) + n = \frac{n(n+1)}{2}$$

After multiplying out and collecting terms of *n*, you find that the number of visits is

$$\frac{1}{2}n^2 + \frac{5}{2}n - 3$$

This is a quadratic equation in *n*. That explains why the graph of Figure 1 looks approximately like a parabola.

Now simplify the analysis further. When you plug in a large value for *n* (for example, 1,000 or 2,000), then $\frac{1}{2}n^2$ is 500,000 or 2,000,000. The lower term, $\frac{5}{2}n - 3$, doesn’t contribute much at all; it is just 2,497 or 4,997, a drop in the bucket compared to the hundreds of thousands or even millions of comparisons specified by the $\frac{1}{2}n^2$ term.
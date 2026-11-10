or obvious, but sometimes it becomes as important an issue as time. It is denoted as $S(n)$, where $n$ is the size of the input.

# Complexity analysis

Complexity analysis attempts to characterize the relationship between the number of data elements and the resource usage (time or space) with a simple formula approximation. Using the RAM model of computation, one can count the number of steps required for an algorithm for executing a program based on the input provided. However, to really understand how good or bad an algorithm is, one must know how it works over all instances. There are three terms to describe these situations:

+   - The **worst-case complexity** of the algorithm is the function defined by the maximum number of steps taken on any instance of input size $n$.
+   - The **best-case complexity** of the algorithm is the function defined by the minimum number of steps taken on any instance of input size $n$.
+   - Finally, the **average-case complexity** of the algorithm is the function defined by the average number of steps taken on any instance of input size $n$.

Every input instance can be represented as a point on a graph, where the x-axis is the size of the problem (for sorting, the number of items to sort) and the y-axis is the number of steps taken by the algorithm on this instance. Worst-case complexity is represented by the curve passing through the highest point of each column. The curve passing through the lowest point of each column represents the best-case complexity.

The average case is probably the most important, but it is problematic. One has to make some assumptions about the probabilities, and the analysis will only be as accurate as the validity of the assumptions. In some cases, the average complexity is established by considering possible inputs to an algorithm, for each input, adding the number of steps for all the inputs and dividing by the number of inputs. Here, it is assumed that the possibility of the occurrence of each input is the same, which will not always be the case. To consider the probability explicitly, the average complexity is defined as the average over the number of steps executed when processing each input weighted by the probability of occurrence of this input.

If a function is linear, that is, if it contains no loops, then its efficiency is a function of the number of instructions it contains. In this case, its efficiency is dependent on the speed of the computer. On the other hand, functions that contain loops will vary widely in their efficiency. The study of algorithm efficiency is, therefore, largely devoted to the study of loops. The efficiency of an algorithm can be expressed as a function of the number of elements or inputs to be processed. The general format is

```
f(n) ≈ efficiency
```

Loops can be of various types. Let us discuss these in detail.

# Linear loops

Consider the following simple loop.

```
for(i=1;i<=n;++i)    for(i=0;i<n;++i)
{
  stmTs                stmTs
}
```

The body of the loop will be repeated for $n$ times. In the following loop,

```
for(i=1;i<n; i=i+2)
{
  stmTs
}
```

the body of the loop will be executed $n/2$ times. In all of the above cases, the number of iterations is directly proportional to a factor. The higher the factor, the higher will be the number of iterations. If either of these loops was plotted, one would get a straight line. Hence such loops are known as linear loops. Because the efficiency is proportional to the number of iterations, it is

```
f(n) = n
```

# Logarithmic loops

Now, the following loops are to be considered in which the controlling variable is multiplied or divided in each iteration.

```
Multiply loop                 Divide loop
for(i=1; i<n; i=i*2)          for(i=n; i>=1; i=i/2)
{
  stmTs                       {
}                               stmTs
                              }
```

Let $n = 10$; the number of iterations in both cases is 4. The reason is that in each iteration the value of $i$ doubles for the multiply loop and is cut in half for the divide loop. The number of iterations is a function of the multiplier or divisor. The loop continues till the following condition is true.

+   - For the multiply loop, $2^{iteration} < n$
+   - For the divide loop, $n/2^{iteration} \geq 1$
+   - Generalizing the analysis, $f(n) = [\log_2 n]$

# Nested loop

For the nested loop, the total number of iterations would be the product of the number of iterations for the inner loop and the number of iterations for the outer loop. There are various types of nested loops, namely quadratic, dependent quadratic, linear logarithmic, etc.

# Quadratic loop

Here, each of the loops iterates the same number of times as shown in the following code.

```
for(i=1;i<=n;i++)
  for(j=1;j<=n;j++)
  {
    stmTs
  }
```
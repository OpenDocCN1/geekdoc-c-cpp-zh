
```cpp
50       if (min_pos != next)
51       {
52          swap(a[min_pos], a[next]);
53       }
54    }
55 }
56
57 /*
58    Prints all elements in an array.
59    @param a the array to print
60    @param size the number of elements in a
61 */
62 void print(int a[], int size)
63 {
64    for (int i = 0; i < size; i++)
65    {
66       cout << a[i] << " ";
67    }
68    cout << endl;
69 }
70
71 int main()
72 {
73    srand(time(0));
74    const int SIZE = 20;
75    int values[SIZE];
76    for (int i = 0; i < SIZE; i++)
77    {
78       values[i] = rand() % 100;
79    }
80    print(values, SIZE);
81    selection_sort(values, SIZE);
82    print(values, SIZE);
83    return 0;
84 }
```

## Program Run

```text
60 47 70 39 6 12 96 93 83 53 36 29 50 97 94 95 38 17 8 26
6 8 12 17 26 29 36 38 39 47 50 53 60 70 83 93 94 95 96 97
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_541_0.png)

- 1. What steps does the selection sort algorithm go through to sort the array 6 5 4 3 2 1?
- 2. How can you change the selection sort algorithm so that it sorts the elements in descending order (that is, with the largest element at the beginning of the array)?
- 3. Suppose we modified the selection sort algorithm to start at the end of the array, working toward the beginning. In each step, the current position is swapped with the minimum. What is the result of this modification?
- 4. Why do we need the temp variable in the swap function? What would happen if you simply assigned a[i] to a[j] and a[j] to a[i]?

**Practice It** Now you can try these exercises at the end of the chapter: R12.1, P12.1, P12.2.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_543_0.png)

- 5. Approximately how many seconds would it take to sort a data set of 80,000 values?
- 6. Look at the graph in Figure 1. What mathematical shape does it resemble?

**Practice It** Now you can try these exercises at the end of the chapter: P12.3.

## 12.3 Analyzing the Performance of the Selection Sort Algorithm

Let us count the number of operations that a program must carry out to sort an array using the selection sort algorithm. Actually, we don’t know how many machine operations are generated for each C++ instruction or which of those instructions are more time-consuming than others, but we can make a simplification. Simply count how often an element is visited. Each visit requires about the same amount of work by other operations, such as incrementing subscripts and comparing values.

Let *n* be the size of the array. First, you must find the smallest of *n* numbers. To achieve this, you must visit *n* elements. Then swap the elements, which takes two visits. (You may argue that there is a certain probability that you don’t need to swap the values. That is true, and one can refine the computation to reflect that observation. As we will soon see, doing so would not affect the overall conclusion.) In the next step, you need to visit only *n* − 1 elements to find the minimum and then visit two of them to swap them. In the following step, *n* − 2 elements are visited to find the minimum. The last run visits two elements to find the minimum and requires two visits to swap the elements. Therefore, the total number of visits is

$$n + 2 + (n - 1) + 2 + \cdots + 2 + 2 = n + (n - 1) + \cdots + 2 + (n - 1) \cdot 2$$
$$= (1 + 2 + \cdots + n) - 1 + (n - 1) \cdot 2$$
$$= \frac{n(n+1)}{2} - 1 + (n - 1) \cdot 2$$

because

$$1 + 2 + \cdots + (n - 1) + n = \frac{n(n+1)}{2}$$

After multiplying out and collecting terms of *n*, you find that the number of visits is

$$\frac{1}{2}n^2 + \frac{5}{2}n - 3$$

This is a quadratic equation in *n*. That explains why the graph of Figure 1 looks approximately like a parabola.

Now simplify the analysis further. When you plug in a large value for *n* (for example, 1,000 or 2,000), then $\frac{1}{2}n^2$ is 500,000 or 2,000,000. The lower term, $\frac{5}{2}n - 3$, doesn’t contribute much at all; it is just 2,497 or 4,997, a drop in the bucket compared to the hundreds of thousands or even millions of comparisons specified by the $\frac{1}{2}n^2$ term. Just ignore these lower-level terms. Next, ignore the constant factor \( \frac{1}{2} \). You need not be interested in the actual count of visits for a single \(n\). You need to compare the ratios of counts for different values of \(n^2\). For example, you can say that sorting an array of 2,000 numbers requires four times as many visits as sorting an array of 1,000 numbers:

\[
\frac{\frac{1}{2}\cdot 2000^2}{\frac{1}{2}\cdot 1000^2}=4
\]

The factor \( \frac{1}{2} \) cancels out in comparisons of this kind. We will simply say, “The number of visits is of order \(n^2\).” That way, we can easily see that the number of comparisons increases fourfold when the size of the array doubles: \((2n)^2 = 4n^2\).

To indicate that the number of visits is of order \(n^2\), computer scientists often use *big-Oh notation*: The number of visits is \(O(n^2)\). This is a convenient shorthand.

To turn an exact expression such as

\[
\frac{1}{2}n^2+\frac{5}{2}n-3
\]

into big-Oh notation, simply locate the fastest-growing term, \(n^2\), and ignore its constant coefficient, \( \frac{1}{2} \) in this case, *no matter how large or small it may be*.

> Computer scientists use big-Oh notation to describe how fast a function grows.

In general, the expression \(f(n)=O(g(n))\) means that \(f\) grows no faster than \(g\), or, more formally, that for all \(n\) larger than some threshold, the ratio \(f(n)/g(n)\) is less than a constant value \(C\). The function \(g\) is usually chosen to be very simple, such as \(n^2\) in our example.

> Selection sort is an \(O(n^2)\) algorithm. Doubling the data set means a fourfold increase in processing time.

You observed before that the actual number of machine operations, and the actual amount of time that the computer spends on them, is approximately proportional to the number of element visits. Maybe there are about 10 machine operations (increments, comparisons, memory loads, and stores) for every element visit. The number of machine operations is then approximately \(10 \times \frac{1}{2}n^2\). As before, we aren’t interested in the coefficient, so we can say that the number of machine operations, and hence the time spent on the sorting, is of the order of \(n^2\) or \(O(n^2)\).

The sad fact remains that doubling the size of the array causes a fourfold increase in the time required for sorting it. When the size of an array increases by a factor of 100, the sorting time increases by a factor of 10,000. To sort an array of a million entries (for example, to create a telephone directory), takes 10,000 times as long as sorting 10,000 entries. If 10,000 entries can be sorted in about a second (as in our example), then sorting one million entries requires almost three hours. You will see in the next section how one can dramatically improve the performance of the sorting process by choosing a more sophisticated algorithm.

**SELF CHECK**

- 7. If you increase the size of a data set tenfold, how much longer does it take to sort it with the selection sort algorithm?
- 8. How large does \(n\) need to be so that \( \frac{1}{2}n^2 \) is bigger than \( \frac{5}{2}n - 3 \)?
- 9. Section 6.2.7 has two algorithms for removing an element from an array of length \(n\). How many array visits does each algorithm require on average?
- 10. Describe the number of array visits in Self Check 9 using the big-Oh notation.

```cpp
// Copy any remaining entries of the first half
while (i1 <= mid)
{
   b[j] = a[i1];
   i1++;
   j++;
}

// Copy any remaining entries of the second half
while (i2 <= to)
{
   b[j] = a[i2];
   i2++;
   j++;
}

// Copy back from the temporary array
for (j = 0; j < n; j++)
{
   a[from + j] = b[j];
}

// The temporary array is no longer needed
delete[] b;
}

/**
   Sorts the elements in a range of an array.
   @param a the array with the elements to sort
   @param from start of the range to sort
   @param to end of the range to sort
*/
void merge_sort(int a[], int from, int to)
{
   if (from == to) { return; }
   int mid = (from + to) / 2;
   // Sort the first half and the second half
   merge_sort(a, from, mid);
   merge_sort(a, mid + 1, to);
   merge(a, from, mid, to);
}

/**
   Prints all elements in an array.
   @param a the array to print
   @param size the number of elements in a
*/
void print(int a[], int size)
{
   for (int i = 0; i < size; i++)
   {
      cout << a[i] << " ";
   }
   cout << endl;
}

int main()
{
   srand(time(0));
   const int SIZE = 20;
   int values[SIZE];
```

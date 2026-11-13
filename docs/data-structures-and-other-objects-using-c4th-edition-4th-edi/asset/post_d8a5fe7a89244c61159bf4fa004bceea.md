
## Insertionsort Running Time

Both the worst-case running time and the average-case running times are quadratic. But the best-case (when the starting array is already sorted) is linear, and the algorithm is also quick when the starting array is nearly sorted.

## Self-Test Exercises for Section 13.1

- 1. Compare the worst-case, average-case, and best-case running times for selectionsort and insertionsort.
- 2. Show the following array after each iteration of selectionsort, using the largest element version of swapping: 5 19 13 36 2 3
- 3. Show the following array after each iteration of insertionsort: 5 19 13 36 23 2
- 4. Give a complete function implementation for insertionsort.
- 5. The selectionsort function in Figure 13.1 on page 633 sorts integers into increasing order. How would you change the function so that it sorts integers into decreasing order?
- 6. The selectionsort function in Figure 13.1 on page 633 sorts integers into increasing order. How would you change the function so that it sorts an array of lowercase strings into alphabetical order?

## 13.2 RECURSIVE SORTING ALGORITHMS

### Divide-and-Conquer Using Recursion

Key Design Concept
Divide-and-conquer works best with two equally sized subproblems, each of which is solved with a recursive call.

Let's start with an explicit statement of a recursive design technique called divide-and-conquer. Here's the idea: When a problem is small, simply solve it. When the problem is large, divide the problem into two smaller subproblems, each of which is about half of the original problem. Solve each subproblem with a recursive call. After the recursive calls, extra work is often needed to combine the solutions of the smaller problems, resulting in a solution to the larger problem.

Divide-and-conquer can work in slightly different ways, perhaps having more than two subproblems or having subproblems with unequal size, but the basic approach—two subproblems with roughly equal size—works best. Applied to sorting, divide-and-conquer results in the following pattern:

### The Divide-and-Conquer Sorting Paradigm

- 1. Divide the elements to be sorted into two groups of equal (or almost equal) size.
- 2. Sort each of these smaller groups of elements (by recursive calls).
- 3. Combine the two sorted groups into one large sorted list.

As an illustration, we can see how these three steps will sort a small array. The first step divides the array into two equally sized groups, as shown in this cut:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_670_0.png)

After the cut, we have two smaller arrays, with five elements each. These smaller arrays can separately be sorted with recursive calls, providing this result:

| 5 | 9 | 12 | 25 | 31 | | 2 | 3 | 6 | 8 | 20 |

When the recursive calls return, the two half-arrays somehow need to be put together into one sorted array, as shown here:

| 2 | 3 | 5 | 6 | 8 | 9 | 12 | 20 | 25 | 31 |

We will present two recursive sorting functions based on this divide-and-conquer paradigm. But first there is a C++ feature that we will discuss to make the recursive calls easier.

## C++ FEATURE

### Specifying a Subarray with Pointer Arithmetic

Our sorting functions will require recursive calls to sort various portions of the array. This raises an interesting problem regarding the arguments of a sorting function. As an example of the problem, look at the specification of one of our sorts:

```
void selectionsort(int data[], size_t n);
// Precondition: data is an array with at least n components.
// Postcondition: The elements of data have been rearranged so
// that data[0] <= data[1] <= ... <= data[n-1].
```

Is it possible to use this function to sort only part of an array? Certainly we can sort the first part of an array. For example, suppose that data is an array of 10 integers. This function call will sort the first five elements of data:

```
selectionsort(data, 5);
```

This function call will rearrange the elements data[0] through data[4] so that the values are smallest to largest. But can we use the function to sort the second part of the array (from data[5] through data[9]) or a middle piece (such as data[2] through data[6])? The answer is yes, but we'll need a C++ feature called pointer arithmetic.

To illustrate pointer arithmetic, we'll continue with our array, data, of 10 integers. Suppose that data has these values:

| data |
| --- |
| 9 | 12 | 31 | 25 | 5 | 8 | 20 | 11 | 3 | 6 |
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

For any value i from 0 to 9, the expression data[i] refers to one of the 10 components. For example, data[5] refers to the value 8 in the array. This is not new. But another use of the index i is new: For any value i from 0 to 9, the expression (data + i) refers to the small array that starts at data[i] and continues to the end of the array. For example, (data + 5) refers to that part of data that begins at data[5] and includes 8, 20, 11, 3, 6. A small array, which is actually part of a larger array, is called a subarray. The expression (data + 5) is an example of pointer arithmetic, which allows a programmer to combine a pointer or an array with integer values. Pointer arithmetic has many interesting uses, but we'll only use it for this one purpose of specifying a subarray.

Consider the subarray (data + 5). This is part of the complete data array, containing the last five elements of data. Moreover, (data + 5) can be used just like any other five-element array. Here are some examples:

```
cout << (data + 5)[0]; // Prints the 8
cout << (data + 5)[2]; // Prints the 11
++((data + 5)[1]); // Adds one to the array element
```

The third statement, ++((data + 5)[1]), adds one to the [1] element of the subarray, increasing it from 20 to 21. After this statement, the data array has these values:

| data |
| --- |
| 9 | 12 | 31 | 25 | 5 | 8 | 21 | 11 | 3 | 6 |
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

Notice that (data + 5)[1] is the [1] element of the subarray, but it is also the [6] element of the whole array. So changing (data + 5)[1] will actually change data[6]. In other words: A subarray is always part of a complete array. Changing the subarray will change the complete array.

Why did we want to use subarrays in the first place? Using a subarray, we can make a function call that sorts part of an array. Here are two examples:

```
selectionsort((data + 5), 4); // Sorts data[5] through data[8]
selectionsort((data + 2), 5); // Sorts data[2] through data[6]
```

For example, the second function call sorts five elements starting at data[2]. With subarrays in hand, we can develop our two recursive sorting algorithms.

### Specifying Subarrays with Pointer Arithmetic

Suppose that data is an array with at least n elements. For any integer i from 0 to n, the expression (data + i) refers to the subarray that begins at data[i] and continues to the end of the array.

In the subarray, (data + i)[0] is the same as data[i]; (data + i)[1] is the same as data[i+1]; and so on.

A subarray is always part of a complete array. Changing the subarray will change the complete array.

### Mergesort

The most straightforward implementation of the divide-and-conquer approach to sorting is the mergesort algorithm. The mergesort algorithm divides the array near its midpoint, sorts the two half-arrays by recursive calls to the algorithm, and then merges the two halves to get a new sorted array of elements. The final “merging” step of the process will require some thought, so we’ll postpone that part of the implementation by assuming that we have a separate function to carry out the merging. The prototype for the merging function is shown here:

```
void merge(int data[ ], size_t n1, size_t n2);
// Precondition: data is an array (or subarray) with at least n1 + n2
// elements. The first n1 elements (from data[0] to data[n1-1]) are sorted
// from smallest to largest, and the last n2 (from data[n1] to
// data[n1 + n2 - 1]) are also sorted from smallest to largest.
// Postcondition: The first n1 + n2 elements of data have been rearranged
// to be sorted from smallest to largest.
// NOTE: If there is insufficient dynamic memory, then bad_alloc is
// thrown.
```

This merge function will be used as the last step of our mergesort. Notice that the merge function will use some dynamic memory, so there is a possibility of failure that we have indicated in the specification. Can you predict where the dynamic memory will come into play? You’ll see the answer shortly, but for now, examine the mergesort function in Figure 13.2.

The stopping case for mergesort’s recursion is when the array to be sorted consists of only one element. In this stopping case, there is no work to do because a single element does not need to be “rearranged.” On the other hand, if there is more than one element, then the mergesort function carries out these steps:

- 1. Calculate the sizes of the two subarrays. The first size, n1, is approximately half of the entire size (calculated by n/2, using integer division).
- The second size, n2, is whatever is left over (calculated by n – n1).



- An array element can be used like any variable.
- An array index must be at least zero and less than the size of the array.
- A bounds error, which occurs if you supply an invalid array index, can corrupt data or cause your program to terminate.
- With a partially filled array, keep a companion variable for the current size.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_318_0.png)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_318_1.png)

### Be able to use common array algorithms.

- To copy an array, use a loop to copy its elements to a new array.
- When separating elements, don't place a separator before the first element.
- A linear search inspects elements in sequence until a match is found.
- Before inserting an element, move elements to the end of the array *starting with the last one*.
- Use a temporary variable when swapping two elements.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_318_2.png)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_318_3.png)

### Implement functions that process arrays.

- When passing an array to a function, also pass the size of the array.
- Array parameters are always reference parameters.
- A function's return type cannot be an array.
- When a function modifies the size of an array, it needs to tell its caller.
- A function that adds elements to an array needs to know its capacity.

### Be able to combine and adapt algorithms for solving a programming problem.

- By combining fundamental algorithms, you can solve complex programming tasks.
- You should be familiar with the implementation of fundamental algorithms so that you can adapt them.

### Discover algorithms by manipulating physical objects.

- Use a sequence of coins, playing cards, or toys to visualize an array of values.
- You can use paper clips as position markers or counters.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_318_4.png)

### Use two-dimensional arrays for data that is arranged in rows and columns.

- Use a two-dimensional array to store tabular data.
- Individual elements in a two-dimensional array are accessed by using two subscripts, array[i][j].
- A two-dimensional array parameter must have a fixed number of columns.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_318_5.png)

### Use vectors for managing collections whose size can change.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_319_0.png)

- A vector stores a sequence of values whose size can change.
- Use the size member function to obtain the current size of a vector.
- Use the push_back member function to add more elements to a vector. Use pop_back to reduce the size.
- Vectors can occur as function arguments and return values.
- Use a reference parameter to modify the contents of a vector.
- A function can return a vector.

## REVIEW EXERCISES

**R6.1** Write code that fills an array double values[10] with each set of values below.

|  | Values |
|---|---|
| a. | 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 |
| b. | 0, 2, 4, 6, 8, 10, 12, 14, 16, 18 |
| c. | 1, 4, 9, 16, 25, 36, 49, 64, 81, 100 |
| d. | 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 |
| e. | 1, 4, 9, 16, 9, 7, 4, 9, 11 |
| f. | 0, 1, 0, 1, 0, 1, 0, 1, 0, 1 |
| g. | 0, 1, 2, 3, 4, 0, 1, 2, 3, 4 |

**R6.2** Consider the following array:

```cpp
int a[] = { 1, 2, 3, 4, 5, 4, 3, 2, 1, 0 };
```

What is the value of total after the following loops complete?

```cpp
a. int total = 0;
   for (int i = 0; i < 10; i++) { total = total + a[i]; }

b. int total = 0;
   for (int i = 0; i < 10; i = i + 2) { total = total + a[i]; }

c. int total = 0;
   for (int i = 1; i < 10; i = i + 2) { total = total + a[i]; }

d. int total = 0;
   for (int i = 2; i <= 10; i++) { total = total + a[i]; }

e. int total = 0;
   for (int i = 0; i < 10; i = 2 * i) { total = total + a[i]; }

f. int total = 0;
   for (int i = 9; i >= 0; i--) { total = total + a[i]; }

g. int total = 0;
   for (int i = 9; i >= 0; i = i - 2) { total = total + a[i]; }

h. int total = 0;
   for (int i = 0; i < 10; i++) { total = a[i] - total; }
```

**R6.3** Consider the following array:

```cpp
int a[] = { 1, 2, 3, 4, 5, 4, 3, 2, 1, 0 };
```

What are the contents of the array after the following loops complete?

- a. `for (int i = 1; i < 10; i++) { a[i] = a[i - 1]; }`
- b. `for (int i = 9; i > 0; i--) { a[i] = a[i - 1]; }`
- c. `for (int i = 0; i < 9; i++) { a[i] = a[i + 1]; }`
- d. `for (int i = 8; i >= 0; i--) { a[i] = a[i + 1]; }`
- e. `for (int i = 1; i < 10; i++) { a[i] = a[i] + a[i - 1]; }`
- f. `for (int i = 1; i < 10; i = i + 2) { a[i] = 0; }`
- g. `for (int i = 0; i < 5; i++) { a[i + 5] = a[i]; }`
- h. `for (int i = 1; i < 5; i++) { a[i] = a[9 - i]; }`

**R6.4** Write a loop that fills an array int values[10] with ten random numbers between 1 and 100. Write code for two nested loops that fill values with ten *different* random numbers between 1 and 100.

**R6.5** Write C++ code for a loop that simultaneously computes both the maximum and minimum of an array.

**R6.6** What is wrong with the following loop?

```cpp
int values[10];
for (int i = 1; i <= 10; i++)
{
   values[i] = i * i;
}
```

Explain two ways of fixing the error.

**R6.7** What is an index of an array? What are the legal index values? What is a bounds error?

**R6.8** Write a program that contains a bounds error. Run the program. What happens on your computer?

**R6.9** Write a loop that reads ten numbers and a second loop that displays them in the opposite order from which they were entered.

**R6.10** Trace the flow of the element separator loop in Section 6.2.5 with the given example. Show two columns, one with the value of i and one with the output.

**R6.11** Trace the flow of the finding matches loop in Section 6.7.4, where values contains the elements 110 90 100 120 80. Show two columns, for i and matches.

**R6.12** Trace the flow of the linear search loop in Section 6.2.6, where values contains the elements 80 90 100 120 110. Show two columns, for pos and found. Repeat the trace when values contains 80 90 100 70.

**R6.13** Trace both mechanisms for removing an element described in Section 6.2.7. Use an array values with elements 110 90 100 120 80, and remove the element at index 2.

**R6.14** For the operations on partially filled arrays below, provide the header of a function.

- a. Sort the elements in decreasing order.
- b. Print all elements, separated by a given string.
- c. Count how many elements are less than a given value.
- d. Remove all elements that are less than a given value.
- e. Place all elements that are less than a given value in another array.

Do not implement the functions.

- h. Return true if the array is currently sorted in increasing order.
- i. Return true if the array contains two adjacent duplicate values.
- j. Return true if the array contains duplicate values (which need not be adjacent).

For each function, provide a test program.

**P6.3** Modify the largest.cpp program to mark both the smallest and the largest element.

**P6.4** Reimplement How To 6.1 without removing the minimum from the array of scores. Instead, compute the final score as the difference of the sum and the minimum of the scores.

**P6.5** Write a function void remove_min that removes the minimum value from a partially filled array without calling other functions.

**P6.6** Write a function that computes the alternating sum of all elements in an array. For example, if alternating_sum is called with an array containing

`1   4   9   16   9   7   4   9   11`

then it computes

`1 − 4 + 9 − 16 + 9 − 7 + 4 − 9 + 11 = −2`

**P6.7** Write a function that implements the algorithm developed in Section 6.5.

**P6.8** Write a function reverse that reverses the sequence of elements in an array. For example, if reverse is called with an array containing

`1   4   9   16   9   7   4   9   11`

then the array is changed to

`11   9   4   7   9   16   9   4   1`

**P6.9** Write a function

```cpp
bool equals(int a[], int a_size, int b[], int b_size)
```

that checks whether two arrays have the same elements in the same order.

**P6.10** Write a function

```cpp
bool same_set(int a[], int a_size, int b[], int b_size)
```

that checks whether two vectors have the same elements in some order, ignoring duplicates. For example, the two arrays

`1   4   9   16   9   7   4   9   11`

and

`11   11   7   9   16   4   1`

would be considered identical. You will probably need one or more helper functions.

**P6.11** Write a function

```cpp
bool same_elements(int a[], int b[], int size)
```

that checks whether two arrays have the same elements in some order, with the same multiplicities. For example,

`1   4   9   16   9   7   4   9   11`


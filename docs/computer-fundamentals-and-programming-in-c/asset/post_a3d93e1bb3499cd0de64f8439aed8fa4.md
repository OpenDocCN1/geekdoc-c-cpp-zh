
**Note**

- It may not terminate if the stopping case is not correct or is incomplete (stack overflow: run-time error).
- Make sure that each recursive step leads to a situation that is closer to a stopping case.

### 12.10.3 Comparing Recursion and Iteration

Recursion is a very powerful tool for solving complex problems, particularly when the underlying problem or data to be treated is already defined in recursive terms. For such problems, recursion can lead to solutions that are much clearer and easier to modify than their iterative counterparts.

However, such recursive definitions do not guarantee that a recursive algorithm is the best way to solve a problem. Depending on the implementation available and the algorithm being used, recursion can require a substantial amount of runtime overhead. Thus, the use of recursion illustrates the classic trade-off between time spent in constructing and maintaining a program and the cost in time and memory of execution of that program.

The following two factors contribute to the inefficiency of some recursive solutions.

- The overhead associated with function calls
- The inefficient utilization of memory

With most implementations of modern programming languages, a function call incurs a bookkeeping overhead in the form of a runtime stack. Recursive functions magnify this bookkeeping overhead, because a single initial call to the function can generate a large number of recursive calls.

Recursion makes inefficient utilization of memory, as every time a new recursive call is made a new set of local variables is allocated to the function. Moreover, it also slows down execution speed, as function calls require jumps, and saving the current state of the calling function onto the stack before the jump.

Recursion is of value when the return values of the recursive function are used in further processing within the calling version of the function (rather than being immediately passed back to an earlier version of the function). In this case it is worth saving the parameter and local variables on the stack because they are used later in some useful way.

If one problem can be solved in both ways (recursive or iterative), then choosing the iterative version is a good idea since it is faster and does not consume a lot of memory.

**Note**

- In general, an iterative version of a program will execute more efficiently in terms of time and space than a recursive version. This is because the overhead involved in entering and exiting a function is avoided in the iterative version. However, a recursive solution can sometimes be the most natural and logical way of solving a complex problem.

## 12.11 SEARCHING AND SORTING

### 12.11.1 Searching Algorithms

Searching an array of integers has already been discussed in Chapter 11. Among the searching algorithms, only two of them will be discussed here—sequential search and binary search.

**Sequential or linear search algorithm**

The idea behind sequential search is to compare the given number to each of the numbers in the array. If a number in the list matches the given key, we can return the index of that number. If we reach the end of the list, we can indicate that the key does not exist in the array by returning -1. Here is an implementation of this simple algorithm:

```c
int lsearch(int ArrayElement[], int key,
            int ArraySize)
{
    int i;
    for (i = 0; i < ArraySize; i++)
        if (ArrayElement[i] == key)
            return (i);
    return (-1);
}
```

The function calling statement will be as follows:

```c
p = lsearch(a, k, n);
if (p == -1)
    printf("\n KEY NOT FOUND");
else
    printf("\n KEY FOUND AT POSITION %d", p);
```

**Binary search algorithm**

The precondition of binary search is that it requires sorted data to operate on. The basic technique is to compare the search element with the element which is in the middle of the search space and then to restrict further searching in the appropriate half of the search space (this can be done because the search space is sorted). Then at each step, the process is repeated (cutting the remaining search space in half at each step) until either the search element is found or we have run out of elements to compare and the element was not in the search space.

To implement binary search, variables beg and end keep track of the lower bound and upper bound of the array, respectively. We begin by examining the middle element of the array. If the key we are searching for is less than the middle element, then it must reside in the lower half of the array. Thus, we set end to (mid - 1). If the key we are searching for is greater than the middle element, then it must reside in the upper half of the array. Thus, we set beg to (mid + 1). This restricts our next iteration through the loop to the top half of the array. In this way, each iteration halves the size of the array to be searched. For example, the first iteration will leave three items to test. After the second iteration, there will be one item left to test. Therefore, it takes only three iterations to find any number.

To illustrate the algorithm, let us consider the following array:

| 3 | 10 | 15 | 20 | 35 | 40 | 60 |
|---|---|---|---|---|---|---|

Suppose we want to search the element “15”.

1. We take `beg = 0`, `end = 6` and compute the location of the middle element as

   `mid = (beg + end) / 2 = (0 + 6) / 2 = 3`

2. We then compare the search key with `mid`, i.e. `a[mid] == a[3]` is not equal to 15. Since `beg < end`, we have to search between `mid` and `end`.

3. As `a[mid] = 20 > 15`, therefore, we take `end = mid − 1 = 3 − 1 = 2` whereas `beg` remains the same. Thus,

   `mid = (beg + end) / 2 = (0 + 2) / 2 = 1`

4. Since `a[mid]`, i.e. `a[1] = 10 < 15`, therefore, we take `beg = mid + 1 = 1 + 1 = 2`, while `end` remains the same.

5. Now `beg = end`. Compute the `mid` element:

   `mid = (beg + end) / 2 = (2 + 2) / 2 = 2`

Since `a[mid]`, i.e. `a[2] = 15`, the search terminates on success. The C code for binary search is given below.

```c
#include <stdio.h>

int binarysearch(int a[], int n, int key)
{
    int beg, mid, end;
    beg = 0;
    end = n - 1;
    while (beg <= end)
    {
        mid = (beg + end) / 2;
        if (key == a[mid])
            return mid;
        else if (key > a[mid])
            beg = mid + 1;
        else
            end = mid - 1;
    }
    return -1;
}

int main()
{
    int arr[50], n, key, index;
    printf("How many elements?");
    scanf("%d", &n);
    puts("Enter the array elements in ascending order");
    for (index = 0; index < n; index++)
        scanf("%d", &arr[index]);
    printf("Enter the search key: ");
    scanf("%d", &key);
    index = binarysearch(arr, n, key);
    if (index == -1)
        puts("Sorry, the given key was not found");
    else
        printf("The given key was found at index:\n%d\n", index);
    return 0;
}
```

**Binary search in a recursive way**

Binary search is often written using recursion, instead of iteration. This is because when the algorithm decides to search the right or left half of the array, it becomes a simpler version of the original problem. In the recursive Search function below, note how the parameters to the recursive calls are adjusted to specify either the right or left half of the array.

```c
/* Given:      Array of integers.
   Low         The low index of the range of integers to search.
   High        The top index of the range of integers to search.
   k           The integer for which to search.
   Task:       To do a recursive binary search for k in the specified range of Array.
   Return:     In the function name, return the index of where k was found or -1 if it was not found.
*/
int search(int x[], int k, int low, int high)
{
    int mid;
    if (low > high)
        return (-1);
    mid = (low + high) / 2;
    return (k == x[mid] ? mid : k < x[mid] ? search(x, k, low, mid - 1) : search(x, k, mid + 1, high));
}
```

### 12.11.2 Sorting Algorithms

Arranging elements of an array in a particular order is called sorting. The order of arrangement may be ascending or descending in nature. There are several methods of arranging or sorting arrays. Sorting algorithms are divided into two categories—internal and external sorts.

**Internal sort** Any sort algorithm, which uses main memory exclusively during the sort. This assumes high-speed random access to all memory.

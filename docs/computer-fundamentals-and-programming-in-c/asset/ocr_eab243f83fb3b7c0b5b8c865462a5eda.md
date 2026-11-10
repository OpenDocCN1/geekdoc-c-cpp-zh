+   **Note**
+   - It may not terminate if the stopping case is not correct or is incomplete (stack overflow: run-time error).
+   - Make sure that each recursive step leads to a situation that is closer to a stopping case.

# 12.10.3 Comparing Recursion and Iteration

Recursion is a very powerful tool for solving complex problems, particularly when the underlying problem or data to be treated is already defined in recursive terms. For such problems, recursion can lead to solutions that are much clearer and easier to modify than their iterative counterparts.

However, such recursive definitions do not guarantee that a recursive algorithm is the best way to solve a problem. Depending on the implementation available and the algorithm being used, recursion can require a substantial amount of runtime overhead. Thus, the use of recursion illustrates the classic trade-off between time spent in constructing and maintaining a program and the cost in time and memory of execution of that program.

The following two factors contribute to the inefficiency of some recursive solutions.

+   - The overhead associated with function calls
+   - The inefficient utilization of memory

With most implementations of modern programming languages, a function call incurs a booking overhead in the form of a runtime stack. Recursive functions magnify this bookkeeping overhead, because a single initial call to the function can generate a large number of recursive calls.

Recursion makes inefficient utilization of memory, as every time a new recursive call is made a new set of local variables is allocated to function. Moreover, it also slows down execution speed, as function calls require jumps, and saving the current state of the calling function onto stack before jump.

Recursion is of value when the return values of the recursive function are used in further processing within the calling version of the function (rather than being immediately passed back to an earlier version of the function). In this case it is worth saving the parameter and local variables on the stack because they are used later in some useful way.

If one problem can be solved in both ways (recursive or iterative), then choosing iterative version is a good idea since it is faster and does not consume a lot of memory.

+   **Note**
+   - In general, an iterative version of a program will execute more efficiently in terms of time and space than a recursive version. This is because the overhead involved in entering and exiting a function is avoided in iterative version. However, a recursive solution can be sometimes the most natural and logical way of solving a complex problem.

# 12.11 SEARCHING AND SORTING

# 12.11.1 Searching Algorithms

Searching an array of integers has already been discussed in Chapter 11. Among the searching algorithms, only two of them will be discussed here—sequential search and binary search.

# Sequential or linear search algorithm

The idea behind sequential search is to compare the given number to each of the numbers in the array. If a number in the list matches the given key, we can return the index of that number. If we reach the end of the list, we can indicate that the key does not exist in the array by returning -1. Here is an implementation of this simple algorithm:

```
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

```
p=lsearch(a,k,n);
if(p == -1)
    printf("\n KEY NOT FOUND");
else
    printf("\n KEY FOUND AT POSITION %d", p);
```

# Binary search algorithm

The precondition of binary search is that it requires sorted data to operate on. The basic technique is to compare the search element with the element which is in the middle of the search space and then to restrict further searching in the appropriate half of the search space (this can be done because the search space is sorted). Then at each step, the process is repeated (cutting the remaining search space in half at each step) until either the search element is found or we have run out of elements to compare and the element was not in the search space.

To implement binary search, variables beg and end keep track of the lower bound and upper bound of the array, respectively. We begin by examining the middle element of the array. If the key we are searching for is less than the middle element, then it must reside in the lower half of the array. Thus, we set end to (mid - 1). If the key we are searching for is greater than the middle element, then it must reside in the upper half of the array. Thus, we set beg to (mid + 1). This restricts our next iteration through the loop to the top half of the array. In this way, each iteration halves the size of the array to be searched. For example, the first iteration
input. For example, the table might be as shown in Display 19.15. This table does not give a single time, but instead gives different times for a variety of different input sizes.

The table is a description of what is called a function in mathematics. Just as a (non-void) C++ function takes an argument and returns a value, so too does this function take an argument, which is an input size, and returns a number, which is the time the program takes on an input of that size. If we call this function T, then T(10) is 2 seconds, T(100) is 2.1 seconds, T(1000) is 10 seconds, and T(10,000) is 2.5 minutes. The table is just a sample of some of the values of this function T. The program will take some amount of time on inputs of every size. So although they are not shown in the table, there are also values for T(1), T(2), ..., T(101), T(102), and so forth. For any positive integer N, T(N) is the amount of time it takes for the program to sort N numbers. The function T is called the running time of the program.

So far we have been assuming that this sorting program will take the same amount of time on any list of N numbers. That need not be true. Perhaps it takes much less time if the list is already sorted or almost sorted. In that case, T(N) is defined to be the time taken by the "hardest" list—that is, the time taken on that list of N numbers that makes the program run the longest. This is called the worst-case running time. In this chapter, we will always mean worst-case running time when we give a running time for an algorithm or for some code.

The time taken by a program or algorithm is often given by a formula, such as 4N + 3, 5N + 4, or N². If the running time T(N) is 5N + 5, then on inputs of size N the program will run for 5N + 5 time units.

The following is some code to search an array a with N elements to determine whether a particular value target is in the array:

```
int i = 0;
bool found = false;
while (i < N && !(found))
    if (a[i] == target)
        found = true;
    else
        i++;
```

# Display 19.15 Some Values of a Running Time Function

| Input Size | Running Time |
|---|---|
| 10 numbers | 2 seconds |
| 100 numbers | 2.1 seconds |
| 1000 numbers | 10 seconds |
| 10,000 numbers | 2.5 minutes |

We want to compute some estimate of how long it will take a computer to execute this code. We would like an estimate that does not depend on which computer we use, either because we do not know which computer we will use or because we might use several different computers to run the program at different times.
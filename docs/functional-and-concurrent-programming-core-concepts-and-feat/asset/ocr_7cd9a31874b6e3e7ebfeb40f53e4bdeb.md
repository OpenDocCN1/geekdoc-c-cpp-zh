```
val highSorted = quickSort(high, exec)
lowFuture.get() ::: pivot ::: highSorted
```

# Listing 26.1: Deadlock-prone parallel quick-sort; see also Lis. 26.5.

This method follows the same pattern as the previous implementation of quick-sort in Listing 10.1. The only difference is that the function uses a separate thread to sort the low values, while the current thread sorts the high values, thus sorting both lists in parallel. After both lists have been sorted, the sorted low values are retrieved using method get, and the two lists are concatenated around the pivot as before. This is the same pattern used in the server example to fetch a customized ad in the background except that the task used to create the future is the function itself, recursively.

At first, the code appears to be working well enough. You can use quickSort to successfully sort a small list of numbers:

```
Scala
val exec = Executors.newFixedThreadPool(3)
quickSort(List(1, 6, 8, 6, 1, 8, 2, 8, 9), exec) // List(1, 1, 2, 6, 6, 8, 8, 8, 9)
```

However, if you use the same three-thread pool in an attempt to sort the list [5,4,1,3,2], the function gets stuck and fails to terminate. Looking at a thread dump would show that all three threads are blocked on a call lowFuture.get in a deadlock.

Figure 26.1 displays the state of the computation at this point as a tree. Each sorting task is split into three branches: low, pivot, and high. The thread that first invokes quickSort is called main here. It splits the list into a pivot (5), a low list ([4,1,3,2]), and a high list ([]). It quickly sorts the empty list itself, and then blocks, waiting for the sorting of list [4,1,3,2] to complete. Similar steps are taking place with the thread

![](bbox=[0.295, 0.665, 0.66, 0.895])

# Figure 26.1 Deadlock as a result of tasks created by tasks.
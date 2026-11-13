```
if(pos == -1)
 printf("\n %d is not found in the array", val);
 else
 printf("\n %d is found at position %d", val, pos);
 getche();
 return 0;
 }
```

# Fibonacci Search

We are all well aware of the Fibonacci series in which the first two terms are 0 and 1 and then each successive term is the sum of previous two terms. In the Fibonacci series given below, each number is called a Fibonacci number.
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...

The same series and concept can be used to search for a given value in a list of numbers. Such a search algorithm which is based on Fibonacci numbers is called Fibonacci search and was developed by Kiefer in 1953. The search follows a divide-and-conquer technique and narrows down possible locations with the help of Fibonacci numbers.
Fibonacci search is similar to binary search. It also works on a sorted list and has a run time complexity of O(log n). However, unlike the binary search algorithm, Fibonacci search does not divide the list into two equal halves rather it subtracts a Fibonacci number from the index to reduce the size of the list to be searched. So, the key advantage of Fibonacci search over binary search is that comparison dispersion is low.

# 14.6 INTRODUCTION TO SORTING

Sorting means arranging the elements of an array so that they are placed in some relevant order which may be either ascending or descending. That is, if A is an array, then the elements of A are arranged in a sorted order (ascending order) in such a way that A[0] < A[1] < A[2] < ..... < A[N].
For example, if we have an array that is declared and initialized as
int A[] = {21, 34, 11, 9, 1, 0, 22};
Then the sorted array (ascending order) can be given as:
A[] = {0, 1, 9, 11, 21, 22, 34};

A sorting algorithm is defined as an algorithm that puts the elements of a list in a certain order, which can be either numerical order, lexicographical order, or any user-defined order. Efficient sorting algorithms are widely used to optimize the use of other algorithms like search and merge algorithms which require sorted lists to work correctly. There are two types of sorting:

+   - Internal sorting which deals with sorting the data stored in the computer’s memory.
+   - External sorting which deals with sorting the data stored in files. External sorting is applied when there is voluminous data that cannot be stored in the memory.

# 14.6.1 Sorting on Multiple Keys

Many a times, when performing real-world applications, it is desired to sort arrays of records using multiple keys. This situation usually occurs when a single key is not sufficient to uniquely identify a record. For example, in a big organization we may want to sort a list of employees on the basis of their departments first and then according to their names in alphabetical order.
Other examples of sorting on multiple keys can be

+   - Telephone directories in which names are sorted by location, category (business or residential), and then in an alphabetical order.
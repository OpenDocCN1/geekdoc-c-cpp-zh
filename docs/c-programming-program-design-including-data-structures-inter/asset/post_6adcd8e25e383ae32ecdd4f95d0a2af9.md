
- 13. This chapter describes the array implementation of queues that use a special array slot, called the reserved slot, to distinguish between an empty and a full queue. Write the definition of the class and the definitions of the function members of this queue design. Also, write a test program to test various operations on a queue.

- 14. Write the definition of the function `moveNthFront` that takes as a parameter a positive integer, `n`. The function moves the `nth` element of the queue to the front. The order of the remaining elements remains unchanged. For example, suppose:
  
  ```text
  queue = {5, 11, 34, 67, 43, 55} and n = 3.
  ```
  
  After a call to the function `moveNthFront`:
  
  ```text
  queue = {34, 5, 11, 67, 43, 55}.
  ```
  
  Add this function to the class `queueType`. Also, write a program to test your method.

- 15. Write a program that reads a line of text, changes each uppercase letter to lowercase, and places each letter both in a queue and onto a stack. The program should then verify whether the line of text is a palindrome (a set of letters or numbers that is the same whether read forward or backward).

- 16. The implementation of a queue in an array, as given in this chapter, uses the variable `count` to determine whether the queue is empty or full. You can also use the variable `count` to return the number of elements in the queue. On the other hand, class `linkedQueueType` does not use such a variable to keep track of the number of elements in the queue. Redefine the class `linkedQueueType` by adding the variable `count` to keep track of the number of elements in the queue. Modify the definitions of the functions `addQueue` and `deleteQueue` as necessary. Add the function `queueCount` to return the number of elements in the queue. Also, write a program to test various operations of the class you defined.

- 17. Write the definition of the class `linkedQueueType`, which is derived from the class `unorderedLinkedList`, as explained in this chapter. Also, write a program to test various operations of this class.

- 18.
  - a. Write the definitions of the functions `setWaitingTime`, `getArrivalTime`, `getTransactionTime`, and `getCustomerNumber` of the class `customerType` defined in the section Application of Queues: Simulation.
  
  - b. Write the definitions of the functions `getRemainingTransactionTime`, `setCurrentCustomer`, `getCurrentCustomerNumber`, `getCurrentCustomerArrivalTime`, `getCurrentCustomerWaitingTime`, and `getCurrentCustomerTransactionTime` of the class `serverType` defined in the section Application of Queues: Simulation.
  
  - c. Write the definition of the function `runSimulation` to complete the design of the computer simulation program (see the section Application of Queues: Simulation). Test run your program for a variety of data. Moreover, use a random number generator to decide whether a customer arrived at a given time unit.

Chapters 12 and 13 described how to organize data into computer memory using an array and how to perform basic operations on that data. Chapter 16 described how to organize data using linked lists. The most important operation that can be performed on a list is the search algorithm. Using the search algorithm, you can do the following:

- Determine whether a particular item is in the list.
- If the data is specially organized (e.g., sorted), find the location in the list where a new item can be inserted.
- Find the location of an item to be deleted.

The search algorithm’s performance, therefore, is crucial. If the search is slow, it takes a large amount of computer time to accomplish your task; if the search is fast, you can accomplish your task quickly.

In the first part of this chapter, we describe the search algorithms: sequential search and binary search. Certain search algorithms work only on sorted data. Therefore, the second half of this chapter discusses various sorting algorithms.

## Searching and Sorting Algorithms

The searching and sorting algorithms that we describe are generic. Because searching and sorting require comparisons of data, the algorithms should work on the type of data that provides appropriate functions to compare data items. Now data can be organized with the help of an array or a linked list. You can create an array of data items, or you can use the class `unorderedLinkedList` to organize data. The algorithms that we describe should work on either organization. Consequently, we will write the function templates to implement a particular algorithm. All algorithms described in this chapter, with the exception of the merge sort algorithms, are for array-based lists. Because of storage issues and some other overheads, merge sort works better for linked lists. Therefore, after describing the merge sort algorithm, we will add it as a function to the class `unorderedLinkedList`. We will also show how to use the searching and sorting algorithms on objects of the class `unorderedArrayListType`. Moreover, we will place all of the array-based searching and sorting functions in the header file `searchSortAlgorithms.h`. Therefore, if you need to use a particular searching and/or sorting function designed in this chapter, your program can include this header file and use that function.

### Search Algorithms

Chapters 12, 13, and 16 described how to implement the sequential search algorithm. This chapter discusses other search algorithms and analyzes them. Analysis of the algorithms enables programmers to decide which algorithm to use for a specific application. Before exploring these algorithms, let us make the following observations.

Associated with each item in a data set is a special member that uniquely identifies the item in the data set. For example, if you have a data set consisting of student records, then the student ID uniquely identifies each student in a particular school. This unique member of the item is called the key of the item. The keys of the items in the data set are used in such operations as searching, sorting, inserting, and deleting. For instance, when we search the data set for a particular item, we compare the key of the item for which we are searching with the keys of the items in the data set.

When analyzing searching and sorting algorithms, the key comparisons refer to comparing the key of the search item with the key of an item in the list. The number of key comparisons refers to the number of times the key of the search item (in algorithms such as searching and sorting) is compared with the keys of the items in the list.

### Sequential Search

The sequential search (also called a linear search) on array-based lists was described in Chapters 12 and 13, and the sequential search on linked lists was covered in Chapter 16. The sequential search works the same for both array-based and linked lists. The search always starts at the first element in the list and continues until either the item is found in the list or the entire list is searched.

Because we are interested in the performance of the sequential search (that is, the analysis of this type of search), for easy reference and the sake of completeness, we provide the sequential search algorithm for array-based lists (as described in Chapters 12 and 13). If the search item is found, its index (that is, its location in the array) is returned. If the search is unsuccessful, −1 is returned. Note that the following sequential search does not require the list elements to be in any particular order.

```cpp
template <class elemType>
int seqSearch(const elemType list[], int length,
              const elemType& item)
{
    int loc;
    bool found = false;

    loc = 0;

    while (loc < length && !found)
        if (list[loc] == item)
            found = true;
        else
            loc++;

    if (found)
        return loc;
    else
        return -1;
} //end seqSearch
```

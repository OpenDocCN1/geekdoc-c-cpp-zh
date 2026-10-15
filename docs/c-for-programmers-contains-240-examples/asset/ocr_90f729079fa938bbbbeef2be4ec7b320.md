# 20.4.3 priority_queue Adapter

Class priority_queue provides functionality that enables insertions in sorted order into the underlying data structure and deletions from the front of the underlying data structure. A priority_queue can be implemented with STL sequence containers vector or deque. By default, a priority_queue is implemented with a vector as the underlying container. When elements are added to a priority_queue, they are inserted in priority order, such that the highest-priority element (i.e., the largest value) will be the first element removed from the priority_queue. This is usually accomplished via a sorting technique called heapsort that always maintains the largest value (i.e., highest-priority element) at the front of the data structure—such a data structure is called a heap. The comparison of elements is performed with comparator function object less<T> by default, but you can supply a different comparator.

There are several common priority_queue operations. push inserts an element at the appropriate location based on priority order of the priority_queue (implemented by calling function push_back of the underlying container, then reordering the elements using heapsort). pop removes the highest-priority element of the priority_queue (implemented by calling function pop_back of the underlying container after removing the top element of the heap). top gets a reference to the top element of the priority_queue (implemented by calling function front of the underlying container). empty determines whether the priority_queue is empty (implemented by calling function empty of the underlying container). size gets the number of elements in the priority_queue (implemented by calling function size of the underlying container).

# Performance Tip 20.20

> Each of the common operations of a priority_queue is implemented as an inline function that calls the appropriate function of the underlying container. This avoids the overhead of a second function call.

# Performance Tip 20.21

> For the best performance, use class vector as the underlying container for a priority_queue.

Figure 20.25 demonstrates the priority_queue adapter class. Header file <queue> must be included to use class priority_queue.

```
1  // Fig. 20.25: fig20_25.cpp
2  // Standard Library adapter priority_queue test program.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  #include <queue> // priority_queue adapter definition
8
9  int main()
10 {
11     std::priority_queue< double > priorities; // create priority_queue
12
```
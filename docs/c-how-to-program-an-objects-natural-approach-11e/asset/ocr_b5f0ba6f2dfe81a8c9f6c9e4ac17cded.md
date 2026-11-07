```
```cpp
// pop elements from queue
while (!values.empty()) {
    std::cout << values.front() << ' '; // view front element
    values.pop(); // remove element
}

std::cout << "\\n";
}
```
```

```
Popping from values: 3.2 9.8 5.4
```

**Fig. 13.11** | Standard library queue adaptor class template. (Part 2 of 2.)

# 13.12.3 priority_queue Adaptor

Class priority_queue (from header <queue>) enables insertions in sorted order into the underlying data structure and deletions from the front of the underlying data structure. By default, a priority_queue stores its elements in a vector.²² Elements added to a priority_queue are inserted in priority order, such that the highest-priority element will be the first element removed. This is usually accomplished by arranging the elements as a heap²³ that always maintains its highest-priority element at the front of the data structure. Element comparisons are performed with comparator function object less<T> by default.

The priority_queue operations include

+   - **push** to insert an element at the appropriate location based on **priority order**.
+   - **emplace** to construct an element in place and re-sort the priority_queue into priority order.
+   - **pop** to remove the priority_queue’s highest-priority element.
+   - **top** to get a reference to the priority_queue’s top element—implemented by calling the underlying container’s **front** member function.
+   - **empty** to determine whether the priority_queue is empty—implemented by calling the underlying container’s **empty** member function.
+   - **size** to get the priority_queue’s number of elements—implemented by calling the underlying container’s **size** member function.

Figure 13.12 demonstrates priority_queue. Line 7 instantiates a priority_queue of doubles and uses a vector as the underlying data structure. Lines 10–12 use member function push to add elements to the priority_queue. Lines 17–20 use the empty member function (available in all containers) to determine whether the priority_queue is empty (line 17). If not, line 18 uses priority_queue function top to retrieve the highest-priority element (i.e., the largest value) in the priority_queue for output. Line 19 calls pop, available in all adaptor classes, to remove the priority_queue’s highest-priority element.

22. “std::priority_queue.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/container/priority_queue

23. Not to be confused with the heap for dynamically allocated memory. See Section 14.4.14.
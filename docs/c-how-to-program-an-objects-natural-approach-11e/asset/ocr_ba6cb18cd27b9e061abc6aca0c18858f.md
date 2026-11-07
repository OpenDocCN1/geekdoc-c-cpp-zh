```
```cpp
35 // display results
36 if (element != -1) {
37     std::cout << std::format("Found value in element {}\n", element);
38 }
39 else {
40     std::cout << "Value not found\n";
41 }
42 }
```
```

Enter integer search key: 36
Found value in element 18

Enter integer search key: 37
Value not found

Fig. 21.1 | Linear search of an array. (Part 2 of 2.)

# 21.3.2 Efficiency of Linear Search

The linear search algorithm runs in O(n) time. Linear search’s worst case is checking every element to determine whether the search key is in the array. If the array’s size doubles, so does the number of comparisons. Linear search can provide outstanding performance if the element matching the search key happens to be at or near the front of the array. But we seek algorithms that perform well, on average, across all searches, including those where the element matching the search key is near the end of the array. If a program needs to perform many searches on large arrays, it may be better to implement a more efficient algorithm, such as the binary search (Section 21.4).

Sometimes the simplest algorithms perform poorly—their virtue is that they’re easy to program, test and debug. More complex algorithms are typically required to maximize performance.

# Checkpoint

1 (True/False) A linear search is typically used to determine whether a sorted array contains a specified search key.
**Answer:** False. Actually, linear search is typically used to determine whether an **unsorted array** contains a specified search key.

2 (*Multiple Choice*) Which of the following statements about linear search is *false*?
   a) It compares every array element with the search key.
   b) Because the array is not in any particular order, it's just as likely that the value will be found in the first element as in the last.
   c) On average, it compares the search key with half the array's elements.
   d) It works well for small or unsorted arrays but it's inefficient for large arrays.
**Answer:** a) is false. It could find a match before reaching the array's end, in which case it would terminate the search before comparing every element with the search key.
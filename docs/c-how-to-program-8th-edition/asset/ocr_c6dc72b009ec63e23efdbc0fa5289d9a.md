```
```cpp
// display vector elements using const_iterator
for(constIterator = integers2.begin();
    constIterator != integers2.end(); ++constIterator )
  cout << *constIterator << ' ';
} // end function printVector
```
```

```
The initial size of integers is: 0
The initial capacity of integers is: 0
The size of integers is: 3
The capacity of integers is: 4

Output array using pointer notation: 1 2 3 4 5 6
Output vector using iterator notation: 1 2 3 4
Reversed contents of vector integers: 4 3 2
```

**Fig. 22.14** | Standard Library vector class template. (Part 2 of 2.)

Lines 20–22 use function `push_back`—available in all sequence containers—to add an element to the end of the vector. If an element is added to a full vector, the vector increases its size—some STL implementations have the vector double its capacity.

> **Performance Tip 22.7**
> 
> It can be wasteful to double a vector’s size when more space is needed. For example, a full vector of 1,000,000 elements resizes to accommodate 2,000,000 elements when a new element is added. This leaves 999,999 unused elements. You can use `resize` and `reserve` to control space usage better.

![](bbox=[0.161, 0.435, 0.217, 0.482])

Lines 24 and 25 use `size` and `capacity` to illustrate the new size and capacity of the vector after the three `push_back` operations. Function `size` returns 3—the number of elements added to the vector. Function `capacity` returns 4, indicating that we can add one more element before the vector needs to add more memory. When we added the first element, the vector allocated space for one element, and the size became 1 to indicate that the vector contained only one element. When we added the second element, the capacity doubled to 2 and the size became 2 as well. When we added the third element, the capacity doubled again to 4. So we can actually add another element before the vector needs to allocate more space. When the vector eventually fills its allocated capacity and the program attempts to add one more element to the vector, the vector will double its capacity to 8 elements.

The manner in which a vector grows to accommodate more elements—a time-consuming operation—is not specified by the C++ Standard Document. C++ library implementors use various clever schemes to minimize the overhead of resizing a vector. Hence, the output of this program may vary, depending on the version of vector that comes with your compiler. Some library implementors allocate a large initial capacity. If a vector stores a small number of elements, such capacity may be a waste of space. However, it can greatly improve performance as programs add many elements to a vector and does not have to reallocate memory to accommodate those elements. This is a classic space–time trade-off. Library implementors must balance the amount of memory used against the amount of time required to perform various vector operations.

Lines 29–30 demonstrate how to output the contents of an array using pointers and pointer arithmetic. Line 33 calls function `printVector` (defined in lines 49–57) to output the contents of a vector using iterators. Function template `printVector` receives a const
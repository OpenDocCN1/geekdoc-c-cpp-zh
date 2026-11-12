just as you access elements in a traditional array, by using the operator [ ]. An advantage of an STL array over traditional C++ arrays is the method at that allows for range checking. For example, a traditional array declared as

```
int myArray[5];
```

permits the programmer to access elements beyond the memory allocated to the array by using an expression such as myArray[24]. This leads to unpredictable results and is a common source of errors in program.

An STL array declared as

```
array<int> mySTLArray(5);
```

would have the same issue if the programmer used the expression mySTLArray[24]. In situations where accessing elements outside the bounds of the array is possible, it is better to use an expression such as mySTLArray.at(24). This expression will throw an out_of_bounds exception that you can catch, enabling you to fix the error and allow the program to continue execution safely.

Two other important features of the STL array is its size method—enabling you to determine how many locations are in the array—and the availability of iterators for array traversal, as discussed in C++ Interlude 6.

| OPERATION | DESCRIPTION | EFFICIENCY |
|---|---|---|
| value_type& front() | Returns a reference to the front entry in the array. | O(1) |
| value_type& back() | Returns a reference to the last (back) entry in the array. | O(1) |
| value_type& at( size_type n ) | Behaves the same as [ ], but performs a bounds check. | O(1) |
| void fill( const value_type& val ) | Fills array elements with val. | O(n) |
| iterator begin() | Returns an iterator to the first element in the container. | O(1) |
| iterator end() | Returns an iterator to the last element in the container. | O(1) |
| reverse_iterator rbegin() | Returns a reverse iterator to the last element in the container. | O(1) |
| reverse_iterator rend() | Returns a reverse iterator to the first element in the container. | O(1) |

Other STL sequence containers have many operations in common but are optimized differently. For example, vector and deque permit efficient access to specific locations using the [ ] operator, but list is better for sorting. Though these containers can be constructed with an initial size, they also grow and shrink as entries are added and removed. If you realize that you need to add a significant number of entries to the container, a resize method lets you adjust the number of elements.

| OPERATION | DESCRIPTION | EFFICIENCY |
|---|---|---|
| value_type& front() | Returns a reference to the front entry in the container. | O(1) |
| value_type& back() | Returns a reference to the last (back) entry in the container. | O(1) |
| | | (continues) |
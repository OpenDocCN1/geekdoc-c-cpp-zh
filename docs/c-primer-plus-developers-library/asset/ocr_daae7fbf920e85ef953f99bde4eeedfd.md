Table F.1　**Some string Data Methods**

| Method | Returns |
|---|---|
| `c_str()` | A pointer of type `const charT*` that points to the first element of an array whose first `size()` elements equal the corresponding elements in the string controlled by `*this` and whose next element is the `charT()` character (end-of-string marker) for the `charT` type. The pointer should not be assumed to be valid after the string object itself has been modified. |
| `get_allocator()` | A copy of the allocator object that is used to allocate memory for the string object. |

Be careful of the differences among `begin()`, `rend()`, `data()`, and `c_str()`. All relate to the first character in a string, but in different ways. The `begin()` and `rend()` methods return iterators, which are generalizations of pointers, as described in Chapter 16, “The string Class and the Standard Template Library.” In particular, `begin()` returns a model of a forward iterator, and `rend()` returns a copy of a reverse iterator. Both refer to the actual string managed by the string object. (Because the string class uses dynamic memory allocation, the actual string contents need not be inside the object, so we use the term *manage* to describe the relationship between object and string.) You can use the methods that return iterators with the iterator-based algorithms of the STL. For example, you can use the STL `reverse()` function to reverse the contents of a string:

```
```cpp
string word;
cin >> word;
reverse(word.begin(), word.end());
```
```

The `data()` and `c_str()` methods, on the other hand, do return ordinary pointers. Furthermore, the returned pointers point to the first element of an *array* that holds the string characters. This array can but need not be a copy of the original string managed by the string object. (The internal representation used by the string object can be an array, but it doesn’t have to be.) Because it is possible that the returned pointers point to the original data, they are const, so they can’t be used to alter the data. Also the pointers are not guaranteed to be valid after the string is modified; this reflects that they may point to the original data. The difference between `data()` and `c_str()` is that the array `c_str()` points to is terminated with a null character (or equivalent), whereas `data()` just guarantees that the actual string characters are present. Thus, the `c_str()` method can be used, for example, as an argument to a function that expects to receive a C-style string:

```
```cpp
string file("tofu.man");
ofstream outFile(file.c_str());
```
```

Similarly, `data()` and `size()` could be used with a function that expects to receive a pointer to an array element and a value that represents the number of elements to process:
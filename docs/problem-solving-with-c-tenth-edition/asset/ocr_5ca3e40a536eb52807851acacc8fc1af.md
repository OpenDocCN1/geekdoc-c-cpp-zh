# DISPLAY 18.22  **The `std::array` (part 2 of 2)**

# ### Sample Dialogue

```
The size of the array: 6
The element at index 1: 20
Setting a[4] to 100.
Array contains:
10
20
30
0
100
0
```

Just like a vector but unlike a standard array, we can retrieve the size of the array using the `size()` function. We can also read and set the contents of the array using the traditional `[]` notation. Attempts to read a value out of range returns 0 and attempts to set a value out of range has no effect. Note that indices 3 and 5 in the array get set to the default value of 0.

We can use the same algorithm that are available to vectors. For example, if we include `<algorithm>`, we can sort the array within the ranges specified by the iterators `begin()` and `end()`.

```
std::sort(a.begin(), a.end());
cout << "After sort, array contains: " << endl;
for (int element : a)
    cout << element << endl;
```

The output is the array in sorted order:

```
After sort, array contains:
0
0
10
20
30
100
```

# ### Regular Expressions

A full treatise of regular expressions is beyond the scope of this book, but a summary of regular expressions and some examples in C++ are described here. At the time of this writing, some compilers do not support the C++11 regular expression library so check your compiler to see if the `<regex>` library
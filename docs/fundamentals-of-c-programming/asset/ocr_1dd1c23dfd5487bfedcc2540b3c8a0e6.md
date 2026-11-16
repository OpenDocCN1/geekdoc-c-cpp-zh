```
void print(int *begin, int *end) {
    for (int *elem = begin; elem != end; elem++)
        std::cout << *elem << ' ';
    std::cout << '\n';
}
```

Here begin points to the beginning of an array, and end points to one position past the end of the array. You can invoke this function with your `vec` vector object as

```
print(&vec[0], &vec[0] + vec.size()));
```

Note that the first parameter is the starting address of the wrapped array, and the second parameter uses pointer arithmetic to compute the memory address just past the end of the wrapped array.

Since the C++11 standard, the `std::vector` class has a method named `data` that returns a pointer to the first element of the array the vector manages. We can rewrite the above statement as

```
print(vec.data(), vec.data() + vec.size()));
```

or better yet as

```
auto p = vec.data();
print(p, p + vec.size()));
```

which avoids calling the `data` method twice.

As these examples show, you may use vector objects instead of arrays without any danger of not being able to use libraries that deal only with arrays.

If you happen to be using an array and need to use a function that expects a vector instead, it is easy to make a vector out of an existing array. If `arr` is a raw integer array containing `n` elements, the statement

```
std::vector<int> vec(arr, arr + n);
```

creates a new vector object `vec` with elements that are identical to `arr`. One disadvantage of this technique is that it copies all the elements in `arr` to a new dynamic array managed by the vector. This is because a vector object demands full control over the array it manages. A vector automatically frees up the memory of its array when it goes out of scope. Forcing a vector to manage a preexisting array could lead to problems in two ways:

+   • The code that created the array could later `delete` the contents of the array out from under the vector. Any attempted use of the vector after that point would be a problem.

+   • When the vector goes out of scope it automatically deallocates the array it manages. The code that originally created the array could afterward attempt to access the deallocated array with similar predictably disastrous results.

For these reasons the developers of the standard library designed the `std::vector` class to be in full control of its managed array. We thus cannot create a vector object from array created elsewhere without making a copy of the array.

We will see in Chapter 19 that it is relatively easy to write a function in a generic way so that it can accept and process either a vector or an array with equal efficiency.

Vectors are convenient data structures for working with dynamically-allocated arrays. C++ provides an object-oriented type equivalent to static C arrays. The `std::array` is the preferred way to represent statically-allocated arrays in C++.
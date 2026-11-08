```
```cpp
// https://godbolt.org/z/6d5fxn9ed
auto maxOf2(int a, int b) {
    return a < b ? b : a;  // one return: the compiler determines int
}

auto minOf3(int a, int b, int c) {
    if (a<b) return a<c ? a : c;
    else return b<c ? b : c;
}

auto medianOf3(int a, int b, int c) {
    // more complex, but no problem for the compiler
    return minOf3(maxOf2(a,b), maxOf2(b,c), maxOf2(a,c));
}
```
```

Listing 7.12 Since C++14, you can let the compiler deduce the return type.

# 7.12  Specialties

There are still some special cases regarding function definitions that I will briefly mention here so that you can recognize them when you stumble upon them.

For example, you can use return to return more than one value. To do this, use the data type tuple. I will go into more detail in Chapter 28, Section 28.1. There you will see how to easily bundle multiple values into a single return value using tuple—which feels like returning multiple values.

# 7.12.1  “noexcept”

If you find the noexcept keyword after the function declaration, then the author of the function promises that this function will not throw an exception (see Chapter 10). Let's assume the hypothetical class File, which has the following function:

```
```cpp
File openFile(const char* filename) noexcept; // Function does not throw an exception
```
```

The function openFile returns a new File object. If anything goes wrong, there are many C++ libraries that throw an exception. This function promises with noexcept not to do that; File probably has other mechanisms to detect errors.

This information might be useful for users, but it is mainly intended for the compiler. Normally, it has to generate a little bit of code in case an exception¹ could be thrown. With this keyword after the function declaration, the compiler can skip that.

¹ The additional effort is so minimal that some even speak of it as zero-cost.
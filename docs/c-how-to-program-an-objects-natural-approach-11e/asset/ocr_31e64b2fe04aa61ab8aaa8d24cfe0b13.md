+   - You can now initialize stack and queue container adapters from iterator pairs representing ranges of elements in other containers. For example, the following code snippet initializes a queue from a vector of ints. For more information, see https://wg21.link/p1425.

```
std::vector values{2, 3, 5, 7, 11, 13};
std::queue myQueue(values.begin(), values.end());
```

+   - The associative containers (Section 13.1.1) enable heterogeneous lookup—you can search for keys using values of compatible types without first converting those values to the container’s key type. For example, if the keys are std::strings, you can pass search functions C-style strings or std::string_views. This heterogeneous lookup capability is now supported for the associative container member functions erase and extract. For more information, see https://wg21.link/p2077.

+   - The <flat_map> and <flat_set> headers provide container adapters for manipulating sorted sequence containers (vectors by default) as maps and sets (Section 13.1.1). These new container adaptors provide better performance characteristics than the sorted associative containers. For more information, see
+   
+     https://www.sandordargo.com/blog/2022/10/05/cpp23-flat_map
+     https://en.cppreference.com/w/cpp/container/flat_map
+     https://en.cppreference.com/w/cpp/header/flat_set

# C++23 Attribute [[assume]]

You can indicate assumptions the compiler should make about your source code so it can optimize the resulting object code. For example, line 2 in the following snippet tells the compiler to assume denominator is not equal to 0, so the compiler does not need to generate any code for division by 0, which might result in more compact or faster code:

```
int quotient(int numerator, int denominator) {
    [[assume(denominator != 0)]];
    return numerator / denominator;
}
```

For more information, see

https://en.cppreference.com/w/cpp/language/attributes/assume

# C++23 <stacktrace> Header

Chapter 12 discussed C++’s exception-handling mechanism. Various programming languages, such as Java, C# and Python, enable programmatic access to information about the functions on the function-call stack when an exception occurs. The new <stacktrace> header adds these capabilities to C++. For more information, see

https://en.cppreference.com/w/cpp/header/stacktrace

# Features Being Considered for Future C++ Versions

+   - Asynchronous capabilities: The proposed new features include three kinds of components—schedulers, senders, and receivers—and customizable
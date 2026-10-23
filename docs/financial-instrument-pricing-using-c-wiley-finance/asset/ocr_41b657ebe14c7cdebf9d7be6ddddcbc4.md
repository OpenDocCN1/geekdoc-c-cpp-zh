**c)** We wish to create functions that process strings in some way (in a sense, we are emulating a simple version of the *Boost C++ String Algorithm* library). A string can be seen as a special kind of vector whose elements are characters. Create functions to do the following (in all cases the input is a string):

+   - Trim all leading and trailing blanks (space, tabs, etc.) from the string.
+   - Trim all leading and trailing blanks based on a unary predicate (e.g. is a digit, is a member of some set of characters).
+   - Produce a vector of strings from a character-separated string.
+   - Join two strings.

# 8. (How Many Ways to Print a Container?)

The objective of this exercise is to focus on the `std::for_each()` algorithm and use it to print the elements of an instance of `std::vector<double>`. We use functionality from C++11 and we attempt to print a vector in as many ways as possible. The advantage is that we can get some hands-on experience with new syntax and we can apply the results to more advanced applications.

Answer the following questions:

+   **a)** Write a function that accepts a vector as argument and that iterates over its elements using standard functionality for STL iterators.
+   
+   **b)** Now apply the `std::for_each()` algorithm to print the elements of the vector. Use a function object and a lambda function as the unary procedure (last argument of the algorithm).
+   
+   **c)** Apply the `std::for_each()` algorithm to modify the values of the elements of the vector. Use both a function object and a lambda function as the *unary procedure* (last argument of algorithm).
+   
+   **d)** Consider using *range-based for* loops to print the elements of the vector:

```
void print(const std::vector<double>& vec)
{
    for (const auto& elem : vec)
    {
        std::cout << elem << ",";
    }
}
```

Consider the functionality for *uniform initialisation* and *initialiser lists* to use to initialise vectors before printing them.

+   **e)** We use the `std::for_each()` algorithm to iterate in a vector and we compute the maximum, minimum and average of the elements in the vector. Use captured variables for these three quantities and encapsulate them as a tuple whose return type is `std::tuple<double, double, double>`.
+   
+   **f)** We generalise the function to print a vector so that it can be used with other sequence containers. To this end, use the *template–template parameter* trick.

*Hint:*

```
template <typename T, template <typename S,typename Alloc >
    class Container,typename TAlloc>
```
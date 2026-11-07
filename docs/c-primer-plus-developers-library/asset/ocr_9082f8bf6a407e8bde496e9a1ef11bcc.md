# # Range-based for Loop

The range-based for loop (discussed in Chapter 5, “Loops and Relational Expressions,” and Chapter 16) simplifies writing loops for built-in arrays and for classes, such as std::string and the STL containers, that have begin() and end() methods identifying a range. The loop applies the indicated action to each element in the array or container:

```
```cpp
double prices[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
for (double x : prices)
    std::cout << x << std::endl;
```
```

Here, x takes on the value of each element in prices in turn. The type of x should match the type of the array element. An easier and safer way of doing this is to use auto to declare x; the compiler will deduce the type from the information in the prices declaration:

```
```cpp
double prices[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
for (auto x : prices)
    std::cout << x << std::endl;
```
```

If your intent is to have the loop modify elements of the array or container, use a reference type:

```
```cpp
std::vector<int> vi(6);
for (auto & x: vi)          // use a reference if loop alters contents
    x = std::rand();
```
```

# # New STL Containers

C++11 adds forward_list, unordered_map, unordered_multimap, unordered_set, and unordered_multiset to its collection of STL containers (see Chapter 16). The forward_list container is a singly linked list that can be traversed in just one direction; it’s simpler and more economical of space than the doubly linked list container. The other four containers support implementing hash tables.

C++11 also adds the array template (discussed in Chapter 4, “Compound Types,” and Chapter 16), for which one specifies an element type and a fixed number of elements:

```
```cpp
std::array<int, 360> ar;    // array of 360 ints
```
```

This template class does not satisfy all the usual template requirements. For example, because the size is fixed, you can’t use any method, such as put_back(), that changes the size of a container. But array does have the begin() and end() methods, which allow you to use many of the range-based STL algorithms with array objects.

# # New STL Methods

C++11 adds cbegin() and cend() to the list of STL methods. Like begin() and end(), the new methods return iterators to the first element and to one past the last element of a container, thus specifying a range encompassing all the elements. In addition, the new
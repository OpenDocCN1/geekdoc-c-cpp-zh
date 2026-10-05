# 138 Introduction to C++

this code adds 5 to i, it does not change the values of the elements. If we want to change the values of the elements we use a reference. We'll discuss references in Chapter 16, for now, it is enough to know that a reference is an alias of the variable to which it refers. For example:

```
for(auto& i : arr) {
    i--;
    cout << i << '\n';
}
```

In each iteration, i is an alternate name for each element in the array. this is displayed. Note that we can use a reference to access the elements, even if we are not going to change their values. In fact, this is the most efficient approach, in order to avoid copying which may be expensive on time. If we don't want to change any value, we make the reference const in order to prevent any unintentional change. For example, the following code calculates the product of the array's elements:

```
int mul = 1, arr[] = {10, 20, 30, 40};
for(const auto& i : arr) {
    mul *= i;
}
```

Note that the ordinary for provides more abilities than the for range statement. With example, a for range we cannot change the values of two elements at the same time. Typically, the for range is used in simple loops to traverse all elements... since it does not have the possibility to exceed the array's bounds and insert a bug as in example C7.3. For more complicated loops, use the ordinary for.

# THE VECTOR CLASS

As we see in Chapter 26, the Standard Template Library (STL) contains a large collection of containers, iterators, function objects, and algorithms that offer a great variety of ways to access and your data. Like an array, a container can store many of elements. For example, the standard vector class is used to store all elements of the same type continuously. The vector class is one of the most useful STL containers, probably the most useful. This section provides a short description of its features.

Unlike arrays, we can specify the initial size of a vector object dynamically, and the most important, its size can grow dynamically whenever required. That is, vector class supports dynamic memory management that allows elements to be added or deleted while the program is running. Adding or deleting elements at the end of the vector is at a fixed cost, but the time required does not depend on the number of elements. Adding or deleting elements at the beginning or in the middle of the vector is

To use the vector class must include the vector file. To create a vector object we use the syntax <type> to specify the type of elements it will contain. The vector class supports various constructors to create objects. We'll discuss classes, objects, and constructors in Chapter 17. Until then, read this section to see examples of declaring vector objects:

```
vector<int> vec; // Create an empty vector of integers.
vector<int> vec(3, 20); // Create a vector of three integers set to 20.
vector<int> vec(1, 2, 3, 4); /* Create a vector of four integers with the
respective initial values. */
```
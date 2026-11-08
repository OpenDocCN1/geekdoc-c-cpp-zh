```
```cpp
bool longer(const std::string& one, const std::string& other)
{
    return one.length() > other.length();
}
```
```

This program prints out these results:

```
Minimum element: 13
Maximum element: 92
Alphabetically last name: Shemp
Longest name: Curly Joe
```

The first two calls to findOptimum() demonstrate that this function can indeed be used to find both the minimum and maximum numbers in a given vector. In passing, we illustrate a distinct function pointer that points to the instantiation of a function template such as greater<>() as well. All you have to do is explicitly instantiate the template by specifying all its template arguments between < and >.

The second half of the example is perhaps even more interesting. The default comparison operators of std::string, as you know, compare strings alphabetically. As in a phone book, Shemp would therefore always appear last. But there are times where you prefer to compare strings in a different manner. Adding callback parameters to functions such as findOptimum() facilitates this capability in Ex19_02 by looking for the longest string, by passing a pointer to longer() to findOptimum().

This example showcases the tremendous value of higher-order functions and callbacks in your never-ending battle against code duplication. If it weren’t for first-class functions, you would have had to write at least three distinct findOptimum() functions already only to make Ex19_02 work: findMinimum(), findMaximum(), and findLongest(). All three would then have contained the same loop to extract the corresponding optimum from a given vector. While for beginners it may be a great exercise to write such loops at least a couple of times, this soon gets old and certainly has no place in professional software development. Luckily, the Standard Library offers a vast collection of generic algorithms similar to findOptimum() that you can reuse instead, and all will accept similar callback functions that allow you to tune them to your needs. We’ll discuss this in more detail in the next chapter.

> **Note** First-class callback functions have plenty more uses beyond serving as the argument to higher-order functions. Callbacks are actively used in other aspects of day-to-day object-oriented programming as well. Objects often store callback functions in their member variables. Callback functions can serve any number of purposes. Callbacks could constitute user-configurable steps in the logic, or signal other objects that some event has occurred. Callbacks in all their forms facilitate various standard object-oriented idioms, most notably variations on the classical Observer pattern. Discussing object-oriented design falls outside of the scope of this book, though; there are other excellent books that specialize in this. You can find a basic example of a callback member variable in the exercises at the end of the chapter.
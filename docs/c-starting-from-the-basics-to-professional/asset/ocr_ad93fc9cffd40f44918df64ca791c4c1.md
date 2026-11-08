**Caution** `vector<>` also provides an `empty()` function, which is sometimes wrongly called in an attempt to clear a `vector<>`. But `empty()` does not empty a `vector<>`; `clear()` does. Instead, the `empty()` function checks whether a given container is empty. That is, `empty()` does not modify the container. Instead, it evaluates to a Boolean value of true if and only if the container is empty. The following statement is therefore almost certainly a mistake:

```
    data.empty();    // Remove all elements... or so I thought...
```

Fortunately, as of C++20 the definition of the `empty()` function is such that compilers are encouraged to issue a warning if you write code like that (give it a try!).

You can remove the last element from a vector object by calling its `pop_back()` function. Here's an example:

```
    std::vector numbers{ 7, 9, 7, 2, 0, 4 };
    numbers.pop_back();    // Remove the last element; numbers becomes { 7, 9, 7, 2, 0 }
```

This is by no means all there is to using `vector<>` containers. For instance, we showed you only how to remove all occurrences of an element, or elements at the back, while it's perfectly possible to erase any single element at any position. Similarly, we only showed you how to add elements at the back of a `vector<>`, while it's perfectly possible to insert elements at arbitrary positions. And so on. You'll learn more about working with `vector<>` containers in Chapter 20.

# ## Example and Conclusion

You are now in a position to create a new version of `Ex5_09.cpp` that uses only the memory required for the current input data:

```
    // Ex5_15.cpp
    // Sorting an array in ascending sequence - using a vector<> container
    import <iostream>;
    import <format>;
    import <vector>;

    int main()
    {
      std::vector<double> x;    // Stores data to be sorted

      while (true)
      {
        double input {};        // Temporary store for a value
        std::cout << "Enter a non-zero value, or 0 to end: ";
        std::cin >> input;
        if (input == 0)
          break;
```
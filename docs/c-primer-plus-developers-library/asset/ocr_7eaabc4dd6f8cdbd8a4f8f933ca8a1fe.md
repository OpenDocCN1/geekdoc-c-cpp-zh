+   9. Compared to an array, a linked list features easier addition and removal of elements but is slower to sort. This raises a possibility: Perhaps it might be faster to copy a list to an array, sort the array, and copy the sorted result back to the list than to simply use the list algorithm for sorting. (But it also could use more memory.) Test the speed hypothesis with the following approach:
+   
+       a. Create a large `vector<int>` object `vi0`, using `rand()` to provide initial values.
+   
+       b. Create a second `vector<int>` object `vi` and a `list<int>` object `li` of the same size as the original and initialize them to values in the original vector.
+   
+       c. Time how long the program takes to sort `vi` using the STL `sort()` algorithm, then time how long it takes to sort `li` using the `list sort()` method.
+   
+       d. Reset `li` to the unsorted contents of `vi0`. Time the combined operation of copying `li` to `vi`, sorting `vi`, and copying the result back to `li`.

To time these operations, you can use `clock()` from the `ctime` library. As in Listing 5.14, you can use this statement to start the first timing:

```
    clock_t start = clock();
```

Then use the following at the end of the operation to get the elapsed time:

```
    clock_t end = clock();
    cout << (double) (end - start) /CLOCKS_PER_SEC;
```

This is by no means a definitive test because the results will depend on a variety of factors, including available memory, whether multiprocessing is going on, and the size of the array or list. (One would expect the relative efficiency advantage of the array over the list to increase with the number of elements being sorted.) Also if you have a choice between a default build and a release build, use the release build for the measurement. With today's speedy computers, you probably will need to use as large an array as possible to get meaningful readings.You might try, for example, 100,000 elements, 1,000,000 elements, and 10,000,000 elements.

+   10. Modify Listing 16.9 (`vect3.cpp`) as follows:
+   
+       a. Add a `price` member to the `Review` structure.
+   
+       b. Instead of using a vector of `Review` objects to hold the input, use a vector of `shared_ptr<Review>` objects. Remember that a `shared_ptr` has to be initialized with a pointer returned by `new`.
+   
+       c. Follow the input stage with a loop that allows the user the following options for displaying books: in original order, in alphabetical order, in order of increasing ratings, in order of decreasing ratings, in order of increasing price, in order of decreasing price, and quitting.
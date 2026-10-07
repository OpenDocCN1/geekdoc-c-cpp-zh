
- 4. Write a function with an old-style interface that has this prototype:

```cpp
int reduce(long ar[], int n);
```

The actual arguments should be the name of an array and the number of elements in the array. The function should sort an array, remove duplicate values, and return a value equal to the number of elements in the reduced array. Write the function using STL functions. (If you decide to use the general unique() function, note that it returns the end of the resulting range.) Test the function in a short program.

- 5. Do the same problem as described in Programming Exercise 4, except make it a template function:

```cpp
template <class T>
int reduce(T ar[], int n);
```

Test the function in a short program, using both a long instantiation and a string instantiation.

- 6. Redo the example shown in Listing 12.12, the STL queue template class instead of the Queue class described in Chapter 12.

- 7. A common game is the lottery card. The card has numbered spots where a certain number are selected at random. Write a Lotto() function that takes two arguments. The first should be the number of spots on a lottery card, and the second should be the number of spots selected at random. The function should return a vector<int> object that contains, in sorted order, the numbers selected at random. For example, you could use the function as follows:

```cpp
vector<int> winners = Lotto(51, 6);
```

This would assign winners to a vector that contains six numbers selected randomly from the range 1 through 51. Note that using rand() doesn't quite do the job it may produce duplicate values. Suggestion: Have the function create a vector that contains all the spots, use random_shuffle(), and then use the beginning of the shuffled vector to obtain the values. Also write a short program that tests the function.

- 8. Mat and Pat want to invite their friends to a party. They want to write a program that does the following:

    - Allows Mat to enter a list of his friends' names. The names are stored in a container and then displayed in sorted order.
    - Allows Pat to enter a list of her friends' names. The names are stored in a container and then displayed in sorted order.
    - Creates a third container that merges the two lists, eliminates duplicates, and displays the contents of this container.

Compared to an array, a linked list features easier addition and removal of elements but is slower to sort. This raises a possibility: Perhaps it might be faster to copy a list to an array, sort the array, and copy the sorted result back to the list than simply use the list algorithm for sorting. (But it could use more memory). Test the speed hypothesis with the following approach:

    - a. Create a large vector<int> object vi, using rand() to provide initial values.
    - b. Create a second vector<int> object vi and a list<int> object li of the same size as the original and initialize it to values in the original vector.
    - c. Time how long the program takes to sort vi using the STL sort() algorithm, then how long it takes to sort li using the list sort() method.
    - d. Reset li to the unsorted contents of vi. Time the combined operation of copying li to vi, sorting vi, and copying the result back to li.

To time these operations, you can use clock() from the ctime library. As in 5.14, you can use this statement to start the first time:

```cpp
clock_t start = clock();
```

Then use the following at the end of the operation to get the elapsed time:
```cpp
clock_t end = clock();
cout << (double)(end - start)/CLOCKS_PER_SEC;
```

This is not a definitive test because the results will depend on a variety of factors, including available memory (which might cause the relative efficiency advantage of the array over the list to increase with the number of elements being sorted). Also if you have a choice between a default build and a release build, use the release build for the measurement. With today's computers, you will probably need to use as large an array as possible to get meaningful readings. You might try, for example, 10,000 elements, 1,000,000 elements, and 10,000,000 elements.

10. Modify Listing 16.9 (vect3.cpp) as follows:

    - a. Add a price member to the Review structure.
    - b. Instead of using a vector of Review objects to hold the input, use a vector of shared_ptr<Review> objects. Remember that a shared_ptr has to be initialized with a pointer returned by new.
    - c. Follow the input stage with a loop that allows the user the following options for displaying books: in original order, in alphabetical order, in order of increasing ratings, in order of decreasing ratings, in order of increasing price, in order of decreasing price, and quitting.

Here’s one possible approach. After getting the initial input, create another vector of shared_ptrs initialized to the original array. Define an operator< function that compares pointed-to structures and use it to sort the second vector so that the shared_ptrs are in the order of the book names stored in the pointed-to objects. Repeat the process to get vectors of shared_ptrs sorted by rating and by price. Note that rbegin() and rend() save you the trouble of also creating vectors of reversed order.

# Input, Output, and Files

In this chapter you'll learn about the following:

- The C++ input and output
- iostream class
- Redirection
- ostream class
- Formatting
- istream class
- Stream states
- File I/O
- Using ifstream class for input and output
- Using ofstream class for output
- Using fstream class for input and output
- Command-line processing
- Binary files
- Random file access
- Inc formatting

This chapter discusses C++ I/O. But first, let's examine the conceptual framework for

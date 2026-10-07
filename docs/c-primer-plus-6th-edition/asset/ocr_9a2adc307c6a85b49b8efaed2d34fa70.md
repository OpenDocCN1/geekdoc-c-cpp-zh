# Storage Duration, Scope, and Linkage

the 80 bytes of allocated memory available to another function, you need to pass or return its address to that function. On the other hand, if you declare p_fees with external link-age to that, the p_fees pointer will be available to all the functions following that declaration in the file. And by using the following in a second file, you make make that pointer available in the second file:

```
extern float * p_fees;
```

# Note

Memory allocated by new is typically freed when the program terminates. However, this is not always true. Under less robust operating systems, for example, in some circum-stances a request for a large block of memory can result in a block that is not deleted auto-matically when the program terminates. The best practice is to use delete to free memory allocated by new.

# Initialization with the new Operator

What if you want to initialize a variable as part of the dynamic memory allocation? With C++98, you can do so in some instances. C++11 expands what is possible. Let’s look first at what has been possible.

If you wish to create and initialize storage for one of the scalar built-in types, such as int or double, you can do so by following the desired type with an initialization value enclosed in parentheses:

```
int *pi = new int (6); // pi set to 6
double * pd = new double (99.99); // *pd set to 99.99
```

The parentheses syntax also be used with classes having suitable constructors, but we haven't got that far yet.

To initialize an ordinary structure or an array, you need C++11 and list-initialization using braces. The new standard allows:

```
struct where {double x; double y; double z};
where *one = new double {2.5, 5.3, 7.2}; // C++11
int *ar = new int {4, 4, 6, 7}; // C++11
```

With C++11, you can also use the brace initialization for single-valued variables:

```
int *pin = new int {}; // pi set to 6
double *pdo = new double {99.99}; // *pd set to 99.99
```

# When new Fails

It may be new can't find the requested amount of memory. For its first decade, C++ handled eventuality by returning a null pointer. Currently, new throws a std::bad_alloc exception. Chapter 15, "Friends, Exceptions, and More,” pro-vidas some examples showing how each approach works.
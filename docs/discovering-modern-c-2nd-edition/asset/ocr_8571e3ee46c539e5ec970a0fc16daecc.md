interface. There are other options that we will introduce later: specialization and meta-programming, which allow for type-dependent behavior.

As a case study, we use the function `accumulate` from the Standard Template Library, Section 4.1. It was developed at a time when programmers used pointers and ordinary arrays even more frequently than today. Thus, the STL creators Alex Stepanov and David Musser established an extremely versatile interface that works for pointers and arrays as well as on all containers of their library.

# 3.3.2.1 Genuine Array Summation

In order to sum the entries of an array generically, the first thing that comes to mind is probably a function that takes the address and size of the array:

Click here to view code image

```
template <typename T>
T sum(const T* array, int n)
{
    T sum(0);
    for(int i = 0; i < n; ++i)
        sum+= array[i];
    return sum;
}
```

This function can be called as expected:

Click here to view code image

```
int ai[] = {2, 4, 7};
double ad[] = {2., 4.5, 7.};

cout << "sum ai is " << sum(ai, 3) << '\n';
cout << "sum ad is " << sum(ad, 3) << '\n';
```

However, we might wonder why we need to pass the size of the array. Could not the compiler deduce it for us? After all, it is known during compilation. In order to use compiler deduction, we introduce a template parameter for the size and pass the array by reference:

Click here to view code image

```
template <typename T, unsigned N>
T sum(const T (&array)[N])
{
```
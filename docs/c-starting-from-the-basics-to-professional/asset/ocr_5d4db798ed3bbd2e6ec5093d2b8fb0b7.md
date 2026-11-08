All in all, it thus seems the best variation would be one that puts the type parameter T last (so that this type can be deduced), and uses auto for lower and upper (to avoid hard-coding their type):

```
```cpp
template <auto lower, auto upper, typename T>
bool is_in_range(const T& value)
{
    return (value <= upper) && (value >= lower);
}
```
```

That being said, in the case of the limits of is_in_range() you should probably use regular function parameters over template parameters. Function parameters give you the flexibility of being able to pass values that are calculated at runtime, whereas with template parameters you must supply the limits at compile time. We used the is_in_range() templates solely to explore the possibilities, not because any of them is an example of appropriate use of non-type template parameters.

Make no mistake, though: while relatively rare, non-type template parameters surely have their uses. We discuss one specific use case in the next subsection.

# Templates for Functions with Fixed-Size Array Arguments

In Chapter 8, in the section on passing arrays by reference, we defined the following function:

```
```cpp
double average10(const double (&array)[10])  // Only arrays of length 10 can be passed!
{
    double sum {};                            // Accumulate total in here
    for (size_t i {}; i < 10; ++i)
        sum += array[i];                       // Sum array elements
    return sum / 10;                           // Return average
}
```
```

Clearly, it would be great if you could create a function that would work for any array size, not just for arrays of exactly ten values. A template with non-type template arguments allows you to do this, as shown next. For good measure, we'll generalize it even further such that it works for arrays of any numerical type as well, not just for arrays of double:

```
```cpp
template <typename T, size_t N>
T average(const T (&array)[N])
{
    T sum {};                                 // Accumulate total in here
    for (size_t i {}; i < N; ++i)
        sum += array[i];                       // Sum array elements
    return sum / N;                            // Return average
}
```
```

Template argument deduction is even powerful enough to deduce the non-type template argument N from the type of the arguments passed to such a template. We can confirm this using a little test program:

```
```cpp
// Ex10_04.cpp
// Defining templates for functions that accept fixed-size arrays
import <iostream>;

template <typename T, size_t N>
T average(const T (&array)[N]);
```
```
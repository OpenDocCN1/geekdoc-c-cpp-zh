![](bbox=[0.3, 0.08, 0.65, 0.19])

# Figure 3-1: An array of length n with begin and end pointers

When software is written for maximal applicability, right-open intervals turned out to be more versatile than closed intervals, especially for types like lists where positions cannot (efficiently) be compared with <. The summation over a right-open interval can be implemented as shown in Listing 3-3.

# Listing 3-3: Sum of array entries

Click here to view code image

```
```cpp
template <typename T>
inline T accumulate_array(T* a, T* a_end)
{
    T sum(0);
    for (; a != a_end; ++a)
        sum+= *a;
    return sum;
}
```
```

and used as follows:

Click here to view code image

```
```cpp
int ai[] = {2, 4, 7};
double ad[] = {2., 4.5, 7.};

cout << "sum ai is " << accumulate_array(ai, &ai[3]) << '\n';
cout << "sum ad is " << accumulate_array(ad, ad+3) << '\n';
```
```

A pair of pointers representing a right-open interval as above is a Range: a very important concept in C++. Many algorithms in the standard library are implemented for ranges of pointer-like objects in a similar style to accumulate_array. To use such functions for new containers, we only need
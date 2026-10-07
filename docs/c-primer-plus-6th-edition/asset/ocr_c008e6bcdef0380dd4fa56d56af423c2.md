What effect does the stack destructor have on the strings? None. The class constructor uses new to create an array for holding pointers. The class destructor eliminates that array, not the strings to which the array elements pointed.

# An Array Template Example and Non-Type Arguments

Templates are frequently used for container classes because the idea of type parameters matches with the need to apply a common storage plan to a variety of types. Indeed, the desire to provide reusable code for container classes was the main motivation for introducing templates, so let's look at another example and explore a few more facets of template design and, in particular, let look at non-type, or expression, arguments and at using an array to handle an inheritance family.

Let's begin with a simple array template that lets you specify an array size. One technique, which the last version of the stack template uses, is to use a dynamic array within the class and a constructor to provide the number of elements. Another approach is to use a template argument to provide the size for a regular array. That is what the new C++11 array template does. Listing 14.17 shows a modern version of how this can be.

Listing 14.17 arraytp.h

```
//arraytp.h -- Array Template
#ifndef ARRAYTP_H_
#define ARRAYTP_H_

#include <iostream>
#include <cdef>

template <class T, int n>
class ArrayTP {
private:
    T ar[n];
public:
    ArrayTP() : {};
    explicit ArrayTP(const T & v);
    virtual T & operator[](int i);
    virtual T operator[](int i) const;
};

template <class T, int n>
ArrayTP<T,n>::ArrayTP(const T & v) 
{
    for (int i = 0; i < n; i++)
        ar[i] = v;
}
```
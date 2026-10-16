# 10.6.3.1 Parameters for Types

Here, the better way is to recognize that the only differences in any of these definitions are the three places where a type is specified. It would be nice if we could define the function and leave these types “blank” as in our earlier pattern and somehow pass the type to the function when we call it. Then we could replace all of these definitions with one.

This is effectively what C++ allows us to do, as shown in Example 10.9.

# Example 10.9 The swap() Template

```
/* This header file provides a template that generates functions
   for interchanging the values of two variables.
   ... remaining opening documentation omitted ...
---------------------------------------------------------------*/

template<typename Item>
inline void swap(Item & first, Item & second)
{
    Item temporary = first;
    first = second;
    second = temporary;
}
```

Rather than specify that the function is to exchange two values of a particular type such as char, int, and so on, this definition uses the identifier Item as a placeholder for the type of the value to be exchanged. More precisely, the line informs the compiler of two things:

+   1. This definition is a template: a pattern from which the compiler can create a function.
+   2. The identifier Item is the name of a type parameter for this definition that will be given a value when the function is called.

The rest of the definition simply specifies the behavior of the function, using the type parameter Item in place of any specific type.

Using this version of the swap library, we can now write

```
#include "swap.h"
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int i1 = 11,
        i2 = 22;
```

5 C++ also allows the keyword class to be used to specify a type parameter.
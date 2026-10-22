template parameter N (the value for which to compute the square root) and two other optional parameters. These optional parameters represent the minimum and maximum values the result can have. If the template is called with only one argument, we know that the square root is at least 1 and at most the value itself.

The recursion then proceeds using a binary search technique (often called *method of bisection* in this context). Inside the template, we compute whether **value** is in the first or the second half of the range between **LO** and **HI**. This case differentiation is done using the conditional operator ? :. If mid² is greater than N, we continue the search in the first half. If mid² is less than or equal to N, we use the same template for the second half again.

The partial specialization ends the recursive process when LO and HI have the same value M, which is our final **value**.

Template instantiations are not cheap: Even relatively modest class templates can allocate over a kilobyte of storage for every instance, and that storage cannot be reclaimed until compilation as completed. Let’s therefore examine the details of a simple program that uses our Sqrt template: Click here to view code image

meta/sqrt1.cpp

```
#include <iostream>
#include "sqrt1.hpp"

int main()
{
std::cout << "Sqrt<16>::value = " << Sqrt<16>::value << '\n';
std::cout << "Sqrt<25>::value = " << Sqrt<25>::value << '\n';
std::cout << "Sqrt<42>::value = " << Sqrt<42>::value << '\n';
std::cout << "Sqrt<1>::value = " << Sqrt<1>::value << '\n';
}
```

The expression

```
Sqrt<16>::value
```

is expanded to

```
Sqrt<16,1,16>::value
```

Inside the template, the metaprogram computes Sqrt<16,1,16>::value as follows: mid = (1+16+1)/2
= 9

Click here to view code image

```
value = (16<9*9) ? Sqrt<16,1,8>::value
: Sqrt<16,9,16>::value
```
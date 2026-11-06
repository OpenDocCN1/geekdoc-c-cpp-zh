The third decision you must make is how inclusive to make the template. In some cases, you want to create a template that can handle a range of situations. However, a template can quickly become unwieldy and difficult to manage. A good template is balanced — it includes the elements you need, but nothing beyond.

# # Creating a Basic Math Template

With a math template, you usually need access to a wealth of calculations but may only use one or two of those calculations at a time. For example, if someone is calculating your mortgage, he or she doesn't need to know the amortization calculation. However, the person might need the amortization calculation when working with the next customer. In short, the calculations all have a purpose and you need them all, but you don't need them all at the same time. Because of the way you use math templates, they work best as a series of function templates. The MathTemplate example in Listing 3-1 shows how to create the series of functions.

# ### Listing 3-1: Defining a Series of Function Templates

```
```cpp
#include <iostream>
#include <cmath>

using namespace std;

template<typename T>
T Area(T height, T length)
{
    return height * length;
}

const double PI = 4.0*atan(1.0);

template<typename T>
T CircleArea(T radius)
{
    double result;

    result = PI * radius * radius;

    // This version truncates the value.
    return (T)result;
}

template<typename T>
T TriangleArea(T base, T height)
{
    double result;

    result = base * height * 0.5;

    return (T)result;
}
```
```
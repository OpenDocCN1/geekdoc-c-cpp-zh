# 100 3 Functions

For some simple, small, but frequently used functions, we can use inline functions. An inline function does not cause control transfer when it is called, but makes itself embedded in every place it is called during the compilation. In this way, the cost of passing parameters and control transfers can be saved.

Inline functions use the keyword "inline" in the function definition. The form is

```
inline Type identifier Function name (Parameters) { Function body; }
```

There are several points that require our attention when using inline functions:

+   - Generally, loop statements and switch statements should not appear in an inline function.
- Inline functions must be defined before their first call.
- Inline functions do not support abnormal interface statements. (Abnormal interface statements will be discussed in Chapter 12)

Generally, inline functions should be simple functions, with simple structures and few statements. Defining a complex function as an inline function may lead to code bloat and also increase the cost. In this case, most compilers will automatically convert the inline function into a common function before processing. What kind of functions should be counted as complex? The answer depends on compilers. Generally, functions that have loop statements cannot be processed as inline functions.

Therefore, the keyword inline is just a request. The compiler does not promise that every function with the keyword inline will be processed as an inline function. Moreover, functions without the inline keyword can possibly be compiled as inline functions.

Example 3.14: An example of an inline function.

```
//3_14.cpp
#include<iostream>
using namespace std;
inline double CalArea(double radius) //Inline function, to calculate
// the area of a circle
{
    return 3.14*radius*radius;
}

int main()
{
    double r(3.0); //r is the radius of the circle
    double area;
    area=CalArea(r);
}
```
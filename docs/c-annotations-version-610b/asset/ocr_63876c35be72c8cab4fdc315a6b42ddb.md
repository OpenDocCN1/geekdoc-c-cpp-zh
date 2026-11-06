```
```
return d_name;
}
```
```

If it is ever necessary to cancel `Person::name`'s inline implementation, then this becomes its non-inline implementation:

```
```cpp
#include "person.ih"

std::string const &Person::name() const
{
    return d_name;
}
```
```

Only the `inline` keyword needs to be removed to obtain the correct non-inline implementation.

Defining members inline has the following effect: whenever an inline-defined function is called, the compiler may *insert the function's body* at the location of the function call. It may be that the function itself is never actually called.

This construction, where the function code itself is inserted rather than a call to the function, is called an inline function. Note that using inline functions may result in multiple occurrences of the code of those functions in a program: one copy for each invocation of the inline function. This is probably OK if the function is a small one, and needs to be executed fast. It's not so desirable if the code of the function is extensive. The compiler knows this too, and handles the use of inline functions as a *request* rather than a *command*. If the compiler considers the function too long, it will not grant the request. Instead it will treat the function as a normal function.

# ### 7.7.2 When to use inline functions

When should inline functions be used, and when not? There are some rules of thumb which may be followed:

+   - In general inline functions should **not** be used. *Voila*; that's simple, isn't it?
+   - Consider defining a function inline once a fully developed and tested program runs too slowly and shows 'bottlenecks' in certain functions, and the bottleneck is removed by defining inline members. A profiler, which runs a program and determines where most of the time is spent, is necessary to perform such optimizations.
+   - Defining inline functions may be considered when they consist of one very simple statement (such as the return statement in the function `Person::name`).
+   - When a function is defined inline, its implementation is inserted in the code wherever the function is used. As a consequence, when the *implementation* of the inline function changes, all sources using the inline function must be recompiled. In practice that means that all functions must be recompiled that include (either directly or indirectly) the header file of the class in which the inline function is defined. Not a very attractive prospect.
+   - It is only useful to implement an inline function when the time spent during a function call is long compared to the time spent by the function's body. An example of an inline function which hardly affects the program's speed is:

```
```cpp
inline void Person::printname() const
{
    cout << d_name << '\n';
}
```
```

This function contains only one statement. However, the statement takes a relatively long time to execute. In general, functions which perform input and output take lots of time. The effect of the
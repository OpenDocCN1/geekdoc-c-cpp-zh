Passing a function to a C++ function can also prove difficult unless you rely on the Standard Library. For example, you can use a transform to interact with a range of values by passing the transform function. As part of the strategy of passing functions to other functions, you can rely on lambda expressions for simple needs. However, passing complex functions is possible as well. When working with complex functions, however, many developers encase them in a typedef to make the code easier to read.

To create a pure function in C++, you must eliminate both state and side effects, which can be quite difficult. The process becomes especially difficult when working with external data, such as a file or a data stream. Obviously, a function that works with external data won't produce the same output every time you call it, but you can still reduce the problems of both state and side effects.

Even the use of recursion in place of the usual for or other looping mechanism can prove difficult in C++. In many cases, recursion relies on the use of mutable variables to track when the recursion should end. Careful use of various recursion strategies can make the use of mutable variables unnecessary, but doing so can be error prone and difficult (sometimes making the code hard to read).

![](bbox=[0.19, 0.51, 0.25, 0.57])

The takeaway from this section is that you can use C++ in a functional manner, but it requires additional work to do so. The benefits of this approach are that multiprocessing applications are easier to create, the code is more concise, and the code is often easier to understand as well. In some cases, you can't use a functional programming style, especially when interacting with third-party libraries. However, if you work through coding issues using the Standard Library and some built-in C++ features, you can find yourself creating mostly functional code and obtaining the desired benefits from doing so.

# # Seeing Data as Immutable

Being able to change the content of a variable is problematic in C++. The memory location used by the variable is important. If the data in a particular memory location changes, the value of the variable pointing to that memory location changes as well. The concept of immutable data requires that specific memory locations remain untainted. To create immutable data in C++, you must use constant variables, as in

```
```cpp
const double pi = 3.1415926;
```
```

The reason you need an immutable variable is that in a multiprocessing scenario, the value of the variable must be the same no matter which processor works with
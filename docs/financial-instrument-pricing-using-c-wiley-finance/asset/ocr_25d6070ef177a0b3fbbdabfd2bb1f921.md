We wish to assign a function to any of the above member functions at run-time. The following code shows how to do it:

```
```cpp
// Binding and polymorphism
typedef std::function <void ()> FunType3;
Base* b = new D;
FunType3 myF3 = std::bind(&Base::print,b);
myF3(); // Derived class D print will be called

delete b;
b = new D2;
myF3(); // Derived class D2 print will be called

delete b;
```
```

In this way we can achieve high levels of customisability using bind in our code. A separate issue is to measure the relative performance.

# 3.7 APPLICATION AREAS

We have now completed our discussion of some of the ways to model functions in C++. The new features are to be found in the C++ standard and are essentially based on the functional programming model, allowing us to write code that is more flexible than code based exclusively on subtype polymorphism. We shall see examples of these features as we progress in this book. Furthermore, we can integrate functions, data types and data containers to form generic and reusable structures for numerical applications. A preview of some examples is:

+   - Improvements to the STL, for example the new `bind()` functionality and the ability to use lambda functions with STL algorithms.
+   - New data types such as `std::tuple`, `std::array<>` and `boost::variant` that we can use as function arguments and return types.
+   - Re-engineering of the somewhat outdated GOF patterns (GOF, 1995) to subsume the object-oriented, generic and functional programming models. The resulting design patterns are very flexible and more reliable than the GOF patterns.
+   - Using `std::function` to model C++ classes for stochastic differential equations (SDEs) and partial differential equations (PDEs).

# 3.8 AN EXAMPLE: *STRATEGY* PATTERN NEW STYLE

We take an example that shows what we wish to achieve in later chapters. In order to scope the problem, we create a class called Point that implements points in two-dimensional space. What is special about the problem is that we create a customisable function that calculates the distance between two points. Furthermore, we have two major requirements concerning the flexibility of the proposed solution:

+   - It should use the Strategy design pattern (GOF, 1995) because this is based on the object-oriented model in conjunction with subtype polymorphism (using virtual functions).
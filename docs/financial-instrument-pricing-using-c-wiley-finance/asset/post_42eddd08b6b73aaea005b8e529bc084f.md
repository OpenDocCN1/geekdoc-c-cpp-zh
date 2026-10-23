
```
fun = pc;
fun(3.0);
```

In this case, creating a function object is more time consuming than creating a lambda function. And we usually save it in a separate file while a lambda function can be defined at the point where it is needed.

## 3.6.2 Binding and Free Functions

It is possible to use `bind()` with free functions. We give examples of free functions of arity two and one, respectively:

```cpp
double func(double a, double b)
{
    return a - b;
}
```

```cpp
double func1(double x)
{
    return exp(x);
}
```

For example, these functions could be defined in a library of algorithms (of course, the code would be more complex in real software systems) and we wish to experiment with these functions in client code. The code was ported from the Boost C++ Bind library and this was a relatively painless process. We only needed to change the namespace from `boost` to `std` and redefine placeholders. The code is:

```cpp
// Port from Boost Bind

using namespace std::placeholders;

// Bind params 1 and 2, answer = -1
double result = (std::bind(&func, _1, _2))(1.0, 2.0);
std::cout << "_1, _2: " << result << std::endl;

// Bind params 2 and 1, answer = 1
result = (std::bind(&func, _2, _1))(1.0, 2.0);
std::cout << "_2, _1: " << result << std::endl;

// Binding to params chosen at run-time
std::cout << "Give a value 1: "; int v1; std::cin >> v1;
std::cout << "Give a value 2: "; int v2; std::cin >> v2;

result = (std::bind(&func, _1, _2))(v1, v2);
std::cout << "_1, _2: " << result << std::endl;

// Using placeholders in more than one place in an expression
result = (std::bind(&func, _1, _1))(v1, v2);

std::cout << "_1, _1: " << result << std::endl;

result = (std::bind(&func, _2, _2))(v1, v2);
std::cout << "_2, _2: " << result << std::endl;

std::function<double (double x)> fA; // Preferred form
fA = func1;
std::cout << "Value: " << fA(0.0);
```

We recommend that you run this code and inspect the output in order to understand this somewhat cryptic syntax.

We need to understand the relationship between placeholders, formal function arguments and how placeholders are assigned to values. As an example, we have:

```cpp
result = (std::bind(&func, _2, _1))(1.0, 2.0);

double func(double a, double b)
{
    return a - b;
}
```

In this case placeholder `_2` is assigned the value `2.0` and it corresponds to formal variable `a` while placeholder `_1` is assigned value `1.0` and it corresponds to formal variable `b`. In this sense the placeholder is a mediator between a function’s formal parameter and the value assigned to that parameter. Thus, the result of calling this function is `1.0`.

## 3.6.3 Binding and Subtype Polymorphism

We investigate the possibility of using virtual member functions with `bind()`. In particular, we would like to bind to a base class’s polymorphic member function and to change the base class pointer at run-time. We consider the following class hierarchy:

```cpp
class Base
{
public:
    virtual void print() const { std::cout << "Base\n"; }
};

class D : public Base
{
public:
    void print() const { std::cout << "Derived\n"; }
};

class D2 : public Base
{
public:
    void print() const { std::cout << "Derived2\n"; }
};
```

We wish to assign a function to any of the above member functions at run-time. The following code shows how to do it:

```cpp
// Binding and polymorphism
typedef std::function <void ()> FunType3;
Base* b = new D;
FunType3 myF3 = std::bind(&Base::print, b);
myF3(); // Derived class D print will be called

delete b;
b = new D2;
myF3(); // Derived class D2 print will be called

delete b;
```

In this way we can achieve high levels of customisability using `bind` in our code. A separate issue is to measure the relative performance.

## 3.7 APPLICATION AREAS

We have now completed our discussion of some of the ways to model functions in C++. The new features are to be found in the C++ standard and are essentially based on the functional programming model, allowing us to write code that is more flexible than code based exclusively on subtype polymorphism. We shall see examples of these features as we progress in this book. Furthermore, we can integrate functions, data types and data containers to form generic and reusable structures for numerical applications. A preview of some examples is:

- Improvements to the STL, for example the new `bind()` functionality and the ability to use lambda functions with STL algorithms.
- New data types such as `std::tuple`, `std::array<>` and `boost::variant` that we can use as function arguments and return types.
- Re-engineering of the somewhat outdated GOF patterns (GOF, 1995) to subsume the object-oriented, generic and functional programming models. The resulting design patterns are very flexible and more reliable than the GOF patterns.
- Using `std::function` to model C++ classes for stochastic differential equations (SDEs) and partial differential equations (PDEs).

## 3.8 AN EXAMPLE: *STRATEGY* PATTERN NEW STYLE

We take an example that shows what we wish to achieve in later chapters. In order to scope the problem, we create a class called `Point` that implements points in two-dimensional space. What is special about the problem is that we create a customisable function that calculates the distance between two points. Furthermore, we have two major requirements concerning the flexibility of the proposed solution:

- It should use the Strategy design pattern (GOF, 1995) because this is based on the object-oriented model in conjunction with subtype polymorphism (using virtual functions).

```cpp
// Assignment operator
Point<X>& operator = (const Point<X>& source);

template <class X>
    friend std::ostream& operator<<(std::ostream& os, const Point<X>& p);
};
```

We can create points by providing them with some implementation of `FunctionType`. We define two specific functions:

```cpp
// Algorithms for calculating distances between points using
// 'double' in this case
double ExactDistance(const Point<double>& p, const Point<double>& p2)
{ // Exact distance as a C function with no state

    // Get the length of the sides
    double a = p.First() - p2.First();
    double b = p.Second() - p2.Second();

    // Use Pythagoras' theorem to calculate distance
    return std::sqrt(a*a + b*b);
}

struct ApproxDistance
{ // Approximate distance as a function object with extra state; this is
  // in essence a wrapper for an algorithm containing its own
  // private state

    // Stick on an extra 'margin' to the calculated distance
    double extra;

    ApproxDistance(double margin): extra(margin) {}

    double operator () (const Point<double>& p, const Point<double>& p2) const
    {
        std::cout << extra;
        return ExactDistance(p, p2) * (1.0 + extra);
    }
};
```

We can now use these algorithms in client code:

```cpp
// The case of stateful delegation (Composition); N.B. each object is
// born with its own algorithm so that there is asymmetry in the calls
// on individual points. The distance from point p1 to point p2 is not
// necessarily the same as from p2 to p1.
Point<double> pA(1.0, 1.0, ExactDistance);

std::cout << "Give margin as fraction [0.0,1.0] please: "; double myMargin;

std::cin >> myMargin;

ApproxDistance taxiObject(myMargin);
Point<double> pB(taxiObject);

std::cout << "Exact distance between A and B points: " << pA.Distance(pB);
std::cout << "Approximate distance: " << pB.Distance(pA);
```

Summarising, we have given a typical example of *composition-based delegation* which is one of the fundamental design techniques to implement many of the design patterns in GOF (1995). However, the GOF patterns are based on the traditional object model which is less flexible it seems than the combination of the object, generic and functional models that we introduce in this book.

## 3.9 MIGRATING FROM TRADITIONAL OBJECT-ORIENTED SOLUTIONS: NUMERICAL QUADRATURE

In Duffy (2004) and Duffy and Kienitz (2009) we discussed a number of classes and code to numerically integrate scalar-valued functions of one variable using the *midpoint rule* and the *Monte Carlo ‘hit or miss’ rule*. The approach used has the following characteristics and shortcomings:

- a) The function to be integrated is a global function (function pointer).
- b) We used the *Bridge* design pattern (GOF, 1995) using raw pointers, subtype polymorphism and object-level composition. We need to pay attention to performance and memory management issues.
- c) Function names have not been standardised, making it difficult to use with other software.
- d) Clients who wish to define their own numerical quadrature schemes must create classes that are derived from a common base class (called `IntegratorImp`).

We have used a combination of C (function pointers), C++ and OOP design patterns. We will rectify these problems by using `std::function<>` to implement the *integrand* (function to be integrated) and the numerical quadrature schemes. Furthermore, the current solution does not allow much flexibility regarding customisability of input and output. For example, some future requirements are:

- e) Absolute and relative accuracy required.
- f) The ability to define user break points in the interval of integration where local difficulties may occur, for example singularities and discontinuities in the integrand.
- g) Output: estimate of the absolute error.
- h) Output: number of function evaluations needed during the execution of the numerical quadrature scheme.

We address issues a) to d) in this chapter while we discuss the other topics in Chapter 19 in the context of the numerical solution of the nonlinear equations. The motivation for the new design is to first define the signature of the function that models the integrand and then to define the signature of the functions that implement numerical quadrature schemes. The input

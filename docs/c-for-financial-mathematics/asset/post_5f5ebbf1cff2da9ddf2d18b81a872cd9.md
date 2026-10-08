
The library `<algorithm>` contains a number of functions that are very useful for working with containers such as `find`.

- Different data structures have different performance characteristics. You should choose your data structure based on how you intend to access and update the data.
- You should not store large objects in containers. Store them by reference using `shared_ptr` instead.

We should add that although the standard template library is very powerful, it is also rather difficult to learn. Unfortunately it makes heavy use of sophisticated ideas such as templates and operator over-loading. The syntax chosen for iterators also assumes that you are very used to working with pointers and so will find the use of `*` and `++` to be natural and convenient.

When the standard template library was first invented it was rather experimental. Time has shown that the object-oriented programming style is quite intuitive. For this reason many computer languages include some form of object orientation. On the other hand, the standard template library is quite difficult to grasp for new programmers. As a result, the use of templates has not been adopted in many other languages.

> **Tip: Use the standard template library, but don’t copy its design.**

You should know how to use the standard template library as it contains invaluable tools. Nevertheless, you should not rush to copy the design of the standard template library. See if you can find an object-oriented solution to your problem before using templates.

## Chapter 19

# Function Objects and Lambda Functions

In Section 10.6 we designed an interface `RealFunction` to represent the mathematical notion of a function mapping real numbers to real numbers. This solved the problem of writing an integration routine that can integrate any real function.

However, there is a better solution in C++, called writing *function objects*. A function object is simply an instance of a class that overloads the operator `()`. Function objects are also sometimes called *functors*. The big advantage of using function objects is that there is a special syntax for writing function objects called *lambda functions*. This makes it quicker to write a function object than a normal class.

### 19.1 Function objects

Here is an example of an integration function which takes as a parameter a function object `f`. This code simply repeats the function we used in Section 10.6 to integrate using the rectangle rule, but this time we are using a function object rather than the interface `RealFunction`.

```cpp
double integrate(
    function<double(double)> f,
    double a,
    double b,
    int nSteps) {
 double total = 0.0;
 double h = (b - a) / nSteps;
 for (int i = 0; i<nSteps; i++) {
    double x = a + i*h + 0.5*h;
    total += h*f(x);
 }
 return total;
}
```

The first thing to notice is that the type of **f** is declared as

```cpp
function<double(double)> f
```

Here **function** is a class defined in the library `<functional>` and in the namespace **std**. The interesting bit is the template type. This example means that **f** represents a function that returns a double and takes a single **double** as a parameter. If you wish to use function objects with different return and parameter types, the general syntax is:

```cpp
function<ReturnType(ParameterType1,ParameterType2,...)> f
```

Declaring the type of the function is the only complex part of using function objects. When we use the function object **f** it is just the same as using an ordinary function because it has overidden the operator **()**. Here is the line of code where **f** is used:

```cpp
total += h*f(x);
```

To write a function object, you must write a class which overloads the **()** operator. Here is an example of a class for evaluating the mathematical function $\sin(x)$.

```cpp
class SinFunction {
public:
	double operator()(double x) {
		return sin(x);
	}
};
```

Putting everything together, here is a test that our integration function works as expected.

```cpp
void testIntegrateSin() {
	SinFunction integrand;
	double value = integrate(integrand, 0, 1, 1000);
	ASSERT_APPROX_EQUAL(-cos(1.0) + cos(0.0),
		value, 0.01);
}
```

### 19.2 Lambda functions

The big advantage of using function objects rather than writing your own interface is that you can use *lambda functions* to write function objects very quickly.

As an example, suppose that we want to write a function that takes parameters $a$, $b$ and $c$ and then computes

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_353_0.png)

using the trapezium rule. We will first need to write a function object to compute the integrand $ax^{2}+bx+c$. We can then compute the integral using our integrate function.

Here is the long answer which doesn’t use lambda functions:

```cpp
class QuadraticFunction {
public:
    /* Members */
    double a;
    double b;
    double c;
    /* Constructor */
    QuadraticFunction(double a,
                      double b,
                      double c) :
        a(a), b(b), c(c) {}
    /* Operator */
    double operator()(double x) {
        return a*x*x+b*x+c;
    }
};

double integrateQuadratic(double a,
                          double b,
                          double c) {
    QuadraticFunction integrand(a, b, c);
    return integrate(integrand, 0, 1, 1000);
}
```

We have to define a class, give it appropriate member variables and a constructor, and override the operator (). We then need to construct an instance of this class and pass it to integrate. A lambda function allows us to do all of this in only a few lines.

```cpp
double integrateQuadratic2(double a,
                           double b,
                           double c) {
    auto lambda =
        [a, b, c](double x) {
            return a*x*x + b*x + c;
        };
    return integrate(lambda, 0, 1, 1000);
}
```

The variable `lambda` is still a function object, just as `integrand` was in the more verbose version of the code. The new syntax is the declaration of the lambda function:

```cpp
[a, b, c](double x) {
    return a*x*x + b*x + c;
};
```

This is an extremely concise syntax which means:

- Generate a class, we don't care what it is called.
- We will want to *capture* the local variables a, b, and c of `integrateQuadratic2` and have them as member variables of our class. When writing a lambda function, you list the captured variables in square brackets.
- We want to write an overload of operator `()` that takes a single `double` parameter which we will call `x`. When writing a lambda function, you list the parameter types and parameter names in round brackets.
- The actual computation for the function is written inside curly brackets and can use both the captured variables and the parameters.

In summary, the syntax of a lambda function is:

```
[CaptureParameters] (FunctionParameters) {FunctionImplementation}
```

The great thing about lambda functions is that as well as being quicker to write, they are easier to read (at least when you are used to the syntax). This is because all the verbose and distracting boiler plate code needed to define a new class is hidden.

There is a lot of flexibility in how you write the capture parameters.

1. You can specify that you would like to capture local variables by reference, by using the `&` symbol before the parameter name.
2. You can specify that you would like to capture all variables by reference simply by specifying just `&`.
3. You can specify that you would like to capture all variables by value, by specifying just `=`.
4. If your lambda function is written inside a member function of a class, you can capture the member functions and member variables of that class by specifying `this`.

As an example, here is how to integrate the payoff of a path-independent option between the limits $a$ and $b$.

```cpp
     double integratePayoff (PathIndependentOption& o,
                             double a,
                             double b) {
       auto lambda =
         [&o](double x) {
             return o.payoff(x);
         };
       return integrate(lambda, a, b, 1000);
     }
```

Since the class PathIndependentOption is abstract, we must capture the variable $\text{o}$ by reference. This is why the list of capture parameters says we are capturing $\text{\&o}$.

This same problem was considered in Section 10.6. As you can see, the use of lambda functions makes the solution much shorter.

Notice that when you store capture parameters by reference, you must always be careful to ensure that function object will be deleted before any of the parameters it has captured. This is for precisely the same reason as one needs to ensure that an instance of a class is deleted before any member variables that are stored by reference.

### 19.3 Function pointers

It is possible to pass an actual function as a parameter, it is not always absolutely necessary to write a function object. For example, to integrate

$$
\int_0^1 (x^2 + 2x + 1) dx
$$

we can write an ordinary function representing the integrand as follows:

```cpp
static double integrand(double x) {
  return x*x + 2 * x + 1;
}
```

We can then pass this integrand to our integrate function as follows.

```cpp
double testIntegrateFunctionPointer() {
  double value = integrate(&integrand, 2, 1);
  ASSERT_APPROX_EQUAL(
    value,
```

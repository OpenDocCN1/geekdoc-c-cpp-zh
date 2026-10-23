```
{
    return h1(t)*f(x...) + h2(t)*g(x...);
};
};
```

An example of use is:

```
FunctionType<double, double> h1 = [] (double t) {return 1.0 -t; };
FunctionType<double, double> h2 = [=] (double t) { return t; };

auto hom2 = homotopyII(f, g, h1, h2);

t = 0.5;
x = 3.0;
std::cout << "Homotopy II: " << hom2(x, t) << '\n';
```

It is possible to simplify the homotopy to one that only needs the mappings f and g as input:

```
auto convexHomotopy = [=] (auto f, auto g)
{ // Homotopy of functions

    // t is usually a scalar while x can be a list of arguments

    auto h1 = [] (double t) { return 1.0 - t; };
    auto h2 = [] (double t) { return t; };

    return [=] (double x, auto&&... t)
    {
        return h1(t)*f(x...) + h2(t)*g(x...);
    };
};
```

In this case we have 'hidden' lambda functions h₁ and h₂ inside this generic lambda.

An example of use is:

```
auto hom3 = convexHomotopy(f, g);
t = 0.25;
x = 4.0;
std::cout << "Homotopy III: " << hom3(t, x) << '\n'; // 13
```

We note that we have changed the relative order of the arguments in the definition of the homotopy in equation (6.1) and its implementation in C++. This is because the time variable t is always a scalar and the state variable is a point in n-dimensional space in general and it will be implemented as a variadic argument. In C++ the compiler complains if the variadic argument is placed before the fixed parameter, hence the reason why the relative order is different between the mathematical and C++ representations.

Finally we give some examples of homotopy mappings that are used in numerical analysis (Allgower and Georg, 2003):

```
```cpp
auto homotopyII = [=] (auto f, auto g, auto h1, auto h2)
{ // Homotopy of functions

    return [=](auto&& t, auto&&... x)
    {
        return h1(t)*f(x...) + h2(t)*g(x...);
    };
};

auto convexHomotopy = [=] (auto f, auto g)
{ // Homotopy of functions

    auto h1 = [](double t) { return 1.0 - t; };
    auto h2 = [](double t) { return t; };

    return [=](auto&& t, auto&&... x)
    {
        return h1(t)*f(x...) + h2(t)*g(x...);
    };
};

auto canonicalHomotopy = [=](auto f, auto&&... x0)
{ // Global homotopy of functions

    return [=](auto&& t, auto&&... x)
    {
        return f(x...) + (t - 1.0)*f(x0...);
    };
};
```
```

We conclude this section with a very brief discussion on how to apply homotopy methods to find the solution to nonlinear systems of equations (Allgower and Georg, 2003):

$$F(x)=0,\quad F:\mathbb{R}^n\to\mathbb{R}^n.$$

In many cases it is difficult to find a solution, mainly because we need a good initial guess at the true solution. Homotopy methods are less sensitive to this problem and to this end we embed the above nonlinear system in a homotopy:

$$h(x,t)=(1-t)\{F(x)-F(x_0)\}+tF(x)=F(x)-(1-t)F(x_0)$$

where $x_0$ is an arbitrary initial guess.

We solve this modified system (see Allgower and Georg, 2003) from $t=0$ to $t=1$. At $t=0$, the solution is $x=x_0$ (which we already know because $x_0$ is given) and we must come up with a scheme that drives a solution to t = 1 in which case we have found the solution of the original problem. The C++ code to model the homotopy is:

```
auto canonicalHomotopy = [=](auto f, auto&&... x0)
{ // Homotopy of functions

    // t is usually a scalar while x can be a list of arguments

    return [=](auto&& t, auto&&... x)
    {
        return f(x...) + (t - 1.0)*f(x0...);
    };
};
```

An example of use is:

```
t = 0.25;
x = 6.0;

double x0 = 2.0;
auto hom5 = canonicalHomotopy(f, x0);
std::cout << "Homotopy V: " << hom5(t, x) << '\n'; // 33
```

The numerical details of solving nonlinear systems using homotopy/continuation methods are given in Allgower and Georg (2003).

## 6.7 GENERALISED LAMBDA CAPTURE

We have already discussed captured variables in the context of lambda functions in Chapter 3. In this section we discuss several capture modes:

- S1: By value: the value is copied into the body of the lambda function.
- S2: By reference: the lambda function uses the ‘live’ variable that is defined outside of the function.
- S3: Generalised lambda capture (init capture) using local (stack) variables: the variable is only defined in the body of the lambda function (this is similar to the use of local variables in the Boost Phoenix library (Demming and Duffy, 2010).
- S4: Using move semantics: the encompassing variable is moved into a variable in the lambda function.

The main challenge is to determine which of these options to use in a given context. Each option has its own pitfalls. For example, option S1 may not work for types for which the copy constructor is not defined. Reference capture (case S2) can lead to dangling references, for example when a variable goes out of scope before the lambda function that uses it is called. Thus, when the lambda function has been called the variable no longer exists!

In this section we focus on cases S3 and S4. To this end, an example of S3 is:

```
void CaptureLocalVariable()
{
    // C++14 init capture with local variables
    int x = 1'000; // This is a digit separator
    auto fun4 = [&r = x]()
    {
        r *= 2;
        std::cout << "\nr: " << r << '\n';
    };

    // Undefined r
    // std::cout << r << '\n';

    fun4(); // Prints the value 2000
}
```

In this case the lifetime of the local variable x is the scope of the lambda function itself.

We now take an example of a mutable lambda function which processes a vector that has already been initialised outside the scope of the lambda function and that is modified in the body of the function. We present four alternatives.

First, capture by reference is:

```
int size = 4; double val = 2.71;
std::vector<double> data(size, val);

// By reference capture mode
auto fun = [&data]() mutable
{
    std::cout << "Vector by reference, values being changed\n";
    for (std::size_t i = 0; i < data.size(); ++i)
    {
        data[i] = 3.14; std::cout << data[i] << ",";
    }

    std::cout << '\n';
};
fun();

// data still exists and has been modified
for (std::size_t i = 0; i < data.size(); ++i)
std::cout << data[i] << ";"; }
```

Second, capture by value is:

```
std::cout << "Capture by value:\n";
int size = 4; double val = -99.99;
std::vector<double> data(size, val);
```

```
// all captured variables are copied
auto fun4 = [=]() mutable
{
    for (std::size_t i = 0; i < data.size(); ++i)
    { data[i] = 42.00; std::cout << data[i] << ","; }
    std::cout << '\n';
};
fun4();

// What has changed? No, we get the old ones i.e -99.99!
for (auto elem : data) { std::cout << elem << ","; }
```

Third, capture by using local variables in combination with a move is:

```
// Using local variable for capture
int size2 = 6; double val2 = 5.0;
std::vector<double> newData(size2, val2);

auto fun3 = [&localData = std::move(newData)]() mutable
{
    for (std::size_t i = 0; i < localData.size(); ++i)
    { localData[i] = 148.413; std::cout << localData[i] << ","; }
    std::cout << '\n';
};
fun3();
```

Finally, the solution using move semantics is:

```
// C++14 init capture
int sz = 5; double d = 1.414;
std::vector<double> arr(sz, d);
auto fun2 = [myData = std::move(arr)]() mutable
{
    std::cout << '\n';
    for (std::size_t i = 0; i < myData.size(); ++i)
    { myData[i] = 93.8344; std::cout << myData[i] << ","; }
    std::cout << '\n';
};
fun2();
```

It is instructive to run the code. For more complex cases, it might be an option to use function objects instead of lambda functions.

### 6.7.1 Living Without Generalised Lambda Capture

Generalised lambda capture is a C++14 feature. Before C++14 we had to depend on C++11 in combination with std::bind in order to emulate the feature. You may prefer to use the C++14 option instead due to the fact that std::bind syntax can be cryptic at times.

The example that we take is as before: we create a lambda function that accepts a vector as input and prints it. The point to note is that std::bind accepts a lambda function as input argument which is bound to a moved vector std::move(data2), as the following code shows:

```
void CaptureEmulation()
{ // Emulating generalized lambda capture with C++11

    std::cout << "\nCapture in C++11 and std::bind\n";
    int size2 = 3; double val2 = 1.41;
    std::vector<double> data2(size2, val2);
    auto fun3 = std::bind([](std::vector<double>& array)
    {
        for (std::size_t i = 0; i < array.size(); ++i)
        {
            std::cout << array[i] << "/";
        }

    }, std::move(data2));
    fun3();

    if (0 == data2.size())
    {
        std::cout << "\nDouble array has no elements, OK\n";
    }
    else
    {
        std::cout << "\n Ouch!\n";
        for (std::size_t i = 0; i < data2.size(); ++i)
        {
            std::cout << data2[i];
        }
    }
}
```

The above code is quite clumsy in our opinion. C++14 syntax is preferable, hence we do not use the above code style in this book.

## 6.8 APPLICATION TO STOCHASTIC DIFFERENTIAL EQUATIONS

Object-oriented developers are familiar with subtype polymorphism and creating class hierarchies in applications. In general, we can create a base class consisting of pure or default virtual functions which are then overridden or can be overridden by derived classes. For example, this was the approach taken in Duffy and Kienitz (2009) to model classes for SDEs. In particular, we model drift and diffusion as functions that can be customised in derived classes.

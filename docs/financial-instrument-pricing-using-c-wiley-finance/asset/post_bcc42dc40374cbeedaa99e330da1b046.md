
## Call Delta as a function of S

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_499_0.png)

**FIGURE 15.4 Call delta**

lambda function of arity two while the other parameters are captured variables. In general, we can create families of functions in this way by letting certain parameters play the role of input arguments while letting the other parameters play the role of captured variables. It can be seen as a kind of design pattern. In the case of two input arguments we speak of a surface.

We take an example of computing the delta of a call option. The asset price and days to maturity play the roles of the horizontal and vertical axes, respectively. We create a matrix of values (using one of the matrix classes that we introduced in Chapter 10), as the following code shows:

```
void DisplayCallDeltaSurface()
{ // Haug 2007 page 26

    // Delta as a function of S and T
    // A. Set up option's captured variables
    double K = 100.0;
    //  double T = 0.4;
    double r = 0.07;
    double b = 0.04;
    double sig = 0.3;

    // B. Define function for delta. lambda function for convenience
    auto callDelta = [&] (double S, double T)
    {
        double tmp = sig * std::sqrt(T);
        double d1 = (std::log(S / K) + (b + (sig*sig)*0.5) * T) / tmp;

        return std::exp((b - r)*T) * N(d1);
    };

    // C. Create meshes in the S and T directions
    std::size_t N = 20;
    std::vector<double> S = CreateMesh(N, 25, 150);
    for (auto el : S)
    {
        std::cout << el << '\n';
    }

    std::size_t M = 20;
    std::vector<double> TExpire = CreateMesh(M, 0.01, 0.5);

    // D. Compute the matrix of deltas
    NestedMatrix<double> C(N + 1, M + 1);
    for (std::size_t i = 0; i < C.size1(); ++i)
    {
        for (std::size_t j = 0; j < C.size2(); ++j)
        {
            C(i, j) = callDelta(S[i], TExpire[j]);
        }
    }

    // E. Display in Excel
    ExcelDriver xl; xl.MakeVisible(true);
    std::string sheetName("Call delta surface");
    long row = 1; long col = 1;
    xl.AddMatrix<NestedMatrix<double>>(C, sheetName, row, col);
}
```

The output is shown in Figure 15.6.

## Call Gamma as a function of S

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_500_0.png)

**FIGURE 15.5 Call gamma**

## 15.5 AUTOMATING DATA GENERATION

This book is concerned with numerical methods for applications in computational finance. Once a method has been programmed we need to write programs, organise test cases and test suites as well as control their run-time execution. In general, developers can use libraries such as Boost.Test or Google Test. A treatment of these libraries is outside the scope of this book. However, we discuss a number of related topics to automate the testing process and to generate data that can be used as input to numerical processes. In particular, we are interested in datasets that are in fact collections of polymorphic tuples or samples. The arity of a dataset is the arity of the samples that it contains. Monomorphic datasets are simpler because all samples in such datasets have the same type and the same arity. Our main focus here is on automatically generating both polymorphic data (parameters in the main) and monomorphic data in the forms of collections containing deterministic or randomly generated data. Some general use cases are:

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_501_0.png)

**FIGURE 15.6 Spot delta call**

- *Generating functions*: choosing a function that will generate deterministic or random numbers to be used as input arguments to algorithms that we wish to test.
- *Scalability*: extending a test that works with a finite set of data to one that works with larger and possibly infinite datasets.
- *Composition*: testing a function `func3` that takes type `T3` as argument and that calls functions `func1` and `func2` having types `T1` and `T2` as arguments, respectively.

We now discuss how to generate input data to algorithms using STL and `<random>` libraries in combination with user-defined code.

### 15.5.1 Data Generation Using Random Number Generators: Basics

In addition to providing input data to algorithms using the console we can generate the data that must lie in a given interval using a random number generator. The generated random numbers follow a particular distribution. This way of generating numbers is in many ways preferable to eliciting user input from the console.

The first use case is to generate random numbers in a given interval `(a, b)` based on the uniform distribution using the following free function:

```
template <typename T> T generateRN(T a, T b)
{ // Generate a uniform random number in interval [a,b]

    std::default_random_engine eng;
    std::random_device rd;
    eng.seed(rd());

    std::uniform_real_distribution<T> uniformVar(a, b);

    return uniformVar(eng);
}
```

This function is easy to use but it makes use of a hard-coded random number engine and the uniform distribution. We get a different random number each time we call this function because we seed the engine for each invocation. An example of use is:

```
double A = 0; double B = 1.0;
std::cout << generateRN(A, B) << '\n';
```

This function allows you to generate uniform random numbers in an interval without too much hassle. For more general cases we create a special generic class that supports the various distributions in the C++ `<random>` library, including the ability to create STL collections of variates from these distributions.

### 15.5.2 A Generic Class to Generate Random Numbers

The C++ `<random>` library supports approximately 20 statistical univariate distributions. Each distribution is a function object and it allows us to generate random numbers that are distributed according to the associated probability function. The function call operator needs an input argument representing a generator. We take an initial example of generating extreme value (Gumbel Type I) distribution variates using a linear congruential engine:

```
// aka minstd_rand0 typedef
std::linear_congruential_engine
    <std::uint_fast32_t, 16807, 0, 2147483647> eng;

// Reinit internal state of random-number engine using new seed value.
std::random_device rd;
eng.seed(rd());

// Create a distribution
double scale = 0.23; double location = 0.5;
std::extreme_value_distribution<double> evd(scale, location);

std::cout << "Extreme value variate: " << evd(eng) << '\n';
```

Looking at this code we see that it is useful but not yet generic. We generalise the code to support the following requirements:

- Distributions with a variable number of input arguments (we use variadic arguments).
- Some distributions use initialiser lists in their constructors.
- It must be possible to create collections of random variates, for example vectors, lists and other STL sequence containers (to realise this requirement we use the template–template parameter method).
- Write as little code as possible and reuse as many of the STL algorithms as possible. In this case we use std::generate() in combination with the random number generator to create a collection of random numbers.
- The associated engine (stateful source of randomness) is hard-coded. It can be generalised by elevating it to the status of a template parameter. This exercise is outside the current scope. The current engine class is std::default_random_engine.

The class that implements the above requirements is:

```
template < typename T, template <typename T> class Dist,
    template <typename T, typename Alloc> class Container =
    std::vector,
    typename Alloc = std::allocator<T> >

class RNGerator
{ // Generate random numbers of a given distribution based on
  // ctor parameters
private:
    Dist<T> dist;
    std::default_random_engine eng; // Others possible, e.g. mt19937
public:
    RNGerator() = default;

template <typename... Args> RNGerator(Args... args)
  : dist (Dist<T>(args...)), eng(std::default_random_engine())
{
    // Hard-coded
    std::random_device rd;
    eng.seed(rd());
}

template<typename T2> RNGerator(const std::initializer_list<T2>&
                              initList)
  : dist(initList), eng(std::default_random_engine())
{
    // Hard-coded
    std::random_device rd;
    eng.seed(rd());
}

T operator() ()
{ // STL-compatible function

    return dist(eng);
}

// Template member function using template template parameter trick
Container<T,Alloc> RandomArray(std::size_t n)
{
    Container<T,Alloc> result(n);

    // STL algorithm to assign values generated by a call to this->()
    std::generate(std::begin(result), std::end(result), *this);

    return result;
}

Container<T, Alloc> RandomArrayII(std::size_t n)
{ // Second approach

    Container<T, Alloc> result(n);

    // STL algorithm to assign values generated by a call to this->()
    for (std::size_t i = 0; i < result.size(); ++i)
    {
        result[i] = (*this)();
    }
    return result;
}

void Randomise(std::size_t count, Container<T, Alloc>& con)
{ // Assign random values to the first count elements of
  // container 'con'
```

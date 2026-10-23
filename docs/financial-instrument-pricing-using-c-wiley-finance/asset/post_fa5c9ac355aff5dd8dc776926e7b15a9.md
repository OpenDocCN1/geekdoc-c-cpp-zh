
numeric value from a customisable data source and applies a function to it that transforms it to another value:

```
using FunctionType = std::function<double (double x)>;

class DataFlow
{
private:
    double data;
    FunctionType _fun;

public:
    DataFlow(const FunctionType& fun) : data(0), _fun(fun) {}

    // Derived classes must override Input()
    virtual double Input() = 0;
    double Compute(double d) { return _fun(d); }

    // Template member function, cannot be overridden
    virtual double Algorithm() final
    { // This algorithm has a fixed structure

        // The steps in the algorithm
        double val = Input();
        return Compute(val);
    }
};
```

We now create a derived class that accepts its input from the console:

```
class ConsoleDataFlow : public DataFlow
{
public:
    ConsoleDataFlow(const FunctionType& fun) : DataFlow(fun) {}

    double Input() override
    {
        std::cout << "Give input value: ";
        double val; std::cin >> val;
        return val;
    }
};
```

An example of use is:

```
// Design pattern
auto fun = [](double d)->double {return std::exp(d);};
auto fun2 = [](double d)->double {return d*d;};

ConsoleDataFlow cdf(fun);
std::cout << cdf.Algorithm() << std::endl;
```

```
ConsoleDataFlow cdf2(func2);
std::cout << cdf2.Algorithm() << std::endl;
```

Summarising, the member function `Algorithm()` cannot be overridden but its variant parts (for example, `Input()` and `Compute()`) can be overridden. Finally, we note that the above design combines subtype polymorphism with uniform function wrappers. In this sense the solution represents a mixture of object-oriented and functional programming styles.

## 7.3.5 Uniform Initialisation

In previous versions of C++ there was some confusion concerning how to initialise variables and objects. It was not always clear when to use braces, parentheses or assignment operators. In C++11 we can avail of a single common syntax called *uniform (braced) initialisation* by placing the values between braces. Some simple examples are:

```
// Initializer list (they are recursive)
print<int>({ 3, 4, 5, 6, 99 });

// Uniform initialisation
double arr[] {1.0, 2.0, 3.0};
std::list<int> arr2{ 1, 3, 5, 7 };

std::tuple<double, double> tup(1.0, 2.0);
std::map<int, std::tuple<double, double>> database
                         { { 1, tup }, { 2, tup } };

for (auto it=std::begin(database); it != std::end(database); ++it)
{
    std::cout << it->first << ": "
              << std::get<0>(it->second) << ", " << std::get<1>
              (it->second) << std::endl;
}
```

We can use this technique to initialise the members of an aggregate object. Consider the classes:

```
// Struct that holds data together
struct Person
{

    std::string name_;
    std::string address_;
    int age_;

};

struct Person2
{
    std::string name_;
    std::string address_;
    int age_;

    Person2(int age, const std::string name, const std::string address)
        : age_(age), name_(name), address_(address) {}
};
```

We use uniform initialisation as follows:

```
// Aggregate initialisation; initialise the data in a
// struct without needing a constructor
Person p1{ "Joe", "Denver", 23 };

// ERROR! Person p1_a( "Joe", "Denver", 23 );
// (No function talking three arguments!!)

// Using constructors to initialise data
Person2 p2{ 55, "Piet", "Zurich" };
Person2 p3( 55, "Piet", "Zurich" );
```

We see from class Person that we can initialise a class’s member data using braced initialisation even though the class does not have the appropriate constructors.

## 7.3.6 Initialiser Lists

An object of type std::initializer_list<T> is a lightweight proxy object that provides access to an array of objects of type const T:

```
// Initialiser lists
template <typename T>
class ILClass
{ // Class using initialiser lists
private:
    std::vector<T> v;
public:
    ILClass(std::initializer_list<T> myList) : v(myList) {}

    void append(std::initializer_list<T> myList)
    { // Extend vector v before element at specified position

        v.insert(std::end(v), std::begin(myList),
            std::end(myList));
    }

    void print() const
    {
std::cout << '\n';
for (auto elem : v) { std::cout << elem << ","; }
std::cout << '\n';
}
};
```

An example of use and corresponding output is:

```
// Initializer lists
ILClass<int> c = { 1,2,3 };
c.print();                         // 1,2,3
c.append({ 4,5,6 });
c.print();                         // 1,2,3,4,5,6
```

## 7.3.7 Keyword noexcept

This keyword specifies that a function cannot throw or is not prepared to throw an exception. If a function does throw an exception then the program will terminate by calling std::terminate() which by default calls std::abort().

In general, the C++03 exception handling mechanism had a number of issues (that we do not discuss here) with the end result that many programmers just avoided using it. In C++11, however, the situation is much more clear-cut: a function throws an exception or it does not throw an exception. The keyword noexcept is part of a function and callers may depend on it.

We say that a function is exception-neutral if it does not throw an exception itself but functions that it calls might emit an exception. If an exception is emitted then the exception-neutral function allows the emitted exception to pass through the calling chain until a handler has been found. Such functions are never noexcept.

## 7.4 SHADES OF POLYMORPHISM

Polymorphism is defined as the ability to take several forms. In object-oriented technology we achieve polymorphic behaviour by being able to attach behaviour to different objects at run-time and calling their member functions. In short, we support polymorphism by declaring pure or default virtual member functions in a base class and then implementing these functions in derived classes. We also call this subtype (or dynamic) polymorphism.

We discuss four different ways to achieve polymorphic behaviour in classes and class hierarchies. We take the popular example of modelling payoff functions. We restrict the scope to one-factor payoffs and we consider just two cases, namely call and bull spread payoff. The goal is that clients should not have to know directly about specific payoffs or their defining data. This is a form of information hiding. This makes client code more extendible and reusable.

We propose the following solutions:

- S1: Traditional C++ hierarchy using subtype polymorphism.
- S2: Using the Strategy design pattern (GOF, 1995) with shared pointers. This is dynamic polymorphism.

```
class BullSpreadPayoff : public Payoff
{
private:
    double K1;
    double K2;
public:
    BullSpreadPayoff(double strike1, double strike2)
    { K1 = strike1; K2 = strike2;}

    double operator () (double S) const
    {
        if (S >= K2)
            return K2 - K1;
        if (S <= K1)
            return 0.0;

        // In the interval [K1, K2]
        return S - K1;
    }
};
```

A test case is:

```
template <typename T>
using SP = std::shared_ptr<T>;

double K = 20.0;
SP<Payoff> call (new CallPayoff (K));

std::cout << "Give a stock price (plain Call): ";
double S;
std::cin >> S;

std::cout << "Call Payoff is: " << (*call)(S) << '\n';

double K1 = 30.0;        // Strike price of bought call
double K2 = 35.0;        // Strike price of sell call

SP<Payoff> bs (new BullSpreadPayoff(K1, K2));    // Hull example

std::cout << "Give a stock price (BullSpread): ";
std::cin >> S;

std::cout << "Bull Spread Payoff is: " << (*bs)(S) << std::endl;
```

This is a popular approach and no doubt many legacy C++ applications (possibly in combination with raw pointers) use it to achieve polymorphism. The main disadvantages of this approach are:

The algorithms now form their own independent class hierarchy:

```
class PayoffStrategy
{
public:
    virtual double payoff(double S) const = 0;
};
```

```
class CallStrategy : public PayoffStrategy
{
private:
    double K;
public:
    CallStrategy(double strike) { K = strike;}
    double payoff(double S) const
    {
        return std::max<double>(S - K, 0);
    }
};
```

An example of use is:

```
double K = 20.0;
SP<PayoffStrategy> call (new CallStrategy (K));
Payoff pay1(call);

std::cout << "Give a stock price (plain Call): ";
double S;
std::cin >> S;

std::cout << "Call Payoff is: " << pay1.payoff(S) << '\n';
```

We now apply CRTP to create a compile-time version of solution S2. In this new solution S3 we create template classes as shown in Figure 7.2:

```
template <typename PayoffType>
    class Payoff
{
private:
    // PayoffStrategy* ps; // OLD
    SP<PayoffStrategy<PayoffType>> ps;

public:
    // Constructors and destructor
    explicit Payoff(const SP<PayoffStrategy<PayoffType>>& p);
    Payoff(const Payoff& source) = delete;
    virtual ~Payoff() {}
```

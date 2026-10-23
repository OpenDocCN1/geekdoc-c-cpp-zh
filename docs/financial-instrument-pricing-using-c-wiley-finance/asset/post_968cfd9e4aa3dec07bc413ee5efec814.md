
// Function call operator; Template Method pattern
double operator () ()
{
    return rng();
}

Some implementations are:

```
#include <random>
#include <cstdlib> // rand()
#include <memory>
#include <vector>
#include <algorithm>
#include <iostream>
#include <ctime>
#include <boost/random.hpp>
```

```
class InfamousRng : public Rng
{
public:
    InfamousRng()
    {
        srand(std::time(0));
    }

    double rng() override
    {
        return rand();
    }
};
```

```
class MTRng : public Rng
{ // Mersenne Twister
private:
    std::mt19937 eng;
    std::uniform_real_distribution<double> d;

public:
    MTRng() : eng(std::mt19937(std::time(0))),
              d(std::uniform_real_distribution<double>(0.0, RAND_MAX))
    {}

    double rng() override
    {
        return d(eng);
    }
};
```

- 2. Strategies provide different implementations for the *same* behaviour. We can thus use the strategy that best suits our efficiency and accuracy requirements. In this sense we call *Strategy* a *service-variation* pattern.

- 3. Clients must be aware of strategies. This introduces coupling because the client needs to know the name of the base class but not the name of the derived classes (in the above case the base class is called `Rng`). Each new algorithm must be implemented as a derived class of `Rng` which precludes functionality from other sources (unless we use adapters). This can be a disadvantage as it can lead to our having to use (multiple) inheritance which will lead to major maintenance problems.

- 4. Strategies increase the number of objects in an application. In many cases these objects must be created on the heap and then the application needs to define an object lifetime policy for them. This is an added complication and will add to development time.

- 5. Performance; the above code uses virtual member functions to vary behaviour which can have a performance impact in an application.

We now take the above code and adapt it to produce a solution based on the principles of PBD. In a sense it is a variation of the OOP approach. In general it is a compile-time trick (based on *parametric polymorphism*) while the above solution is based on *subtype polymorphism*.

The central idiom in PBD is to create a class template (called the *host class*) that in the most general case takes one or more type parameters as arguments. These types are specialised by *policy classes* and each one implements a particular implicit interface called a *policy*.

We have now defined enough terms to design the above problem using PBD. First, the host class is:

```
template <typename RngPolicy>
    class RandomGenerator : public RngPolicy
{ // Policy-based design random number generator.
// This is a host class.

public:
    // Function call operator, Template Method pattern
    double operator () ()
    {
        return rng();
    }

    std::vector<double> randomArray(unsigned N)
    {
        std::vector<double> result(N);
        for (std::size_t i = 0; i < result.size(); ++i)
        {
            result[i] = rng();
        }

        return result;
    }
};
```

In this case we see that the host class includes no hard-coded class names, just a template parameter that implements an *implicit interface*, in this case the implementation of the *function call operator* (this entails that the class becomes a function object). Any class that implements this operator can be used as a policy. We do not force clients to inherit from some base class. This adds to the reusability and customisability of the host class. In fact, a library can be created consisting of the host class and a set of already *predefined implementations* for each policy. For example, we can define a policy that implements the `knuth_b` engine adaptor which returns shuffled sequences generated with the pseudo-random number generator engine `minstd_rand0`:

```
```cpp
class KnuthRng
{
  // knuth_b algorithm as a policy class
private:
  std::knuth_b eng;
  std::uniform_real_distribution<double> d;

public:
  KnuthRng() : eng(std::knuth_b(std::time(0))),
               d(std::uniform_real_distribution<double>(0.0, RAND_MAX))
  {
  }

  double rng()
  {
    return d(eng);
  }

  // Function call operator,Template Method pattern
  double operator () ()
  {
    return rng();
  }
};
```
```

An example of using PBD in the current context is:

```
```cpp
// Policy-based classes
RandomGenerator<KnuthRng> policyRng;

auto rnArr4 = policyRng.randomArray(100);

// Use OOP classes with policy RNG
RandomGenerator<LfRng> policyRng2;

auto rnArr5 = policyRng2.randomArray(100);
```
```

We note that in this it is *not* possible to change a policy of the host class at run-time, in contrast to the design based on the GOF *Strategy*. Incidentally, the code example in Section 9.3.3

was an example of PDB with three policy classes for input, processing and output. We recall that the host class in this case is defined as:

```
template <typename I, typename O, typename Processing>
  class SUD : private I, private O, private Processing
```

## 9.5.1 Advantages and Limitations of PBD

The term policy-based design idiom is discussed in Alexandrescu (2001) where it is defined and a number of examples are given to show how to use it. In a sense it has reached almost mythical status in the C++ community. The summary of PBD from Wikipedia reads:

> A key feature of the policy idiom is that, usually (though it is not strictly necessary), the host class will derive from each of its policy classes using (public) multiple inheritance. (Alternatives are for the host class to merely contain a member variable of each policy class type, or else to inherit the policy classes privately; however inheriting the policy classes publicly has the major advantage that a policy class can add new methods, inherited by the instantiated host class and accessible to its users, which the host class itself need not even know about.) A notable feature of this aspect of the policy idiom is that, relative to object-oriented programming, policies invert the relationship between base class and derived class – whereas in OOP interfaces are traditionally represented by (abstract) base classes and implementations of interfaces by derived classes. In policy-based design the derived (host) class represents the interfaces and the policy classes implement them. It should also be noted that in the case of policies, the public inheritance does not represent ISA relationship between the host and the policy classes. While this would traditionally be considered evidence of a design defect in OOP contexts, this does not apply in the context of the policy idiom.

We can check this description against examples. We take a critical look at PBD from both a language and a design process point of view.

- The policy interface has a direct, explicit representation in C++ code. This interface is defined implicitly (via duck typing); hence it is documented separately and manually using comments. Duck typing is a layer of the programming language on top of typing and it is concerned with establishing the suitability of an object for some purpose. This suitability is determined by the presence of certain methods and properties (with the appropriate semantic meaning). In other words, a programmer is only concerned with ensuring that objects behave as demanded of them in a given context rather than ensuring that they are of a specific class. This is a crucial observation. It implies a form of polymorphism without the need to create class hierarchies. We note that duck typing can be defined for both run-time and compile-time scenarios but a discussion is outside the scope of this book.

- Templates apply duck typing in a static typing context.

- Policy-based design may not be the best approach for all applications. It seems to be closely identified with C++ and with C++ templates in particular. Other languages, for

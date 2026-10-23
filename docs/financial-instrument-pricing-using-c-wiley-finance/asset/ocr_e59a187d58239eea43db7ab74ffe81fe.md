# 32.2.1 Some Random Number Generators

Until recently, there were few standardised (standard) C and C++ libraries for random number generation and statistical distributions. But as discussed in Chapter 26, we see that C++ has support for 16 random number engines and 30 distributions. Furthermore, the Boost Random library has support for 30 random number engines and 28 distributions. It subsumes the functionality in C++ <random> and it contains a number of useful functions not found in C++ at the moment of writing.

In Chapter 31 we defined several random number generators as C++ classes that we can use in the software framework. We now define two more classes based on the 64-bit versions of the Mersenne Twister and Boost lagged Fibonacci algorithms, respectively. The code is based on the CRTP pattern:

```
class MTRng64 : public Rng<MTRng64>
{ // C++11 versions

private:
    // Normal (0,1) rng
    std::mt19937_64 dre;
    std::normal_distribution<double> nor;
public:
    MTRng64() : dre(std::mt19937_64()),
        nor(std::normal_distribution<double>(0.0, 1.0)) {}

    double GenerateRn()
    {
        return nor(dre);
    }
};
```

and

```
using FibGenerator = boost::variate_generator
    <boost::lagged_fibonacci607, boost::normal_distribution<double>>;

class FibonacciRng : public Rng<FibonacciRng>
{ // C++11 versions

private:
    // Normal (0,1) rng
    boost::lagged_fibonacci607 dre;
    boost::normal_distribution<double> nor;

    FibGenerator gen;

public:
    FibonacciRng() : dre(boost::lagged_fibonacci607()),
        nor(boost::normal_distribution<double>(0.0, 1.0)),
        gen (FibGenerator(dre, nor)){}
```
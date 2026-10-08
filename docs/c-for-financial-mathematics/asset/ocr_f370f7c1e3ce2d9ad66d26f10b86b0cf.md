has a function with signature

```
double getPayoff(double stockPrice)
```

Here we have replaced our plain English description of a path-independent option with a list of functions we expect to be available on any **PathIndependentOption** object. Note that in the implementation of **MonteCarlo-Pricer::price** given above these are the only two functions of the option that we actually use.

This description is called the *interface* of a path-independent option. It describes how we can *use* a path-independent option in our code, but it doesn't describe at all how to *implement* a path-independent option. In fact it doesn't make sense to talk about how to implement any of these functions because there is no one correct implementation. The implementation for a call option and a digital put should be completely different. However, they should both have functions **getMaturity** and **getPayoff**.

You can think of the interface as a *contract* or *specification* that a path-independent option must fulfil. If the class is written in accordance with this specification, we can price it by Monte Carlo.

# 10.2 Describing an interface in C++

How do we tell C++ that a **PathIndependentOption** is something with a payoff and a **getMaturity** function? It's easiest to see with an example. The C++ definition of a **PathIndependentOption** is given below:

```
class PathIndependentOption {
public:
/* A virtual destructor */
virtual ~PathIndependentOption() {}
/* Returns the payoff at maturity */
virtual double payoff(double finalStockPrice) const = 0;
/* Returns the maturity of the option */
virtual double getMaturity() const = 0;
};
```

The syntax is certainly strange. Your eye is probably drawn to the keyword *virtual* and the use of = 0. However, what you should focus on is the similarities with more familiar class definitions.

The class is called **PathIndependentOption**. There is a function called **payoff** and a function called **getMaturity**. They each take and return the

This technique of increasing encapsulation by using a factory method, `newInstance`, to provide implementations is called the factory design pattern. It has numerous advantages stemming from the fact that it allows one to clearly separate the interface from the implementation. One says that this decouples the interface and the implementation. Dependencies between different classes in your program is called coupling. Reducing coupling results in more maintainable code.

## 13.2.1 Implementation of PortfolioImpl

All the hard work has been in the design of the classes `Portfolio` and `PortfolioImpl`. Providing the implementation of the methods is very easy.

First, we must implement the factory method `newInstance`. This simply needs to return a new `PortfolioImpl` instance.

```cpp
shared_ptr<Portfolio> Portfolio::newInstance() {
    shared_ptr<Portfolio> ret =
        make_shared<PortfolioImpl>();
    return ret;
}
```

The implementation of `add` is easy:

```cpp
int PortfolioImpl::add(double quantity,
    shared_ptr<Priceable> security) {
    quantities.push_back(quantity);
    securities.push_back(security);
    return quantities.size();
}
```

as is implementing the implementation of `size`:

```cpp
int PortfolioImpl::size() const {
    return quantities.size();
}
```

and the implementation of `setQuantity`:

```cpp
void PortfolioImpl::setQuantity(int index,
    double quantity) {
    quantities[index] = quantity;
}
```

The end result of all our efforts is that we can write a function `price` for a `Portfolio` with ease:

```cpp
double PortfolioImpl::price(
    const BlackScholesModel& model) const {
    double ret = 0;
    int n = size();
    for (int i = 0; i < n; i++) {
        ret += quantities[i]
            * securities[i]->price(model);
    }
    return ret;
}
```

All of this implementation code is very simple. However, pause for a moment to consider the fact that our `Portfolio` implementation can now store any kind of stock derivative and price it. It will always choose the most efficient method of pricing depending upon the type of derivative it contains. Call options will be priced using the Black-Scholes formula for call options. Put options will be priced using the put option formula. Other options will be priced by Monte Carlo. Similarly, holdings in stock and zero-coupon bonds will be priced by calling the appropriate pricing function. The end result is an extremely versatile and useful class.

What is more, our `Portfolio` will work equally well with securities we haven't even implemented yet! The user of our library can provide their own implementations of our classes if they decide to sell novel financial products. Being able to cope with rapidly changing business requirements without having to rewrite all your software is an essential feature of commercial software. It is this “pluggability” that makes object-oriented software so important in the financial industry.

## 13.3 Testing

As we have tried to emphasise in this book, a crucial part of software development is testing that your code works.

In this test, we check the put-call parity formula which we will now derive. A portfolio, $\mathbf{P}$, consisting of 1 unit of a call option and $-1$ units of a put option both with strike $K$ will pay off an amount equal to

$$\max\{S_T - K, 0\} - \max\{K - S_T, 0\}$$

at maturity (where $S_T$ is the stock price at maturity). By considering separately the cases where $S_T < K$ and $S_T \geq K$, one can see that this expression simplifies to:

$$S_T - K.$$

So the value of the $\mathbf{P}$ is equal to the discounted expectation of $S_T - K$. In the $\mathbb{Q}$-measure, the discounted expectation of $S_T$ must be $S_0$. We deduce that the discounted expectation of $S_T - K$ is:

$$ S_0 - e^{-rT} K. $$

This is the value of $\mathcal{P}$ at time 0.

The test below confirms that this holds for our `Portfolio` class when $r=0$.

```cpp
static void testPutCallParity() {
    shared_ptr<Portfolio> portfolio
        = Portfolio::newInstance();

    shared_ptr<CallOption> c
        = make_shared<CallOption>();
    c->setStrike(110);
    c->setMaturity(1.0);

    shared_ptr<PutOption> p = make_shared<PutOption>();
    p->setStrike(110);
    p->setMaturity(1.0);

    portfolio->add(100, c);
    portfolio->add(-100, p);

    BlackScholesModel bsm;
    bsm.volatility = 0.1;
    bsm.stockPrice = 100;
    bsm.riskFreeRate = 0;

    double expected = bsm.stockPrice - c->getStrike();
    double portfolioPrice = portfolio->price(bsm);

    ASSERT_APPROX_EQUAL(100 * expected,
        portfolioPrice, 0.0001);
}
```

One might feel that we should write many more tests for our `Portfolio` class to test that it correctly prices more sophisticated portfolios. A central benefit of our design is that writing a large number of tests for the **Portfolio** class is not really necessary. We already have a suite of tests to confirm that various different types of option are priced correctly. The **Portfolio** class has a very simple *price* method and every line of that method is already tested by our test of put-call parity. Testing that **Portfolio** works with a portfolio of complex options would add nothing new.

## 13.4 UML

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_252_0.png)

**FIGURE 13.1:** Design of the Portfolio class.

Figure 13.1 summarises the classes we have introduced in this chapter as a UML diagram.

The diagram indicates that **PortfolioImpl** implements the interface **Portfolio** which in turn extends the interface *Priceable*. *Priceable* is also implemented by the class *CallOption*.

On the other hand, a **PortfolioImpl** contains a vector of *Priceable* objects; this is indicated by the arrow labelled *securities*. This relationship is a *has a* relationship. A **PortfolioImpl** has a number of associated securities. All of these relationships are *is a* relationships and are implemented using class extension.

The `*` symbol on the arrow indicates that a **PortfolioImpl** can have any number of associated securities. In UML you can label the *multiplicity* of any relationship with a number or range of numbers. For example, the relationship “parents” between a human and their parents could be labelled with the multiplicity 2. `*` simply means there is no limit on the multiplicity.

The `newInstance` function is underlined to indicate that it is a static function.

We have deliberately omitted the full hierarchy of options from our diagram to keep it readable. We have also indicated that a `CallOption` has public member variables *strike* and *maturity* even though these variables can only be accessed through get and set methods. We have not mentioned that the **PortfolioImpl** stores references to *Priceable* objects using a vector of shared pointers. Thus our diagram is a slight simplification of our classes. It is intended to illuminate the design rather than to precisely mirror the code.

## 13.5 Limitations

We do not claim that the code in this chapter is the last word on pricing a portfolio of options. Here are some important limitations.

- (i) We are using a fixed number of scenarios and steps in Monte Carlo calculations, this should be configurable.
- (ii) We haven't made any attempt to optimise our code.
- (iii) We haven't taken advantage of the multiple CPUs available on modern computers.
- (iv) Our ContinuousTimeOption and Priceable interfaces are not sufficiently general. For example, they cannot cope with discrete time options and options on multiple underlying stocks.
- (v) When pricing a portfolio by Monte Carlo, it isn't a good idea to keep generating random numbers. It is better to generate all the risk factors in one go and then use the same scenarios to price each element. This both involves less random number generation and will ensure that hedges cancel each other accurately.

Many of these limitations will be addressed in later chapters.

## Exercises

1. 13.5.1. A zero-coupon bond is a financial instrument that is guaranteed to pay out a value of 1 at its maturity T. These instruments are not often traded in practice, but are a useful mathematical abstraction to represent a risk-free bank account. Putting money in a risk-free bank account up to time T is the equivalent of investing in zero-coupon bonds with maturity T. The theory of risk-neutral pricing tells us that the risk-neutral price of a zero-coupon bond at time 0 is $\exp(-rT)$.

Use this fact to create implementations of the Priceable interface for stocks and zero-coupon bonds.

```
```\n\t\t\tbool isPathDependent() const {\n\t\t\t\treturn false;\n\t\t\t};\n\t};\n```
```

The implementation of **PathIndependentOption** does the following.

+   * It provides an implementation of `isPathDependent`.
* It has an abstract function to compute the payoff given only the final stock price. By definition of “path independent” a path-independent option should be able to provide an implementation of this function.
* This means we can implement the `payoff` function that takes an entire path of stock prices. We only need to look at the last price.

Once we’ve written a **PathIndependentOption** class, we can use this to write a **CallOption** class that extends it.

```
```\nclass CallOption : public PathIndependentOption {\n\tpublic:\n\n\t\tdouble payoff( double stockAtMaturity ) const;\n\n\t\tdouble price( const BlackScholesModel& bsm )\n\t\t\t\tconst;\n};\n```
```

To implement a **CallOption** we will have to write a function to compute the payoff at maturity. So the `payoff` function above must be declared.

We have also chosen to provide an override for `price`. This is because we know that it would be better to use the Black–Scholes formula to price a Call Option than to use the default Monte Carlo implementation.

Notice that all the functions `getMaturity`, `getStrike`, etc., are implemented by the grandparent **ContinuousTimeOptionBase**.

Similarly, the **ContinuousTimeOption** method `payoff` is implemented by the parent **PathIndependentOption**, so we only have to implement a simpler method that computes the payoff using the price at maturity.

We could write **PutOption**, **DigitalCallOption**, and **DigitalPutOption** in a similar way with very little additional code. This is left as an exercise.

# 12.6.1 UML

Figure 12.1 shows a UML diagram for the class hierarchy of options in FMLlib12. Actually, the **DigitalPutOption** and **DigitalCallOption** don’t exist. You should write them yourself as an exercise.

The arrows in Figure 12.1 (with the specific shape of arrow head shown)
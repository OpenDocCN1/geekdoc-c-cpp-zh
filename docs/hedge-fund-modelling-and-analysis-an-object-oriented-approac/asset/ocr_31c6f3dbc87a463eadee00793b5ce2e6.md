# Market Risk Management

# 261

```
// Declare and call GetData()
V2DD data = ctai.GetData("./data/cta_index.dat");

// Declare and call ModifiedVaR() member function
DBL mvar = rmetrics.ModifiedVaR(data, 95);

// Output results
cout << "\n Modified VaR = $\$\ << fixed << setprecision(0) << mvar << << '\\n";
// ...
```

![](bbox=[0.137, 0.281, 0.862, 0.545])



The Monte-Carlo (MC) method assumes that a series of hedge fund returns can be characterised by a stochastic (or probabilistic) model. MC methods are widely used of classical algorithms for simulating the behaviour of various physical and mathematical systems having been popularised by John von Neumann and Nicholas Metropolis to name but two. MC methods are distinguished from other simulation-based methods by being of a stochastic nature, that the MC model includes a non-deterministic component that introduces a degree of uncertainty or randomness into the process through the use of random generators. The fundamental idea

> ⁶ John von Neumann (1903–1957) was a Hungarian-American mathematician who made major contributions...\⁷ Nicholas Metropolis (1915–1999) was a Greek American physicist.
⁸ MC simulations rely heavily on the sampling method and stability of the random number generator (RNG). For this reason, many financial houses spend a great deal of time, money and effort developing better and more robust RNGs.
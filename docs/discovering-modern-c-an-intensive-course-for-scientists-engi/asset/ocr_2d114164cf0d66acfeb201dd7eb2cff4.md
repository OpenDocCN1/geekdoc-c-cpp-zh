![](bbox=[0.215, 0.085, 0.815, 0.355])

Figure 4-8: Simulated share price over 20 years

The development of \( S^1 \) with the parameters \( \mu = 0.05, \sigma = 0.3, \Delta = 1.0, t = 20 \) as constants according to (4.2) can now be programmed in a few lines:

```
default_random_engine re(random_device(){});
normal_distribution<> normal;

const double mu= 0.05, sigma= 0.3, delta= 0.5, years= 20.01,
        a= sigma * sqrt(delta),
        b= delta * (mu - 0.5 * sigma * sigma) ;
vector<double>
        s= {345.25}; // Start with initial price

for (double t= 0.0; t < years; t+= delta)
        s.push_back( s.back() * exp(a * normal(re) + b) )
```

Figure 4-8 depicts five possible developments of the share price for the parameters from the previous code.

We hope that this introduction to random numbers will give you a smooth start to the exploration of this powerful library.

# ## 4.3 Meta-programming

In this section, we will give you a foretaste of meta-programming. Here, we will focus on the library support and in Chapter 5 we will provide more background.

# ### 4.3.1 Limits

A very useful library for generic programming is `<limits>` which provides important information on types. It can also prevent surprising behavior when the source is compiled on
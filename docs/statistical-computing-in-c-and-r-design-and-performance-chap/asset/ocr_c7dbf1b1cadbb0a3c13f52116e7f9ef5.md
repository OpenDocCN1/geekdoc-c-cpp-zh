# 502 C++ LIBRARY EXTENSIONS (TR1)

+   - An object dist from the normal_distribution class with mean mu and standard deviation (both parameters being type double) is created with

```
normal_distribution<> dist normal(mu, sigma)
```

The default is the standard normal distribution.

+   - The binomial_distribution class has parameters n and p with n of type int and p of type double. The syntax

```
binomial_distribution<> dist(n, p);
```

will create an instance of the class. The parameters n and p default to 1 and .5, respectively.

+   - The gamma_distribution class (e.g., Section 4.6) is parameterized with a single shape parameter alpha of type double that defaults to 1. An instance of the class is obtained via

```
gamma_distribution<> dist(alpha);
```

To produce values for a gamma distribution with mean alpha*beta, multiply values from this generator by beta.

+   - An instance of the poisson_distribution class with double precision mean lambda is produced with

```
poisson_distribution dist(lambda);
```

The following program illustrates the use of variate_generator in combination with several of the distributions mentioned above.

```
//trNG.cpp
#include <tr/random>
#include <iostream>

using namespace std;

int main() {
    variate_generator<mt19937
```

First, we need to include the header file tr/random which allows us to access the distributions and generators. Objects are created to produce random numbers from the uniform (on [0, 1]), normal (with two mean and standard deviation .5), binomial (with 3 trials and success
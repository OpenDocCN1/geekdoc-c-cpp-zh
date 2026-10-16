parameters. Such representations are easily generated and even more easily found on the Web. Sampling distributions map integers into a specific range according to their probability density function P:

# Sampling Distributions (§iso.26.5.8.6) (continues) Distribution Precondition Defaults Result

```
discrete_distribution<I>{b,e} 0<=b[i] none [0:e-b) P(i|p0… pn-1) = p_i
```

The sequence [b:e) provides weights w_i so p_i = w_i/S and 0 < S = w0 + … + wn?1 where n = e-b

# Sampling Distributions (continued) (§iso.26.5.8.6)

Distribution Precondition Defaults Result

```
discrete_distribution<I>(lst)
discrete_distribution<I>(lst.begin(),lst.end())
discrete_distribution<I>(n,min,max,f) discrete_distribution<I>(b,e)
piecewise_constant_distribution<R>{b,e ,b2,e2}
piecewise_linear_distribution<R>{b,e ,b2,e2}
```

where the ith element of [b:e) is obtained by f(min+i*(max?min)/n +(max-min)/(2*n)) b[i]<b[i+1] none [_* b:*(e-1)) P(x|x0,… xn, ρ0… ρn) b[i]<b[i+1] none [_* b:*(e-1)) P(x|x0,… xn, ρ0… ρn)

= p i b b_{i+1} - x + ρ x - b_i i+1 - bi bi+1 - bi b_i < b_{i+1} for all b_i in [b:e) 1 n-1 ρ = w_i/S where S = 2_i Σ(w_i + w_{i+1})(b_{i+i} - b_i) =0 [b:e] are the interval boundaries [b2:e2] are the weights

# 40.7.4 C-Style Random Numbers

In <cstdlib> and <stdlib.h>, the standard library provides a simple basis for the generation of random numbers:

```
#define RAND_MAX implementation_defined /* large positive integer */
int rand(); // pseudo-random number between 0 and RAND_MAX void srand(unsigned int i); // seed random number generator by i
```

Producing a good random number generator isn’t easy, and unfortunately not all systems deliver a good rand(). In particular, the low-order bits of a random number are often suspect, so rand()%n is not a good portable way of generating a random number between 0 and n-1. Often, int((double(rand()))/RAND_MAX)*n) gives acceptable results.

However, for serious applications, generators based on uniform_int_distribution (§40.7.3) will give more reliable results.
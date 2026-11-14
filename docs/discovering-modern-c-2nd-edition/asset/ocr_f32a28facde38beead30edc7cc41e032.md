+   -- minstd_rand0
+   -- mt19937
+   -- mt19937_64
+   -- ranlux24
+   -- ranlux24_base
+   -- ranlux48
+   -- ranlux48_base

The predefined engines in the last group are just type definitions, for instance:

Click here to view code image

```
using knuth_b= shuffle_order_engine <minstd_rand0 , 256>;
```

# 4.2.2.4 Distribution Overview

As mentioned before, the distribution classes map the unsigned integers to the parameterized distributions. Table 4–3 summarizes the distributions defined in C++11. Due to space limits, we used some abbreviated notations. The result type of a distribution can be specified as an argument of the class template where I represents an integer and R a real type. When different symbols are used in the constructor (e.g., m) and the describing formula (e.g., μ), we denoted the equivalence in the precondition (like m ≡ μ). For consistency’s sake, we used the same notation in the log-normal and the normal distribution (in contrast to other books, online references, and the standard).

# Table 4–3: Distributions Defined in C++11

| Distribution | Produced Values |
|---|---|
| Uniform distributions | |
| uniform_int_distribution | integer |
| uniform_real_distribution | real |
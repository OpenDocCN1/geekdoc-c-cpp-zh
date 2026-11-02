All generators are of type `gsl_rng`, a corresponding pointer variable is declared in line 6. The generator is actually allocated in line 11 using the function `gsl_rng_alloc()`, which expects an argument of type `gsl_rng_type *`. Many different generators are predefined in the GSL, see below. Here, the generator "gsl_rng_mt19937" is used, which is also the default generator. All random number generators can be initialized with a seed using the function `gsl_rng_set()`, which expects a generator and an `int` number as arguments. Here, the seed value 1000 is used (line 12). The actual generation of the numbers is performed in the loop in lines 14-18. The generation of numbers is performed always by means of auxiliary functions. They receive a pointer to the generator as argument, sometimes also parameters of the corresponding distribution, and return a random number. Here, we generate numbers which are uniformly distributed in the interval [0,1) via the function `gsl_rng_uniform()`, see line 16. Therefore, the value 0 is included, but the value 1 is excluded. Finally, the generator is destroyed (line 20).

The GSL offers several high-quality generators. Also other generators are included for back compatibility. In total more than 27 different generator algorithms are implemented. The best known are

+   - `gsl_rng_mt19937`
+     The MT19937 generator [Matsumoto and Nishimura (1998)]. It has a period of about $10^{6000}$ and passed the *Diehard* statistical tests [Marsaglia].
+   - `gsl_rng_gfsr4`
+     is a lagged-Fibonacci generator [Ziff (1998)]. In the present implementation, the generator has a period of about $10^{2917}$.
+   - `gsl_rng_ranlux`
+     The *ranlux* 24 bit generator [Lüscher (1994)]. It has a period of $10^{171}$.
+   - `gsl_rng_rand48`
+     is the Unix linear congruential random number generator `rand48()`. It is also included for compatibility and has lower quality compared to modern generators, e.g. a period of about $10^{14}$. But this is sufficient for small applications without the need for high-quality statistics.
+   - `gsl_rng_rand`
+     is the standard Unix (BSD) linear congruential random number generator `rand()`. It is included for compatibility (i.e. you can use it on non-Unix system) and has a very bad quality compared to modern generators, e.g. a period of about $10^9$.

## 7.3 GNU scientific library

The GNU Scientific library (GSL) [Galassi et al. (2006)] contains a huge number of subroutines that can be used to solve standard numerical problems. Amongst other things, the library features:

- complex numbers and functions
- polynomials
- evaluation, differentiation and integration of functions
- performing interpolations
- Fourier, wavelet and Hankel transforms
- minimizing functions
- diagonalization of matrices
- solving linear equations (through matrix inversion)
- random numbers
- statistics/histograms
- fitting data
- solving nonlinear equations
- solving ordinary and partial differential equations
- Monte Carlo simulation and simulated annealing

Some of the functionality comes through a C interface to the BLAS (basic linear algebra subroutines) package, which is originally implemented using Fortran. The library is under continuous development. Note that it comes under the GNU General Public License (GPL). This means the library is free, including the source code. You are allowed to extend and to modify the library. You can include it into other software, provided it is also free (GPL) if it is distributed as well.

We start to explain the usage via a simple example: We want to print a table of the probability mass function of the Binomial distribution, defined in Sec. 8.1.1. For this and related purposes, the GSL offers functions for different distributions. When using any of these, one has to include the header file gsl/gsl_randist.h. Similar header files exist for the other sections of the GSL. The function to calculate the probability mass function of the Binomial distribution has the following prototype:

```c
double gsl_ran_binomial_pdf(const unsigned int x, const double p,
    const unsigned int n);
```

The first argument contains the value, for which the probability is to be calculated. The second and third arguments contain the values of the parameters p and n (with 0 ≤ p ≤ 1 and x = 0,1,...,n). This and all other functions of the GSL are explained in the user guide, which can be downloaded from the web page or bought as printed copy [Galassi et al. (2006)]. Next, the small sample C program named binomial.c is shown, which reads in p and n from the command line and prints a table with all feasible values of p(x):

GET SOURCE CODE
DIR: libraries
FILE(S): binomial.c

```c
1 #include <stdio.h>
2 #include <gsl/gsl_randist.h>
3
4 int main(int argc, char *argv[])
5 {
6     int n;                         /* parameters of distribution */
7     double p;
8     int x;                         /* argument of pdf */
9     double prob;                   /* resulting probability and sum of all probs */
10    int argz = 1;                  /* for treating command line arguments */
11
12    sscanf(argv[argz++], "%lf", &p);
13    n = atol(argv[argz++]);        /* get arguments */
14
15    for(x=0; x<=n; x++)            /* iterate to print full distribution */
16    {
17        prob = gsl_ran_binomial_pdf(x, p, n);
18        printf("%d %f\n", x, prob);
19    }
20    return(0);
21 }
```

Line 2 contains the inclusion of the suitable GSL header file. Lines 6-10 contain the variable declarations. In lines 12 and 13, the command-line arguments are read in, see Sec. 1.3. Lines 15-19 contain the main loop, where the evaluation of the distribution is called (line 17) and the result is printed to the standard output (line 18). The program can be compiled using:

```
cc -o binomial binomial.c -lgsl -lgslcblas -lm
```

For linking, in addition to the GSL (-lgsl) also an auxiliary library (-lgslcblas) and the standard math library (-lm) have to be stated. Note

All generators are of type `gsl_rng`, a corresponding pointer variable is declared in line 6. The generator is actually allocated in line 11 using the function `gsl_rng_alloc()`, which expects an argument of type `gsl_rng_type *`. Many different generators are predefined in the GSL, see below. Here, the generator "gsl_rng_mt19937" is used, which is also the default generator. All random number generators can be initialized with a seed using the function `gsl_rng_set()`, which expects a generator and an `int` number as arguments. Here, the seed value 1000 is used (line 12). The actual generation of the numbers is performed in the loop in lines 14-18. The generation of numbers is performed always by means of auxiliary functions. They receive a pointer to the generator as argument, sometimes also parameters of the corresponding distribution, and return a random number. Here, we generate numbers which are uniformly distributed in the interval [0,1) via the function `gsl_rng_uniform()`, see line 16. Therefore, the value 0 is included, but the value 1 is excluded. Finally, the generator is destroyed (line 20).

The GSL offers several high-quality generators. Also other generators are included for back compatibility. In total more than 27 different generator algorithms are implemented. The best known are

- `gsl_rng_mt19937`
  The MT19937 generator [Matsumoto and Nishimura (1998)]. It has a period of about $10^{6000}$ and passed the *Diehard* statistical tests [Marsaglia].
- `gsl_rng_gfsr4`
  is a lagged-Fibonacci generator [Ziff (1998)]. In the present implementation, the generator has a period of about $10^{2917}$.
- `gsl_rng_ranlux`
  The *ranlux* 24 bit generator [Lüscher (1994)]. It has a period of $10^{171}$.
- `gsl_rng_rand48`
  is the Unix linear congruential random number generator `rand48()`. It is also included for compatibility and has lower quality compared to modern generators, e.g. a period of about $10^{14}$. But this is sufficient for small applications without the need for high-quality statistics.
- `gsl_rng_rand`
  is the standard Unix (BSD) linear congruential random number generator `rand()`. It is included for compatibility (i.e. you can use it on non-Unix system) and has a very bad quality compared to modern generators, e.g. a period of about $10^9$.

Note that it is not necessary to hard-code the type of the random number generator in the program. One can define an environment variable `GSL_RNG_TYPE` and call in the program the function `gsl_rng_env_setup()` (no arguments). Then the global variable `gsl_rng_default` of type `gsl_rng_type *` will contain the current generator and can be used as argument when calling `gsl_rng_alloc()`. If the environment variable is not assigned, `gsl_rng_default` will contain `gsl_rng_mt19937`.

In addition to the functions discussed so far, the GSL enables us to investigate the properties of random number generators, copy generators, store the state of generators in files, and read them back in.

Now, to actually generate data which is distributed according to a Binomial distribution $Bin(n,p)$, the following function is provided:

```c
unsigned int gsl_ran_binomial(const gsl_rng * r, double p,
                              unsigned int n);
```

The first argument is a pointer to a GSL random number generator as described above. One has to pass the parameters $p$ and $n$ as second and third arguments. Thus, to generate 10000 numbers which are distributed according to a Binomial (10,0.4) distribution, one has to replace line 16 in the above program by

```c
r = (double) gsl_ran_binomial (rng, 0.4, 10);
```

Apart from the Binomial distribution, the GSL implements many different distributions. Usually the probability density function (or the probability mass function for discrete variables) and a function for generating (pseudo) random numbers according to the distribution are available. Examples are the Gaussian distribution, the exponential distribution, the Levy distribution, the Chi-squared distribution, the Pareto distribution, the Weibull distribution, and the hyper-geometric distribution. See the GSL documentation for more details.

To record histograms of the generated random numbers and of any other data, the GSL offers histograms via the `gsl_histogram` data type. Included are functions for creating, updating, accessing, printing, analyzing and deleting histograms. Interestingly, the histograms can have bins of non-uniform size, which is useful for logarithmic binning. Again, see the GSL documentation for more details and exercise (2).

We close this section by showing how one can solve a system of linear equations using the GSL. For this example already a couple of different data

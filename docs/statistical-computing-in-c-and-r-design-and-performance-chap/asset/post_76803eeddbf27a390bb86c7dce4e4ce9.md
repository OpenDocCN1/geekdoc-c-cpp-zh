
# 186 PROGRAMMING IN R

number of elements that are selected = nk. Thus, an equivalent formula is

```math
$$\chi^2 = \frac{K-1}{K-k} \sum_{i=1}^K \frac{(Obs[i] - N/K)^2}{N/K} \quad (5.2)$$
```

In the case of data from the Guess game K = 40 and k = 5.

The R function chisq.test computes the chi-square statistic in (5.1). We have wrapped it the hyperChi function in Listing 5.6 to automatically produce the statistic in (5.2).

Listing 5.6 hyperChi.r

```r
#hyperChi.r
hyperChi <- function (O, K, k) {
  chisast <- (K - 1)*chisq.test(O/(K - k))
  names(chisast) <- NULL
  list(chisast) <-chisq(chisast, K - 1)
}
```

The chisq.test function takes the observed frequencies as its first argument and a vector p specifies the probabilities of occurrence for observations considering each row of this frequency vector. The p argument defaults to equally categories which suffices for our case. Our wrapper function has two arguments K and k that represent the size of the population and the number of draws without replacement, respectively. The chisq.test function returns a list whose first component is the value of the chi-square statistic. The list subset operator [] is used to isolate the test value which is inflated appropriately according to the values of K and k. The chisq.test function has left the result with the name "X-squared" attached that we would prefer not to appear in our output. The (replacement version of the) names function is used to suppress this behavior by setting the name to NULL. Finally, the output from the function is returned as a list whose first component is the chi-square statistic and the second is its associated upper-tail p-value.

An application of hyperChi to the Guess5 data produces

```
> hyperChi(Obs, 40, 5)
[[1]]
[1] 27.77691

[[2]]
[1] 0.910013
```

The p-value of .91 leads to the expected conclusion that the data does not exhibit a significant departure from uniform selection of the ball numbers.

# 5.7 Using C/C++ code in R

The R "foreign" interface allows computational routines to be coded in, e.g., C or C++, and imported into R as a shared library. In this section we will explore and illustrate how this can be done.

One situation where it is common to use a combination of R and C/C++ programs is in the creation of R packages. Descriptions of this process are given in the Writing R Extensions manual and, e.g., in Chapter 7 of Gentleman (2009). The development here is of a smaller scale. Our perspective is that of someone who has written a relatively small and focused set of C++ code designed for a specific task of their personal interest. In some cases this type of program development can benefit from a pairing with R. For example, one may have developed a new estimation method that has been coded in C++.

![](img/b50973a0535e1d41c799ab78355b19f6_202_0.png)

# USING C/C++ CODE IN R

Simulation experiments to assess the properties of the method could be managed in R and the data analysis tools that R provides could then be used directly for summary and analysis of the simulation results. There are also many R functions that become available through the R API These are the same as the ones discussed in Section 4.9 in our treatment of the R Standalone Math Library that includes, e.g., methods for random number generation. The code development process can be simplified in many instances by making use of this resource.

There are two interfaces between R and C/C++ .c and .Call Both of these functions pass pointers to R objects to C/C++ code The difference is that the former cannot use R internal data structures while the latter .c is less involved and likely to be the preferred option for our particular setting. Thus, we focus on .c here. An in-depth description of using .Call and more generally, programming with R data structures is contained in the R Internals and Chapters 5-6 of the Writing R Extensions manual Chapter 6 of Gentleman (2009) provides a new introduction to the topic.

Let us begin by importing both C and C++ implementations of simple “Hello world!” programs into R for this purpose might like

```c
//hello.c
#include "R.h"

void hello(int *n) {
	int i;
	for(i = 0; i < *n; i++) {
	printf("Hello %d times!\n", i);
	*n++;
}
}
```

After a while we will be able to call this program from inside an R session where it will print "Hello y!" as many times as desired.

The simple hello.c program has some distinguishing features relative to what was seen in Chapter 3. First there is no main function. The presence of either C or C++ programs will create problems in compiling the shared libraries that are needed for using such code in R. For creating a shared library that can be called from R, the function that serves the purpose of main in C/C++ code must

- 1. have as a return type and
- 2. have arguments are pointers.

Both of equalities are present in the hello.c listing. This program will print out the greeting number of times determined by the pointer to int that is the argument for the hello function. The phrase is printed to the R console using the printf function that is made available through the R header file. Finally, *n is augmented by one and the program terminates. The printf function is an analog of the R function that is used to produce formatted output in C language. The first argument to printf is a character string (enclosed in quotes) with % placeholders for the values of each argument. The % placeholder is augmented by a character that denotes the storage type for it:

- d for integer variable,
- e for floating-point variable,
- f for floating-point variable and
- s for printing a character string.

The initial argument to printf in our program is "Hello y'all %d times!". The d informs the compiler that the next argument is an integer variable and the format is tailored to a variable of that type. The \n at the end of character string produces a new line after printing the message. To compile the C code we enter on the shell line.

```
$ R CMD SH hello.c
```

This creates a shared library hello.so that can now be imported into R using dyn.load. Specifically, this is accomplished inside R with

```
> dyn.load("hello.so")
> is.loaded("hello")
```
[1] TRUE

The is.loaded function checks that the shared library has been successfully loaded. Note that R refers to by the name of the function that interfaces with R, or func in this case, rather than the library name. The linked program can now be executed using the .C function as produce, e.g.,

```
> .C("hello", as.integer(3))
Hello y'all 0 times!
Hello y'all 1 times!
Hello y'all 2 times!
```

The list information provided at the end of this output is what has been returned by the .C function. It represents the values of the arguments (i.e., the values stored in memory locations for the pointers that were passed in the function call) that were returned from the hello program. In particular the output shows that last line had the effect of advancing the value of n (from the initial value assigned in R) by one unit. Also, note that the use of as.integer for passing the integer 3 into the C program is necessary.

A similar program can be developed in C++ as we now demonstrate. First, we will be a class with a header file X.hh (the hh extension is necessary) that contains the code

```cpp
//X.hh
#ifndef X_HH
#define X_HH
class X {
int n;
public:
X(int N);
    X();
};
#endif
```

The class constructor and destructor are defined in X.cc (again, the cc extension is necessary) as

```cpp
//X.cc
#include <R.h>
#include <Rmath.h>
#include "X.hh"

X::X(int N) {
    n = N;
    for(int i = 0; i < n; i++)
        printf("Hello world %d times!\n", i);
        printf("Normal %f \n", rnorm(1.96, 0, 1, 0));
}

X::~X() {
    for(int i = 0; i < n; i++)
        printf("Goodbye %d times!\n", i);
}
```

A driver program shown below uses an object of the X class.

```cpp
//useX.cc
#include "X.hh"

extern "C" {
    void func(int*n) {
        X *(n);
    }
}
```

This last program represents the conduit between R and our C++ code. It will be compiled and linked with C libraries using the C compiler. To allow for this mixing of C and C++ code, it must be enclosed in an extern "C" { } "wrapper" that encapsulates the function between curly braces. Beyond that, the intent of our program is to call both the constructor and destructor for the X class and thereby have the corresponding greeting and farewell messages printed in R.

To compile the X class program use

```
$ R CMD LIB X.cc useX.so
```

to create the shared object file X.so. A specific name could have been given to the library other than X.so using the -o option. In absence of a specified name, the name of the first file (without extension) is used as the shared library. Thus, switching X.cc to useXcc on the command line would produce the shared library useX.so.

Now an R session is started and the library can be loaded with

```
> dyn.load("X.so")
> is.loaded("func")
```

[1] TRUE

The response from is.loaded indicates that the library has been loaded successfully. Note that R refers to by the name of the function that interfaces with R, or func in this case, rather than the library name. The linked program can now be executed using the .C function as produce, e.g.,

```
> .C("func", as.integer(3))
Hello world 0 times!
Hello world 1 times!
Hello world 2 times!
```

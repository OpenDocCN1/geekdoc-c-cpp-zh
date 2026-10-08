Now edit the file you have just created and type in the first line:

```
```c
#pragma once
```
```

Then enter the *declarations* for all the functions we want to make available from our library. In our example, the complete code required is:

```
```c
#pragma once

const double PI = 3.14159265358979;

/**
 *  Computes the cumulative
 *  distribution function of the
 *  normal distribution
 */
double normcdf( double x );

/**
 *  Computes the inverse of normcdf
 */
double norminv( double x );
```
```

This contains the declarations for all the functions we wish to make available. It contains both the declaration and the definition for PI.

In general, you should put the following in your header file:

+   * (i) The first line `#pragma once`. We'll explain why shortly.
* (ii) Declarations of functions you wish to make available from your library.
* (iii) Declarations of global variables you wish to make available.
* (iv) Definitions of constant global variables.

Whereas in your source file you should put:

+   * (i) Definitions of functions declared in the header.
* (ii) Definitions of global variables missing from the header.

We will expand on these rules throughout this book as we meet more types of declaration and definition.

The reason why constants are treated differently is that the C++ compiler can “inline” them. This means to replace every use of the constant with the actual value. This gives a slight performance boost. As a consequence, however, the definition needs to be in the header, so that every file knows the correct value to inline.
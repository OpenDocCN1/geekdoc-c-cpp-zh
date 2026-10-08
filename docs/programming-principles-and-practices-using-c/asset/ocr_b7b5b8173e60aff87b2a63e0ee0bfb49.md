![](bbox=[0.0, 0.08, 0.85, 0.32])

+   24.1 Introduction  
24.2 Size, precision, and overflow
24.2.1 Numeric limits  
24.3 Arrays  
24.4 C-style multidimensional arrays  
24.5 The Matrix library
24.5.1 Dimensions and access
24.5.2 1D Matrix
24.5.3 2D Matrix
24.5.4 Matrix I/O
24.5.5 3D Matrix

+   24.6 An example: solving linear equations
24.6.1 Classical Gaussian elimination
24.6.2 Pivoting
24.6.3 Testing
24.7 Random numbers
24.8 The standard mathematical functions
24.9 Complex numbers
24.10 References

# 24.1 Introduction

For some people, numerics – that is, serious numerical computations – are everything. Many scientists, engineers, and statisticians are in this category. For many people, numerics are sometimes essential. A computer scientist occasionally collaborating with a physicist would be in this category. For most people, a need for numerics – beyond simple arithmetic of integers and floating-point numbers – is rare. The purpose of this chapter is to address language-technical details needed to deal with simple numerical problems. We do not attempt to teach numerical analysis or the finer points of floating-point operations; such topics are far beyond the scope of this book and blend with domain-specific topics in the application areas. Here, we present

+   - Issues related to the built-in types having fixed size, such as precision and overflow
- Arrays, both the built-in notion of multidimensional arrays and a Matrix library that is better suited to numerical computation
- A most basic description of random numbers
- The standard library mathematical functions
- Complex numbers

The emphasis is on the Matrix library that makes handling of matrices (multidimensional arrays) trivial.

# 24.2 Size, precision, and overflow

When we use the built-in types and usual computational techniques, numbers are stored in fixed amounts of memory; that is, the integer types (int, long, etc.)
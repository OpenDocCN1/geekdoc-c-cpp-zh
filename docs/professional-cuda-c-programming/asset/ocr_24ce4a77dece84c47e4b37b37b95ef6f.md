Instructions that operate on floating-point values are naturally referred to as floating-point instructions. CUDA supports all the usual arithmetic operations for floating-point such as addition, multiplication, division, and subtraction.

As mentioned, CUDA and other programming models that adhere to IEEE 754 support two tiers of accuracy in floating-point: 32-bit and 64-bit. These different formats are also referred to as single-precision and double-precision, respectively. Double-precision values use twice as many bits as single-precision variables, double-precision values can correctly represent many more values. This means the set of double-precision values has both a finer granularity and wider range than single-precision values. For instance, a version of the earlier floating-point accuracy uses instead of single-precision floats:

```
double a = 3.1415927;
double b = 3.1415928;
if (a == b) {
    printf("a is equal to b\n");
} else {
    printf("a does not equal b\n");
}}
```

This code produces the expected output:

+   - a does not equal b

because the nearest representable values for a and b are not the same when using double-precision values.

Note that all compute-capable NVIDIA GPUs support single-precision floating-point, you will need an NVIDIA GPU of compute capability 1.3 or higher to use double-precision values.

Still, even double-precision values have their limits. A later section in this chapter, "Single-Precision vs. Double-Precision" will more quantitatively explore the challenges of floating-point programming and the differences between single- and double-precision floating-point.

# Intrinsic and Standard Functions

In addition to the separation between single- and double-precision operations, CUDA categorizes all arithmetic functions as intrinsic or standard functions. Standard functions are used to support operations that are accessible from, standardized across, the host and device. Standard functions include arithmetic operations from the C standard library such as sqrt, exp, and sin. Single-instruction operations like multiplication and addition are also included as standard functions.

CUDA intrinsic functions can be accessed from device code. Programming, a function being intrinsic, or built-in, means the compiler has special knowledge about its behavior, which enables more optimization and specialized instruction usage. This is true for CUDA intrinsic functions. In fact, many trigonometric functions are directly implemented in hardware on GPUs because they are used heavily in graphics applications (to perform translations, rotations, and so on for 3D visuals)

In CUDA, many intrinsic functions are related to a standard function, meaning that a standard function exists that implements the same operation. For example, the standard function for performing a double-precision floating-point square root is sqrt. The intrinsic version implementing
The SquareRoot_Test function, defined on line [23], checks the computations by interacting with the user. Only nonnegative values are allowed for input, as checked on line [29]. On line [31], the structured binding is used to simultaneously receive `val` and `flag`, returned by SquareRootApproxNewton.

Finding roots and approximating functions are great numerical analysis problems. Usually, more sophisticated methods such as Taylor series expansion are used. For more on this fascinating domain, we recommend the book by Press et al. (2007). We have only scratched the surface here, but the point is to make more conscious implementations involving FP numbers.

In this section, we learned about the following:

+   - The Newton algorithm for finding a function’s zero-crossing (finding roots)
+   - Computing a function derivative
+   - Representing functions with `std::function`
+   - Checking the convergence of a numerical algorithm that accounts for the specifics of floating-point numbers
+   - Passing many values from a function using `std::tuple` and `std::make_tuple`
+   - Applying the Newton zero-finding algorithm to compute the square root function

# 7.5  Summary

# Things to Remember

+   - Real numbers can be approximated either with fixed-point (FX) or floating-point (FP) representations
+   - In C++, only built-in integer types use FX representations. FX with fractions can be implemented as a class
+   - The spacing of FX numbers is uniform
+   - The spacing of FP values is not uniform – it is larger for numbers with larger exponents
+   - FP allows for a greater dynamic range of values than FX
+   - Rounding errors are inevitable when representing real numbers in FX and FP formats
+   - Computations with FX and FP numbers can result in overflow, underflow, or roundoff errors
+   - Subtracting close values can lead to severe cancelation errors
+   - IEEE 754 defines standards for FP representation. The most common are the single-precision (`float`) and double-precision (`double`) formats
+   - The machine epsilon ε conveys the value represented by the lowest bit of the significand. This is the difference between 1.0 and the next closest higher value representable in the FP format. The product of ε·D provides a spacing assessment around an FP number D
+   - In C++, FP values are rounded to the nearest, whereas integer values are rounded toward 0 (cutting off the fraction)
+   - The `std::numeric_limits<T>` class conveys information about the numerical properties of a type T, such as minimum and maximum values, etc
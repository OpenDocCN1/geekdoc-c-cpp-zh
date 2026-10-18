
What this means is that if $y$ happened to be $\sqrt{x}$, the previous equation would be fulfilled. So, let’s rename the variables as follows:

$$x^2-a=0$$

Now $a$ denotes the constant input argument for which we wish to determine the value of $\sqrt{a}$, while $x$ is a running variable. Equation (7.50) has exactly the form of the zero-finding problem defined in Eq. (7.46). Hence, we can use the previous Newton algorithm to solve Eq. (7.50). The found value of a root will be a good approximation of what we are looking for: $\sqrt{a}$. The previous idea is realized in the code shown in Listing 7.16.

```cpp
namespace NewtonZero
{

    // Compute the square root of the arg
auto SquareRootApproxNewton( const FP arg )
{
    // This is a reverse function of the square root
    auto sq_root = [ arg = arg ] ( double x ) { return x * x - arg; };

    return FindZero( sq_root, 1.0 );
}
```

On line [11], the NewtonZero namespace is opened again. Then, the function SquareRootApproxNewton, defined on line [15], computes the approximate value of the square root of its argument arg. To do this, we only need the definition of the function, as in Eq. (7.50). Again, this is implemented on line [18] using the lambda function. Then, on line [20], the result of FindZero is returned (discussed in the previous section).

```cpp
void SquareRoot_Test( void )
{
    std::cout << "Enter positive value to compute the square root ";

    double arg {};

    if ( ! ( std::cin >> arg ) || arg < 0.0 ) return;

    auto [ val, flag ] = SquareRootApproxNewton( arg );

    if( flag )
        std::cout << "sqrt( " << arg << " )= " << val << std::endl;
    else
        std::cout << "Cannot compute the square root" << std::endl;

}
} // End of NewtonZero
```

The SquareRoot_Test function, defined on line [23], checks the computations by interacting with the user. Only nonnegative values are allowed for input, as checked on line [29]. On line [31], the structured binding is used to simultaneously receive `val` and `flag`, returned by SquareRootApproxNewton.

Finding roots and approximating functions are great numerical analysis problems. Usually, more sophisticated methods such as Taylor series expansion are used. For more on this fascinating domain, we recommend the book by Press et al. (2007). We have only scratched the surface here, but the point is to make more conscious implementations involving FP numbers.

In this section, we learned about the following:

+   - The Newton algorithm for finding a function’s zero-crossing (finding roots)
+   - Computing a function derivative
+   - Representing functions with `std::function`
+   - Checking the convergence of a numerical algorithm that accounts for the specifics of floating-point numbers
+   - Passing many values from a function using `std::tuple` and `std::make_tuple`
+   - Applying the Newton zero-finding algorithm to compute the square root function

# 7.5 Summary

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

+   1. Convert the value \( 87_{10} \), analyzed in Section 7.1, to the equivalent representations with the following bases: \( B = 3 \), \( B = 5 \), \( B = 11 \).
+   2. Repeat the subtraction operation from Section 7.1.4, but use Eq. (7.9).
+   3. Using Eqs. (7.10) and (7.11), derive the formulas and algorithms for summation and multiplication of two values in these representations.
+   4. Using bit operations, implement the left and right round shifts described in Table 7.3.
+   5. Using one of the FxFor types defined in Listing 7.8, compute the roots of a second-order polynomial. Analyze the allowable range and maximum error. Devise a method for computing the square root in the fixed-point format.
+   6. Using FxFor types, in the student grade project in Chapter 3, eliminate the floating-point type `double`; see Listing 3.3.
+   7. Refactor the code in Listing 3.4, line [81], to represent matrices with FxFor data. Verify the matrix multiplication in Listing 3.23. What can you change on line [35] to increase computation accuracy and the allowable range?
+   8. Extend the class FxFor presented in Section 7.3.2 to contain flags signaling overflow situations in operations.
+   9. In the class FxFor, replace the standard wrap-around rounding with the value-saturation mechanism. That is, when trying to extend the value beyond the storage data capacity, sustain the maximum allowable value.
+   10. Explain the benefits and pitfalls of the floating-point number representation.
+   11. What are FP rounding errors?
+   12. What are overflow and underflow when computing with FP numbers?
+   13. What is the machine epsilon, and how can it be used in computations with FP numbers?
+   14. Write a program to generate floating-point values, as shown in Figures 7.7 and 7.8.
+   15. Using a plot drawing library such as gnuplot (www.gnuplot.info), draw diagrams with floating-point values.
+   16. Check std::numeric_limits< T > for float, double, and long double in your system. Check it for int and long.
+   17. Using the Newton method from Section 7.4.8, write code to compute a local extremum and both roots of the square equation. Compare with the solution given by Eqs. (7.40) and (7.41).
+   18. The second parameter of the procedure FindZero in Listing 7.16 is the iteration start value, which was arbitrarily set to 1.0. However, the closer it is to a real, but unknown, value of the square root, the faster convergence can be expected. For an estimate of this start value, write a function for finding the square root with the bisection method (see Algorithm 2.3).
+   19. Modify the code shown in Listing 7.16 to compute \(\sqrt[3]{x}\).
+   20. Let's assume a series of \( N \) pairs \( (x_i, y_i) \) is given. Develop and implement an algorithm for computing coefficients \( a \), \( b \), and \( c \) of the square polynomial of the form \( ax_i^2 + bx_i + c \sim y_i \) that fits best the series of pairs.

+   21. In the function InnerProduct_SortAlg, we used std::sort to arrange the summands in order. Can you explain why this helps? What should the sort order be? What is the time complexity of this solution?
+   22. Rewrite the matrix multiplication procedure in Listing 3.23 using the Kahan algorithm for summation.
+   23. The broad group of definite integrals 
+   
+   _b_ ^_b_ f(x) dx _a_ _a_
+   
+   of integrable functions f can be approximated by the following summation:
+   
+   _S<sub>N</sub>_ = _N_ _N_ _f_ (_c<sub>i</sub>_) _Δx<sub>i</sub>_, where _c<sub>i</sub>_ <|unk|> (_x<sub>i</sub>,x<sub>i</sub>_+_1_), _Δx<sub>i</sub>_ = _x<sub>i</sub>_+_1_-_x<sub>i</sub>_ and _x_<sub>1</sub> = _a_, _x<sub>N</sub>_ = _b_.
+   (7.52)
+   
+   Assuming division of the integration interval <|unk|> _a_, _b_ <|unk|> into a number _N_ of equal partitions, the previous summation can be further simplified as follows:
+   
+   <|unk|> _Δx<sub>i</sub>_ = _Δx_ = _x<sub>N</sub>_-_x_<sub>1</sub> _N_ = _b_-_a_ _N_ = _b_-_a_ _N_ and _x<sub>i</sub>_ = _i_ · _Δx_
+   (7.53)
+   
+   The point _c<sub>i</sub>_ can be chosen as the middle point between the points _x<sub>i</sub>_ and _x<sub>i</sub>_+_1_, as follows:
+   
+   _c<sub>i</sub>_ = _x<sub>i</sub>_+_1_+_x<sub>i</sub>_ _i_+_1_ = (_i_+_1_) · _Δx_+_i_ · _Δx_ _Δx_ (_i_+_1_ _2_) = _Δx_ (_i_+_1_ _2_)
+   (7.54)
+   
+   Insert Eqs. (7.53)-(7.54) into Eq. (7.52), and implement a method for numerically computing the definite integrals for any function. Represent functions programmatically, as discussed in Section 3.14.9.
+   24. Read, analyze, and implement the trapezoidal method for approximating definite integrals (https://en.wikipedia.org/wiki/Trapezoidal_rule). Compare this and the method developed in the previous step.
+   25. Using the integration procedure devised to compute Eq. (7.52), evaluate the constant π based on the following relation:
+   
+   <|unk|> _π_ = _b_ ^_b_ 4 _1_+_x_<sup>2</sup> _0_ _dx_
+   (7.55)
+   
+   Measure the execution time and accuracy of this approximation as a function of _N_.
+   26. Derive the values of the normalized positive minimum _kMin_ and maximum _kMax_ in the IEEE 754 format (Section 7.4.4). Then show that _kMin_ · _kMax_ = 4-2<sup>-(p-2)</sup>, where _p_ is the number of bits in the significand. Based on this relation derive the limiting conditions on the minimum and maximum values for the dividend _a_ and the divisor _b_ to assure valid divisions _c_=_a_/_b_ in the floating-point domain.
+   27. Refactor the FxFor class (Listing 7.1) by adding definition of the C++20 spaceship operator <=>.

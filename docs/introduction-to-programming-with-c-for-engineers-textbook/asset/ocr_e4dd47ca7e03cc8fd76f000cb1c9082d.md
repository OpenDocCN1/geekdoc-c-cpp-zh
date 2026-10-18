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
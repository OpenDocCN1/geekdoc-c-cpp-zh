# Modify 6.7

+   1. Write a value returning function with the following prototype:
+   
+   bool validate(double rad1, double rad2, double criticalRadius);
+   
+   The function should return true if rad1 < critical radius < rad2 and false otherwise. Use this function in program chapter6_8 to verify that the critical radius entered by the user lies in between the inner and outer radius read from the data file. Allow the user three tries to input a correct value for the critical radius. Your program should terminate with a message after three invalid entries for the critical radius.

+   2. Add a new method to the Point class. The prototype for the new method is:
+   
+   void Point::input(istream& in);
+   
+   The statement: p.input(fin) will input two floating point values from the input file stream fin and assign them to the x and y coordinates of the calling object. Use this method in program chapter6_8 to replace the two fin >> x >> y statements. Note: When you use p.input(fin), you do not need to call either set methods.

# 6.9 Numerical Technique: Roots of Polynomials

A polynomial is a function of a single object that can be expressed in the general form

f(x) = a_0 x^N + a_1 x^{N-1} + a_2 x^{N-2} + ... + a_{N-2}x^2 + a_{N-1}x + a_N, (6.1)

where the object is x and the coefficients are represented by a_0, a_1, ..., a_N. The degree of a polynomial is equal to the largest nonzero exponent. Therefore, the general form for a cubic (third-degree) polynomial is

g(x) = a_0 x^3 + a_1 x^2 + a_2 x + a_3,

and a specific example of a cubic polynomial is

h(x) = x^3 - 2x^2 + 0.5x - 6.5.

Note that, for each term in the equation, the sum of the coefficient subscript and the object exponent is equal to the polynomial degree using the notation in Equation (6.1).

# Polynomial Roots

The solutions to many engineering problems involve finding the roots of an equation of the form

y = f(x),

where the roots are the values of x for which y is equal to zero. Examples of applications in which we need to find roots of equations include designing the control system for a robot arm,
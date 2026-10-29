operators +, -, and * for addition, subtraction, and multiplication. Evaluation of a polynomial is implemented as a member function with one argument of type int. The evaluation member function returns the value obtained by plugging in its argument for x and performing the indicated operations.

Include four constructors: a default constructor, a copy constructor, a constructor with a single argument of type int that produces the polynomial that has only one constant term that is equal to the constructor argument, and a constructor with two arguments of type int that produces the one-term polynomial whose coefficient and exponent are given by the two arguments. [In the previous notation the polynomial produced by the one-argument constructor is of the simple form consisting of only a0. The polynomial produced by the two-argument constructor is of the slightly more complicated form a0x^n.] Include a suitable destructor. Include member functions to input and output polynomials.

When the user inputs a polynomial, the user types in the following:
a_n x^n + a_{n-1} x^{n-1} + ... + a0

However, if a coefficient a_i is 0, the user may omit the term a_i x^i. For example, the polynomial
3x^4 + 7x^2 + 5
can be input as
3x^4 + 7x^2 + 5

It could also be input as
3x^4 + 0x^3 + 7x^2 + 0x^1 + 5

If a coefficient is negative, a minus sign is used in place of a plus sign, as in the following examples:
3x^5 - 7x^3 + 2x^1 - 8
-7x^4 + 5x^2 + 9

A minus sign at the front of the polynomial, as in the second of the above two examples, applies only to the first coefficient; it does not negate the entire polynomial. Polynomials are output in the same format. In the case of output, the terms with 0 coefficients are not output. To simplify input, you can assume that polynomials are always entered one term per line and that there will always be a constant term a0. If there is no constant term, the user enters 0 for the constant term, as in the following:
12x^8 + 3x^2 + 0

4. Part A. The annotation in Display 17.24 says that a real SearchTree template class should have a copy constructor, an overloaded assignment operator, other overloaded operators, and other member functions. Obtain the code for Display 17.24 and add declarations for

![](bbox=[0.05, 0.92, 0.22, 0.98])
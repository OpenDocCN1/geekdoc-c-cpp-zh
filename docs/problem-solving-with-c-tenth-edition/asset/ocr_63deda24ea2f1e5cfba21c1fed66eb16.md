the head of a new linked list that contains all of the nodes in the original two lists. The nodes in this longer list are also sorted from smallest to largest values. Note that your function will neither create nor destroy any nodes. When the function call ends, the two pointer variable arguments should have the value NULL.

3. Design and implement a class whose objects represent polynomials. The polynomial

$a_n x^n + a_{n-1} x^{n-1} + \dots + a_0$

will be implemented as a linked list. Each node will contain an int value for the power of x and an int value for the corresponding coefficient. The class operations should include addition, subtraction, multiplication, and evaluation of a polynomial. Overload the operators +, -, and * for addition, subtraction, and multiplication.

Evaluation of a polynomial is implemented as a member function with one argument of type int. The evaluation member function returns the value obtained by plugging in its argument for x and performing the indicated operations. Include four constructors: a default constructor, a copy constructor, a constructor with a single argument of type int that produces the polynomial that has only one constant term that is equal to the constructor argument, and a constructor with two arguments of type int that produces the one-term polynomial whose coefficient and exponent are given by the two arguments. (In the notation above, the polynomial produced by the one-argument constructor is of the simple form consisting of only a0. The polynomial produced by the two-argument constructor is of the slightly more complicated form a_n x^n.) Include a suitable destructor. Include member functions to input and output polynomials.

When the user inputs a polynomial, the user types in the following:

$a_n x^n + a_{n-1} x^{n-1} + \dots + a_0$

However, if a coefficient a_i is zero, the user may omit the term a_i x^i. For example, the polynomial

$3x^4 + 7x^2 + 5$

can be input as

3x^4 + 7x^2 + 5

It could also be input as

3x^4 + 0x^3 + 7x^2 + 0x^1 + 5
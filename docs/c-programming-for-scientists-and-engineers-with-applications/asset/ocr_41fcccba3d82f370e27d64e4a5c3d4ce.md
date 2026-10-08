f. Declare and define the following constants, giving them the obvious values.

three, plus, e, gravity

+   3. Answer the following questions
   a. In C the built-in data types are \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

   and \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

   b. In C the derived data types are \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\, and \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.

# 2.3 Arithmetic Operations and Expressions

Engineering and scientific computing involves arithmetic operations and arithmetic expressions. Arithmetic operations can be performed on numeric data of type int, float, and double, which have the usual arithmetic operations built into the language. Millions of arithmetic operations are performed every day in engineering and scientific calculations. Computers are designed to perform them very quickly.

# 2.3.1 Arithmetic Operators and Operations

The basic arithmetic operations are expressed in C using the following symbols:

+   addition +
subtraction -
multiplication *
division /
nremainder %

Each of these has multiple meanings depending on the declared types of the operands.

Exponentiation is performed in C by using the function pow(double, double), from the math library. The addition and subtraction symbols can be used with either one operand a unary plus (e.g., +245), a unary minus (e.g., -12), or two operands (to indicate addition or subtraction). Unary operators should be separated by parentheses so that two operators do not immediately follow each other. The following examples show the use of the operators.
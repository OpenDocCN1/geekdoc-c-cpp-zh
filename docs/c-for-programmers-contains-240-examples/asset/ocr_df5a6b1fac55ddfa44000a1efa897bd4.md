```
std::cout << "Sum is " << number1 + number2 << std::endl;
```

thus eliminating the need for the variable sum.

A powerful feature of C++ is that you can create your own data types called classes (we introduce this capability in Chapter 3 and explore it in depth in Chapters 9 and 10). You can then “teach” C++ how to input and output values of these new data types using the >> and << operators (this is called *operator overloading*—a topic we explore in Chapter 11).

# 2.5 Arithmetic

Figure 2.6 summarizes the C++ *arithmetic operators*. The *asterisk* (*) indicates multiplication and the *percent sign* (%) is the modulus operator that will be discussed shortly. The arithmetic operators in Fig. 2.6 are all binary operators.

*Integer division* (i.e., where both the numerator and the denominator are integers) yields an integer quotient; for example, the expression 7 / 4 evaluates to 1 and the expression 17 / 5 evaluates to 3. Note that any fractional part in integer division is discarded (i.e., truncated)—no rounding occurs.

C++ provides the *modulus operator*, %, that yields the remainder after integer division. The modulus operator can be used only with integer operands. The expression x % y yields the remainder after x is divided by y. Thus, 7 % 4 yields 3 and 17 % 5 yields 2. In later chapters, we discuss many interesting applications of the modulus operator, such as determining whether one number is a multiple of another (a special case of this is determining whether a number is odd or even).

![](bbox=[0.166, 0.535, 0.218, 0.576])

> **Common Programming Error 2.3**
> 
> Attempting to use the modulus operator (%) with noninteger operands is a compilation error.

| C++ operation | C++ arithmetic operator | Algebraic expression | C++ expression |
|---|---|---|---|
| Addition | + | f + 7 | f + 7 |
| Subtraction | - | p − c | p - c |
| Multiplication | * | bm or b · m | b * m |
| Division | / | x / y or x ÷ y | x / y |
| Modulus | % | r mod s | r % s |

**Fig. 2.6**  |  Arithmetic operators.

# Parentheses for Grouping Subexpressions

Parentheses are used in C++ expressions in the same manner as in algebraic expressions. For example, to multiply a times the quantity b + c we write a * ( b + c ).

# Rules of Operator Precedence

C++ applies the operators in arithmetic expressions in a precise sequence determined by the following *rules of operator precedence*, which are generally the same as those followed in algebra:
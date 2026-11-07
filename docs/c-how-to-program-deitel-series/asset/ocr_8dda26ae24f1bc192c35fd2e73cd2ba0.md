![](bbox=[0.472, 0.116, 0.62, 0.188])

**Fig. 2.7**  |  Memory locations after storing values in the variables for number1 and number2.

*replaces* whatever value was stored in sum. The calculated sum of number1 and number2 is placed into variable sum without regard to what value may already be in sum—that value is lost). After sum is calculated, memory appears as in Fig. 2.8. The values of number1 and number2 appear exactly as they did before the calculation. These values were used, but not destroyed, as the computer performed the calculation. Thus, when a value is read out of a memory location, the operation is nondestructive.

![](bbox=[0.472, 0.376, 0.62, 0.487])

**Fig. 2.8**  |  Memory locations after calculating and storing the sum of number1 and number2.

# ## 2.6 Arithmetic

Most programs perform arithmetic calculations. Figure 2.9 summarizes the C++ **arithmetic operators**. Note the use of various special symbols not used in the standard. The **asterisk (*)** indicates *multiplication* and the **percent sign (%)** is the *modulus operator* that will be discussed shortly. The arithmetic operators in Fig. 2.9 are all binary operators, i.e., operators that take two operands. For example, the expression number1 + number2 contains the binary operator + and the two operands number1 and number2.

**Integer division** (i.e., where both the numerator and the denominator are integers) yields an integer as quotient; for example, the expression 7 / 4 evaluates to 1 and the expres-

| C++ operation | C++ arithmetic operator | Algebraic expression | C++ expression |
|---|---|---|---|
| Addition | + | *f + 7* | f + 7 |
| Subtraction | - | *p − c* | p − c |
| Multiplication | * | *bm or b · m* | b * m |
| Division | / | *x / y or x/y or x ÷ y* | x / y |
| Modulus | % | *r mod s* | r % s |

**Fig. 2.9**  |  Arithmetic operators.
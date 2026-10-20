```
sum = number1 + number2; // add numbers, then store total in sum
```

performs the addition, then replaces any previous value in sum. After sum has been calculated, memory appears as shown in Fig. 2.10. The values of number1 and number2 appear exactly as they did before they were used in the calculation of sum. These values were used, but not destroyed, as the computer performed the calculation. When a value is read from a memory location, the process is nondestructive.

|  |  |
|---|---|---|
| number1 | 45 |
| number2 | 72 |
| sum | 117 |

Fig. 2.10 | Memory locations after storing the sum of number1 and number2.

# 2.7 Arithmetic

Most programs perform arithmetic calculations. The arithmetic operators are summarized in Fig. 2.11. Note the use of various special symbols not used in algebra. The asterisk (*) indicates multiplication, and the percent sign (%) is the remainder operator, which we’ll discuss shortly. The arithmetic operators in Fig. 2.11 are binary operators, because each operates on two operands. For example, the expression f + 7 contains the binary operator + and the two operands f and 7.

| Java operation | Operator | Algebraic expression | Java expression |
|---|---|---|---|
| Addition | + | f + 7 | f + 7 |
| Subtraction | - | p - c | p - c |
| Multiplication | * | b m | b * m |
| Division | / | x / y or x/y or x ÷ y | x / y |
| Remainder | % | r mod s | r % s |

Fig. 2.11 | Arithmetic operators.

Integer division yields an integer quotient. For example, the expression 7 / 4 evaluates to 1, and the expression 17 / 5 evaluates to 3. Any fractional part in integer division is simply discarded (i.e., truncated)—no rounding occurs. Java provides the remainder operator, %, which yields the remainder after division. The expression x % y yields the remainder after x is divided by y. Thus, 7 % 4 yields 3, and 17 % 5 yields 2. This operator is most commonly used with integer operands but can also be used with other arithmetic types. In this chapter’s exercises and in later chapters, we consider several interesting applications of the remainder operator, such as determining whether one number is a multiple of another.
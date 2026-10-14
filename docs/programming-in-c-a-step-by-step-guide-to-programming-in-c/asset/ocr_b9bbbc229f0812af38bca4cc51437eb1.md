If the operands are of different types, the ‘lower’ type is automatically converted to the ‘higher’ type before the operation proceeds. The result is of higher type.
Given below is the sequence of rules that are applied while evaluating expressions.

All **short** type are automatically converted to **int**; then

+   1. If one of the operands is **long double**, the other will be converted to **long double** and the result will be **long double**;
+   2. else, if one of the operands is **double**, the other will be converted to **double** and the result will be **double**;
+   3. else, if one of the operands is **float**, the other will be converted to **float** and the result will be **float**;
+   4. else, if one of the operands is **unsigned long int**, the other will be converted to **unsigned long int** and the result will be **unsigned long int**;
+   5. else if one of the operands is **long int** and the other is **unsigned int**, then: if **unsigned int** can be converted to **long int**, the **unsigned int** operand will be converted as such and the result will be **long int**; else, both operands will be converted to **unsigned long int** and the result will be **unsigned long int**;
+   6. else, if one of the operands is **long int**, the other will be converted to **long int** and the result will be **long int**;
+   7. else, if one of the operands is **unsigned int**, the other will be converted to **unsigned int** and the result will be **unsigned int**;

The final result of an expression is converted to type of the variable on the left of the assignment sign before assigning the value to it. However, the following changes are introduced during the final assignment:

+   1. **float** to **int** causes truncation of the fractional part.
+   2. **double** to **float** causes rounding of digits.
+   3. **long int** to **int** causes dropping of the excess higher order bits

# 3.2.2 Mixed-mode Expressions
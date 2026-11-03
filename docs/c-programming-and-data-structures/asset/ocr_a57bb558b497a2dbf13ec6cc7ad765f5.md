# 1.57 TYPE CONVERSIONS IN EXPRESSIONS

# 1.57.1 Implicit Type Conversion

C permits mixing of constants and variables of different types in an expression. C automatically converts any intermediate values to the proper type so that the expression can be evaluated without losing any significance.

This automatic conversion is known as implicit type conversion.

During evaluation it adheres to very strict rules of type conversion. If the operands are of different types, the 'lower' type is automatically converted to the 'higher' type before the operation proceeds. The result is of the higher type. A typical type conversion process is illustrated in Fig. 1.93

Given below is the sequence of rules that are applied while evaluating expressions.

+   All short and char are automatically converted to int; then
+   1. if one of the operands is long double, the other will be converted to long double and the result will be long double;
+   2. else, if one of the operands is double, the other will be converted to double and the result will be double;
+   3. else, if one of the operands is float, the other will be converted to float and the result will be float;
+   4. else, if one of the operands is unsigned long int, the other will be converted to unsigned long int and the result will be unsigned long int;
+   5. else, if one of the operands is long int and the other is unsigned int, then
+      (a) if unsigned int can be converted to long int, the unsigned int operand will be converted as such and the result will be long int;
+      (b) else, both operands will be converted to unsigned long int and the result will be unsigned long int;
+   6. else, if one of the operands is long int, the other will be converted to long int and the result will be long int;
+   7. else, if one of the operands is unsigned int, the other will be converted to unsigned int and the result will be unsigned int.

![](bbox=[0.22, 0.78, 0.78, 0.94])

Fig. 1.93 Process of implicit type conversion
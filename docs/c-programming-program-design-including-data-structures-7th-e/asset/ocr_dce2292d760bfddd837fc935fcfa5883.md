+   8.  
+      a. Rewrite the definition of the `class complexType` so that the arithmetic and relational operators are overloaded as nonmember functions.  
+      b. Write the definitions of the member functions of the `class complexType` as designed in part a.  
+      c. Write a test program that tests various operations on the `class complexType` as designed in parts a and b. Format your answer with two decimal places.

+   9.  
+      a. Extend the definition of the `class newString` as follows:  
+         i. Overload the operators `+` and `+=` to perform the string concatenation operations.  
+         ii. Add the function `length` to return the length of the string.  
+      b. Write the definition of the function to implement the operations defined in part a.  
+      c. Write a test program to test various operations on the `newString` objects.

10. Rational fractions are of the form $a / b$, in which $a$ and $b$ are integers and $b \ne 0$. In this exercise, by “fractions” we mean rational fractions. Suppose $a / b$ and $c / d$ are fractions. Arithmetic operations on fractions are defined by the following rules:

$$a / b + c / d = (ad + bc) / bd$$

$$a / b - c / d = (ad - bc) / bd$$

$$a / b \times c / d = ac / bd$$

$$(a / b) / (c / d) = ad / bc,$$ in which $c / d \ne 0$.

Fractions are compared as follows: $a / b$ op $c / d$ if $ad$ op $bc$, in which op is any of the rational operations. For example, $a / b < c / d$ if $ad < bc$.

Design a `class`—say, `fractionType`—that performs the arithmetic and relational operations on fractions. Overload the arithmetic and relational operators so that the appropriate symbols can be used to perform the operation. Also, overload the stream insertion and stream extraction operators for easy input and output.

Write a C++ program that, using the `class fractionType`, performs operations on fractions.

Among other things, test the following: Suppose x, y, and z are objects of type fractionType. If the input is 2/3, in the statement:

```
cin >> x;
```
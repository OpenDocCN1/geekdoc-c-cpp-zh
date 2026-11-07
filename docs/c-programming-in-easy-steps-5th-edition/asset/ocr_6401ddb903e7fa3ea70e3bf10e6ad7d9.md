# Doing arithmetic

The arithmetical operators commonly used in C++ programs are listed in the table below, together with the operation they perform:

| Operator: | Operation: |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |
| ++ | Increment |
| -- | Decrement |

The operators for addition, subtraction, multiplication, and division act as you would expect. Care must be taken, however, to bracket expressions where more than one operator is used to clarify the expression – operations within innermost parentheses are performed first:

```
```cpp
a = b * c - d % e / f ;        // This is unclear.
a = ( b * c ) - ( ( d % e ) / f );   // This is clearer.
```
```

The % modulus operator will divide the first given number by the second given number and return the remainder of the operation. This is useful to determine if a number has an odd or even value.

![](bbox=[0.118, 0.536, 0.207, 0.595])

Values used with operators to form expressions are called “operands” – in the expression 2 + 3 the numerical values 2 and 3 are the operands.

The ++ increment operator and -- decrement operator alter the given number by one and return the resulting value. These are most commonly used to count iterations in a loop. Counting up, the ++ operator increases the value by one, while counting down, the -- decrement operator decreases the value by one.

The increment and decrement operators can be placed before or after a value to different effect. If placed before the operand (prefix), its value is immediately changed; if placed after the operand (postfix), its value is noted first, then the value is changed.

![](bbox=[0.118, 0.756, 0.187, 0.8])

arithmetic.cpp

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use
+      ```cpp
+      #include <iostream>
+      using namespace std ;
+      ```
+   2. Add a main function containing a final **return** statement
+      ```cpp
+      int main()
+      ```
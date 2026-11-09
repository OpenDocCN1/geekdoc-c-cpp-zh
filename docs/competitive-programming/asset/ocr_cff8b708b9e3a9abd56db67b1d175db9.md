+   6. UVa 10061 - How many zeros & how many digits? (there exists a formula for this)  
+   7. UVa 10139 - Factorisors (there exists a formula for this)  
+   8. UVa 10858 - Recover Factorial  
+   9. UVa 10220 - I Love Big Numbers! (use Java BigInteger class)  
+   10. UVa 10323 - Factorial! You Must Be Kidding  
+   11. UVa 10780 - Again Prime? No time.  
+   12. UVa 11347 - Multifactorials  
+   13. UVa 11415 - Count the Factorials

# 5.4  Java BigInteger Class

# 5.4.1  Basic Features

When intermediate and/or final results of an integer-based mathematics computation cannot be stored in the largest built-in integer data type and the given problem does not use any modulo arithmetic technique, we have to resort to BigInteger (sometimes also called as BigNum) libraries. A simple example: try to compute 25! (factorial of 25). The result is 15,511,210,043,330,985,984,000,000 which is beyond the capacity of 64-bit unsigned long long in C/C++.

The way the BigInteger library works is to store the big integer as a (long) string. For example we can store 10²¹ inside a string num1 = “1,000,000,000,000,000,000,000” without problem whereas this is already overflow in a 64-bit unsigned long long in C/C++. Then, for common mathematical operations, the BigInteger library uses a kind of digit by digit operations to process the two big integer operands. For example with num2 = “17”, we have num1 * num2 as:

```
num1       =  1,000,000,000,000,000,000,000
num2       =                         17
           ------------------------------ *
             7,000,000,000,000,000,000,000
            10,000,000,000,000,000,000,000
           ------------------------------ +
num1 * num2 = 17,000,000,000,000,000,000,000
```

Addition and subtraction are two simpler operations in BigInteger. Multiplication takes a bit more programming job. Efficient division and raising number to a certain power are more complicated. Anyway, coding these library routines in C/C++ under stressful contest environment can be a buggy affair, even if we can bring notes containing such C/C++ library in ICPC. Fortunately, Java has a BigInteger class that we can use for this purpose (as of 9 August 2010, C++ STL currently does not have such library thus it is a good idea to use Java for BigInteger problems).

The Java BigInteger (BI) class supports the following basic integer operations: addition — add(BI), subtraction — subtract(BI), multiplication — multiply(BI), division — divide(BI), remainder — remainder(BI), combination of division and remainder — divideAndRemainder(BI), modulo — mod(BI) (slightly different to remainder(BI)), and power — pow(int exponent). For example, the following short Java code is the solution for UVa 10925 - Krakovia which simply requires BigInteger addition (to sum N large bills) and division (to divide the large sum to F friends).
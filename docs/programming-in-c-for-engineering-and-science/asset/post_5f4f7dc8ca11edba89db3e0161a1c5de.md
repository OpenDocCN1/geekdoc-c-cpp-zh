
+   3. Parentheses in expressions must be paired. That is, for each left parenthesis, there must be exactly one matching right parenthesis that occurs later in the expression.

+   4. Both real and integer division are denoted by /; which operation is performed is determined by the type of the operands.

+   5. All multiplications must be indicated by *; for example, 2*n is valid, but 2n is not.

+   6. A semicolon must appear at the end of each expression (assignments, input, output, etc.) that is meant to be a programming statement.

+   7. There are many operators in C++—we’ve barely scratched the surface—and remembering their priorities will be increasingly difficult. For this reason, it is wise to use parentheses in complex expressions to clearly specify the order in which the operators are to be applied.

## TEST YOURSELF

### Section 4.2

Find the value of each of the expressions in Questions 1–8, or explain why it is not a valid expression.

+   1. 3 - 2 - 1
+   2. 2.0 + 3.0 / 5.0
+   3. 2 + 3 / 5
+   4. 5 / 2 + 3

+   5. 7 + 6 % 5
+   6. (7 + 6) % 5
+   7. (2 + 3 * 4) / (8 - 2 + 1)
+   8. 12.0 / 1.0 * 3.0

Questions 9–18 assume that two, three, and four are reals with values 2.0, 3.0, and 4.0, respectively; intEight and intFive are integers with values 8 and 5, respectively; and ASCII representation is used for characters (see Appendix A). Find the value of each expression.

+   9. two + three * three
+   10. intFive / 3
+   11. (three + two / four) * 2
+   12. intEight / intFive * 5.1
+   13. four * 2 / two * 2

+   14. intFive * 2 / two * 2
+   15. 'c' - 1
+   16. 'b' + 'c' - 'a'
+   17. int(two * three / four)
+   18. (int)(two * three / four)

Tell whether each is a valid C++ statement. If it is not valid, explain why it is not.

+   1. pi = 3.0;
+   2. 0 = n;
+   3. n = n + n;
+   4. n + n = n;
+   5. m = 1;
+   6. m = "1";
+   7. m = n = 1;
+   8. c = '65';
+   9. c = 65;

+   10. c = '1';
+   11. c = "1";
+   12. m = m;
+   13. pi = m;
+   14. m = pi;
+   15. m++;
+   16. m + n;
+   17. ++pi;

For Questions 18-23, assume that the following declarations have been made:

```
int intEight = 8, intFive1 = 5, intFive2 = 5, jobId;
double two = 2.0, three = 3.0, four = 4.0, xValue;
```

Find the value assigned to the given variable or indicate why the statement is not valid.

+   18. xValue = three + two / four;
+   19. xValue = intEight / intFive1 + 5.1;
+   20. jobId = intEight / intFive1 + 5.1;
+   21. jobId = intFive1++;
+   22. jobId = ++intFive2;
+   23. intEight *= 8;

For each of Questions 24-26, write a C++ assignment statement that calculates the given expression and assigns the result to the specified variable.

+   24. rate times time to distance
+   25. a² + b² to c
+   26. Assuming that x is an integer variable, write four different statements that increment x by 1.

## Section 4.4

+   1. In C++, input and output are carried out using ________, which connect an executing program with an input/output device.

2. (True or False) C++ has no input or output facilities built into the language.

3. ________ is the stream object associated with the keyboard; its type is ________.

4. ________ and ________ are stream objects associated with the screen; their type is ________.

5. The input operator is ________.

6. The output operator is ________.

7. The value produced by the input expression cin >> x is ________.

8. The value produced by the output expression cout << x is ________.

9. The input and output operators are (left or right) ________ associative.

10. ________ can be inserted into an output list to format the output of items.

Questions 11–13 assume the declarations

```
int number = 123;
double rate = 23.45678;
```

For each, show precisely the output that the set of statements produces, indicating blanks with _, or explain why an error occurs.

11. cout << number << rate << endl;

```
12. cout << '\n' << setw(5) << number << number + 1
    << setw(5) << number + 2
    << setw(1) << number + 4 << endl;
```

```
13. cout << showpoint << fixed
    << setw(8) << setprecision(0) << rate << endl
    << setw(8) << setprecision(1) << rate << endl
    << setw(8) << setprecision(2) << rate << endl
    << setw(8) << rate << endl
    << setprecision(1) << rate << endl;
```

Questions 14–17 assume the declarations

```
int number1, number2, number3;
double real1, real2, real3;
```

For each, tell what value, if any, will be assigned to each variable, or explain why an error occurs, when the statement is executed with the given input data:

14. cin >> number1 >> number2 >> number3;      Input:  11 22
    33 44

```
15. cin >> real1 >> real2 >> real3;
Input: 1.1 2 3.3 4
```

```
16. cin >> number1 >> number2 >> number3;
Input: 1.1 2 3.3 4
```

```
17. cin >> number1 >> real1 >> number2;
>> real2 >> number3 >> real3;
Input: 1.1 2
3.3 4
5.5 6
```

+   1. sqrt(6.0 + 3.0)
+   2. pow(2.0, 3)
+   3. floor(2.34)
+   4. ceil(2.34)
+   5. sqrt(r2 + r3 + r4)
+   6. pow(r2, i4)
+   7. sqrt(pow(4.0, 2))
+   8. sqrt(pow(-4.0, 2))
+   9. pow(sqrt(-4.0), 2)
+   10. ceil(8.0 / 5.0)
+   11. floor(8.0 / 5.0)
+   12. pow(r2, i4) / pow(r4, i3)
+   13. pow(i3, pow(r2, 2))
+   14. sqrt(i4 * pow(r4, 3))
+   15. floor(sqrt(i4 - r3))

For Questions 16–19, write C++ expressions that will compute the given expression.

+   16. The square root of the average of x and y
+   17. | a / (b + c) | (where |x| denotes the absolute value of x)
+   18. a^x, computed as e^{ln a} (where ln is the natural logarithm function)
+   19. The real quantity amount rounded to the nearest hundredth

## EXERCISES

Find the value of each of the expressions in Exercises 1–19, or explain why it is not a valid expression.

+   1. 9 - 5 - 3
+   2. 2 / 3 + 3 / 5
+   3. 9.0 / 2 / 5
+   4. 9 / 2 / 5
+   5. 2.0 / 4
+   6. (2 + 3) % 2

7. 7 % 5 % 3
8. (7 % 5) % 3
9. 7 % (5 % 3)
10. (7 % 5 % 3)
11. 25 * 1 / 2
12. 25 * 1.0 / 2
13. 25 * (1 / 2)

14. -3.0 * 5.0
15. 5.0 * -3.0
16. 12 / 2 * 3
17. ((12 + 3) / 2) / (8 - (5 + 1))
18. ((12 + 3) / 2) / (8 - 5 + 1)
19. (12 + 3 / 2) / (8 - 5 + 1)

Exercises 20–24 assume that r1 and r2 are reals with values 2.0 and 3.0, respectively; i1, i2, and i3 are integers with values 4, 5, and 8, respectively; and ASCII representation is used for characters (see Appendix A). Find the value of each expression.

20. r1 + r2 * r2
21. i3 / 3
22. i3 / 3.0

23. (r2 + r1) * i1
24. i3 / i2 * 5.1

Write C++ expressions to compute each of the quantities in Exercises 25–28.

25. 10 + 5B - 4AC
26. The average of m and n (their sum divided by two)
27. Three times the difference 4 - n divided by twice the quantity m² + n²
28. Using the given values of cost, verify that the statement
cost = double(int(cost*100.0 + 0.5)) / 100.0;
can be used to convert each of these real values of cost to dollars, rounded to the nearest cent.
a) 12.342    d) 12.340
b) 12.348    e) 13.0
c) 12.345

29. Write an expression similar to that in Exercise 28 that rounds a real amount x to the nearest tenth.

30. Write an expression similar to that in Exercise 28 that rounds a real amount x to the nearest thousandth.

## Section 4.3

Exercises 1–16 assume that number is an integer variable, xValue and yValue are real variables, and grade is a character variable. Tell whether each is a valid C++ statement. If it is not valid, explain why it is not.

+   1. xValue = 2.71828;
+   2. 3 = number;
+   3. grade = 'B+';
+   4. number = number + number;
+   5. xValue = 1;
+   6. grade = A;
+   7. number + 1 = number;
+   8. xValue = '1';
+   9. xValue = yValue = 3.2;
+   10. yValue = yValue;
+   11. xValue = 'A';
+   12. grade = grade + 10;
+   13. xValue /= yValue;
+   14. xValue = number;
+   15. number = yValue;
+   16. xValue = yValue++;

For Exercises 17–29, assume that the following declarations have been made:

```
int int16 = 16, int10 = 10, number;
double real4 = 4.0, real6 = 6.0, real8 = 8.0, xCoord;
char numeral = '2', symbol;
```

Find the value assigned to the given variable or indicate why the statement is not valid.

+   17. xCoord = (real4 + real6) * real6;
+   18. xCoord = (real6 + real4 / real8) * 2;
+   19. xCoord = int16 / int10 + 5;
+   20. number = int16 / int10 + 5;

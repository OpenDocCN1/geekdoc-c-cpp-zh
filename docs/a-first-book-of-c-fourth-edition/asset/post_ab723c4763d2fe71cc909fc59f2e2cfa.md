
# EXERCISES 5.3

+   1. 
+      a. `for(i = 1; i <= 20; i++)`
+      b. `for(icount = 1; icount <= 20; icount = icount + 2)`
+      c. `for(j = 1; j <= 100; j = j + 5)`
+      d. `for(icount = 20; icount >= 1; icount--)`
+      e. `for(icount = 20; icount >=1; icount = icount - 2)`
+      f. `for(count = 1.0; count <= 16.2; count = count + 0.2)`
+      g. `for(xcnt = 20.0; xcnt >= 10.0; xcnt = xcnt - 0.5)`

+   2. 
+      a. 20
+      b. 10
+      c. 20
+      d. 20
+      e. 10
+      f. 77
+      g. 21

+   3. 
+      a. 10
+      b. 1024
+      c. 75
+      d. -5
+      e. 40320
+      f. 0.03125

# Chapter 6

# EXERCISES 6.1

+   1. 
+      a. requires one int value
+      b. requires three values in this order: an int and two doubles
+      c. requires three values in this order: an int and two doubles
+      d. requires three values in this order: a char and two floats
+      e. requires two doubles
+      f. requires six values in this order: two ints, two chars and two doubles
+      g. requires four values in this order: two ints and two chars

```
2. a. void check(int num1, double num2, double num3)
   {
       cout << "In check()\n";
       cout << "The value of num1 is " << num1 << endl;
       cout << "The value of num2 is " << num2 << endl;
       cout << "The value of num3 is " << num3 << endl;
       return;
   }
```

```
3. a. void findAbs(double number)
{
    cout << "The absolute value of " << number << " is: ";
    if(number < 0)
        number = -number;
    cout << number << endl;
    return;
}
```

# EXERCISES 6.2

+   2. a. void check(int num1, float num2, double num3)
+      b. double findAbs(double x)
+      c. float mult(float first, float second)
+      d. int square(int number)
+      e. int powfun(int num, int exponent)
+      f. void table(void) or void table()

```
3. a. double rightTriangle(double a, double b)
{
    return sqrt((a * a) + (b * b));
}
```

b. See solution file pgm6-2cx3b.cpp.

```
4. a. double findAbs(double number)
{
    if(number < 0)
        number = -number;
    return number;
}
```

b. See solution file pgm6-2cx4b.cpp.

# EXERCISES 6.3

+   1. a. doubles amount
+      b. doubles price
+      c. ints minutes
+      d. chars key
+      e. doubles yield

```
2. void time(int& sec, int& min, int& hours)
```

```
3. a. void findMax(int x, int y, int& max)
{
    int maxnum;                // variable declaration

    if (x >= y)                // find the maximum number
        maxnum = x;
    else
        maxnum = y;
    max = maxnum;

    return;                    // return statement
}
```

# EXERCISES 6.4

1. a.

| Variable or Constant Name | Data Type | Scope |
|---|---|---|
| PRICE | int | global to main(), roi(), and step() |
| YEARS | long int | global to main(), roi(), and step() |
| YIELD | double | global to main(), roi(), and step() |
| bondtype | int | local to main() |
| interest | double | local to main() |
| coupon | double | local to main() |
| mat1 | int | local to roi() |
| mat2 | int | local to roi() |
| count | int | local to roi() |
| effectiveRate | double | local to roi() |
| first | double | local to step() |
| last | double | local to step() |
| numofyrs | int | local to step() |
| fracpart | double | local to step() |

2. a.

| Variable or Constant Name | Data Type | Scope |
|---|---|---|
| KEY | char | global to main(), func1(), and func2() |
| NUMBER | long int | global to main(), func1(), and func2() |
| a, b, c | int | local to main() |
| x, y | double | local to main() |
| secnum | double | global to func1() and func2() |
| num1, num2 | int | local to func1() |
| o, p | int | local to func1() |
| q | float | local to func1() |
| first, last | double | local to func2() |
| a, b, c, o, p | int | local to func2() |
| r | double | local to func2() |
| s, t, x | double | local to func2() |

3. All function parameters have local scope in their defined function. Note that although function parameters assume a value that depends on the calling function, these parameters can change values in their functions. This makes them behave as though they were local variables in the called function.

# EXERCISES 6.5

1. a. The storage categories available to local variables are auto, static, and register.

b. The storage categories available to global variables are extern and static. A local auto variable is unique to the function in which it's declared. Every time the function is called, the auto variable is re-created, as though it never existed. A local static variable is also unique to the function where it's declared. However, a static variable retains its last value and isn't re-created when its function is called again.

2. The first function declares yrs to be a static variable and assigns a value of 1 to it only once, when the function is compiled. Each time the function is called thereafter, the value in yrs is increased by 2. The second function also declares yrs to be static but assigns it the value 1 every time it's called, and the value of yrs after the function is finished will always be 3. By resetting the value of yrs to 1 each time it's called, the second function defeats the purpose of declaring the variable to be static.

```
6. char goodstr[1] = "Good Morning";
   char goodstr[1] = { 'G', 'o', 'o', 'd', ' ', 'M', 'o', 'r', 'n', 'i', 'n', 'g' };
   char goodstr[12] = { 'G', 'o', 'o', 'd', ' ', 'M', 'o', 'r', 'n', 'i', 'n', 'g' };
```

+   7. a. char message1[] = "Input the Following Data";
+         char message2[] = "----------------------";
+         char message3[] = "Enter the Date: ";
+         char message4[] = "Enter the Account Number: ";
+      b. See solution file pgm7-2ex7b.cpp.

# EXERCISES 7.3

+   1. void sortArray(double inArray[500])
+         void sortArray(double inArray[])
+   
+   2. char findKey(char select[256])
+         char findKey(char select[])
+   
+   3. double prime (double [256])
+         double prime (double [])

# EXERCISES 7.4

+   1. a. const int NUMROWS = 6;
+         const int NUMCOLS = 10;
+             int val[NUMROWS][NUMCOLS];
+   
+      b. const int NUMROWS = 2;
+         const int NUMCOLS = 5;
+             int val[NUMROWS][NUMCOLS];
+   
+      c. const int NUMROWS = 7;
+         const int NUMCOLS = 12;
+             char val[NUMROWS][NUMCOLS];
+   
+   2. The output is as follows:
+   
+      8    16    9    52    3    15    27    6    14    25    2    10

This page intentionally left blank

# Note:

+   - Page numbers followed by t indicate tables.
+   - Page numbers followed by +t indicate discussions plus tables.

# Symbols

& (ampersand): address operator, 258, 343

&& (ampersands). See AND operator

* (asterisk): indirection operator, 345, 351
See also multiplication operator

*/ (asterisk-slash): end comment symbol, 24

\ (backslash): escape character, 21, 41

\\ (backslashes): pathname item separator, 391, 661

\\ (backslash sequence, 41t

| (bar): bitwise OR operator, 100, 401

|| (bars). See OR operator

{} (braces): list delimiters, 303
See also statement delimiters

:: (colons). See scope resolution operator

, (comma): list item separator, 206, 303, 314

\" escape sequence, 41t

"" (double quotes): string delimiters, 20, 42, 43, 606

= (equals sign). See assignment operator

== (equals signs). See equality (equal to) operator

! (exclamation point). See NOT operator

!= (exclamation point-equals sign). See inequality (not equal to) operator

!infeq expression, 402, 409

> (greater than sign). See greater than operator

>= (greater than/equal sign). See greater than or equal to operator

>> (greater than signs): extraction operator, 118, 119, 132

< (less than sign). See less than operator

<= (less than/equal sign). See less than or equal to operator

<< (less than signs): insertion symbol, 18, 50

- (minus sign):
negation operator, 52, 53t
private visibility indicator, 572
See also subtraction operator

-> operator (data member access operator), 510, 716-717

-- (minus signs). See decrement operator

() . See parentheses

% (percent sign). See modulus operator

. (period). See dot operator

+ (plus sign): concatenation operator, 614t, 616, 619, 620
public visibility indicator, 572
See also addition operator

++ (plus signs). See increment operator

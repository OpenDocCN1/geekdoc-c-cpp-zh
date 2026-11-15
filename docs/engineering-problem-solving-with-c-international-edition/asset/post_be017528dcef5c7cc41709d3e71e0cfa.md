
Remember that the logarithm of a negative value or zero does not exist, and thus an execution error occurs if you use a logarithm function with a negative value for its argument.

An additional mathematical function that you may find useful is the abs function. This function computes the absolute value of an integer, and returns an integer value. The header file containing information relative to this function is stdlib.h, and it should be included in programs referencing this function.

## PRACTICE!

- Evaluate the following expressions:
- 1. floor(-2.6)
- 2. ceil(-2.6)
- 3. pow(2, -3)
- 4. sqrt(floor(10.7))
- 5. fabs(-10.2 * 5)
- 6. floor(ceil(10.8))
- 7. log10(100) + log10(0.001)
- 8. fabs(pow(-2, 5))

## Trigonometric Functions

Trigonometric functions

The trigonometric functions assume that all arguments are of type double and that they return values of type double. In addition, as previously stated, the trigonometric functions also assume that angles are represented in radians. To convert radians to degrees, or degrees to radians, use the following statements:

```
#define PI 3.141593
...
angle_deg = angle_rad * (180 / PI);
angle_rad = angle_deg * (PI / 180);
```

The trigonometric functions are included in the Standard C library, and a preprocessor directive including the information in math.h should be used with these functions. Following is a brief summary of these functions:

| sin(x) | This function computes the sine of x, where x is in radians. |
| --- | --- |
| cos(x) | This function computes the cosine of x, where x is in radians. |
| tan(x) | This function computes the tangent of x, where x is in radians. |
| asin(x) | This function computes the arcsine or inverse sine of x, where x must be in the range [-1, 1]. The function returns an angle in radians in the range [-π/2, π/2]. |
| acos(x) | This function computes the arccosine or inverse cosine of x, where x must be in the range [-1, 1]. The function returns an angle in radians in the range [0, π]. |
| atan(x) | This function computes the arctangent or inverse tangent of x. The function returns an angle in radians in the range [-π/2, π/2]. |
| atan2(y, x) | This function computes the arctangent or inverse tangent of the value y/x. The function returns an angle in radians in the range [-π, π]. |

Note that the atan function always returns an angle in Quadrant I or IV, whereas the atan2 function returns an angle that can be in any quadrant, depending on the signs of x and y. Thus, in many applications, the atan2 function is preferred over the atan function.

The other trigonometric and inverse trigonometric functions can be computed with the use of the following equations:

sec x = 1 / cos x \qquad asec x = acos ( 1 / x )
csc x = 1 / sin x \qquad acsc x = asin ( 1 / x )
cot x = 1 / tan x \qquad acot x = acos ( x / \sqrt{1 + x^2} )

Using degrees instead of radians is a common error in programs with trigonometric functions.

## PRACTICE!

In Problems 1 through 3, give assignment statements for computing the indicated values, assuming that the variables have been declared and given appropriate values. Also assume that the following declarations have been made:

```
#define g 9.8
#define PI 3.141593
```

- 1. Velocity computation:
- Velocity = \sqrt{v_0^2 + 2a(x - x_0)}.

- 2. Length contraction:
- Length = k \sqrt{1 - (v/c)^2}.

- 3. Distance of the center of gravity from a reference plane in a hollow cylinder sector:
- Center = \frac{38.1972(r^2 - s^2)\sin a}{(r^2 - s^2) \cdot a}.

In Problems 4 through 6, give the equations that correspond to the assignment statement.

- 4. Electrical oscillation frequency:
- frequency = 1/sqrt(2*pi*c/L);

- 5. Range for a projectile:
- range = (v0*v0/g)*sin(2*theta);

- 6. Speed of a disk at the bottom of an incline:
- v = sqrt(2*g*h/(1 + I/(m*pow(r,2))));

## Hyperbolic Functions*

Hyperbolic functions are functions of the natural exponential function e^x; the inverse hyperbolic functions are functions of the natural logarithm function ln x. These functions are useful in specialized applications, such as the design of some types of digital filters. C includes several hyperbolic functions, as shown in the following descriptions:

- sinh(x) This function computes the hyperbolic sine of x, which is equal to (e^x - e^-x) / 2.
- cosh(x) This function computes the hyperbolic cosine of x, which is equal to (e^x + e^-x) / 2.
- tanh(x) This function computes the hyperbolic tangent of x, which is equal to sinh x / cosh x.

Additional hyperbolic functions and the inverse hyperbolic functions can be computed with these relationships:

- coth x = cosh x / sinh x (for x != 0).
- sech x = 1 / cosh x.
- csch x = 1 / sinh x.
- asinh x = ln(x + sqrt(x^2 + 1)).
- acosh x = ln(x + sqrt(x^2 - 1)) (for x >= 1).
- atanh x = 1/2 ln((1+x)/(1-x)) (for |x| < 1).
- acoth x = 1/2 ln((x+1)/(x-1)) (for |x| > 1).
- asech x = ln((1 + sqrt(1-x^2))/x) (for 0 < x <= 1).
- acsch x = ln(1/x + sqrt(1+x^2)/|x|) (for x != 0).

Many of the hyperbolic functions and inverse trigonometric functions have restrictions on the range of acceptable values for arguments. If the arguments are entered from the keyboard, remind the user of the range restrictions. In the next chapter, we introduce C statements that allow you to determine if a value is in the proper range within the program.

![](img/02c4582f051c5b51776411c92b079035_86_0.png)

## PRACTICE!

Give assignment statements for calculating the following values, given the value of x. (Assume that the value of x is in the proper range of values for the calculations.)

- 1. coth x
- 2. sec x
- 3. csc x
- 4. acoth x
- 5. acosh x
- 6. acsc x

## 2.9 Character Functions

Numerous functions are available to use with character data. There are functions designed for character input and output, functions to convert characters between uppercase and lowercase, and functions to perform character comparisons. In this section, we will discuss these character functions.

### Character I/O

Although printf and scanf functions can be used to print and read characters using the %c specifier, C also contains special functions for reading and printing characters. The getchar function reads the next character from the keyboard and returns the integer value of the character; the putchar function prints a character to the computer screen.

The putchar function takes one integer argument and returns an integer value. The execution of the putchar function causes the character that corresponds to the integer argument to be written to the computer screen. If several putchar function references are made in a row, the characters are printed one after another on the same line, until a newline character is printed. Thus, the following statements cause the characters ab to be printed on one line, followed by the character c on the next line:

```
putchar('a');
putchar('b');
putchar('\n');
putchar('\t');
```

The same information could be printed using the integer values that correspond to the characters (see Table 2.3):

```
putchar(97);
putchar(98);
putchar(10);
putchar(99);
```

The getchar function reads the next character from the keyboard and returns the integer value of the character. If several getchar function references are made in a row, the processing of characters continues until an EOF is received. The EOF is a special value defined as a symbolic constant in stdio.h. Recall that a variable defined with the char data type can represent only the 128 ASCII characters. The value of EOF is outside of this range. Because an integer variable can represent more than 128 values, we use an int type instead of a char type to receive the value returned by the getchar function so that we can store the EOF and detect the end of data. The following statements cause one character to be read from the keyboard and printed on a new line:

```
int c;
...
putchar('\n');
c = getchar();
putchar(c);
putchar('\n');
```

The actual value of the EOF is system dependent. The EOF character is often represented by the control-z character. A control-z is entered from the keyboard by pressing the control (ctrl) key, and then pressing the z key while the control key is still pressed. This combination of characters is often written as ^z (control-z), but is not the same as pressing the ^ key with the z key. The use of EOF will be discussed in more detail in Chapter 3.

### Character Comparisons

Character functions

The Standard C library contains additional functions for use with characters. These character functions fall into two categories; one set of functions is used to convert characters between uppercase and lowercase, and the other set is used to perform character comparisons. The following preprocessor directive should be used in programs referencing these character functions:

```
#include <ctype.h>
```

The following statement converts the lowercase letter stored in the variable ch to an uppercase character and stores the result in the character variable upper:

```
upper = toupper(ch);
```

If ch is a lowercase letter, the function toupper returns the corresponding uppercase letter; otherwise, the function returns ch. Note that no change is made to the variable ch.

Each character function requires an integer argument, and each function returns an integer value. The character comparison functions return a nonzero value if the comparison is true; otherwise, they return a zero. We now list these functions with a brief explanation:

| tolower(ch) | If ch is an uppercase letter, this function returns the corresponding lowercase letter; otherwise, it returns ch. |
| --- | --- |
| toupper(ch) | If ch is a lowercase letter, this function returns the corresponding uppercase letter; otherwise, it returns ch. |
| isdigit(ch) | This function returns a nonzero value if ch is a decimal digit; otherwise, it returns zero. |
| islower(ch) | This function returns a nonzero value if ch is a lowercase letter; otherwise, it returns zero. |
| isupper(ch) | This function returns a nonzero value if ch is an uppercase letter; otherwise, it returns a zero. |
| isalpha(ch) | This function returns a nonzero value if ch is an uppercase letter or a lowercase letter; otherwise, it returns a zero. |
| isalnum(ch) | This function returns a nonzero value if ch is an alphabetic character or a numeric digit; otherwise, it returns a zero. |

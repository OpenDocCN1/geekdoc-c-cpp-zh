| Function | Description | Example |
|---|---|---|
| `exp(x)` | exponential function e^x | `exp(1.0)` is 2.718282<br>`exp(2.0)` is 7.389056 |
| `fabs(x)` | absolute value of x | `fabs(5.1)` is 5.1<br>`fabs(0.0)` is 0.0<br>`fabs(-8.76)` is 8.76 |
| `floor(x)` | rounds x to the largest integer not greater than x | `floor(9.2)` is 9.0<br>`floor(-9.8)` is -10.0 |
| `fmod(x, y)` | remainder of x/y as a floating-point number | `fmod(2.6, 1.2)` is 0.2 |
| `log(x)` | natural logarithm of x (base e) | `log(2.718282)` is 1.0<br>`log(7.389056)` is 2.0 |
| `log10(x)` | logarithm of x (base 10) | `log10(10.0)` is 1.0<br>`log10(100.0)` is 2.0 |
| `pow(x, y)` | x raised to power y (x^y) | `pow(2, 7)` is 128<br>`pow(9, .5)` is 3 |
| `sin(x)` | trigonometric sine of x (x in radians) | `sin(0.0)` is 0 |
| `sqrt(x)` | square root of x (where x is a nonnegative value) | `sqrt(9.0)` is 3.0 |
| `tan(x)` | trigonometric tangent of x (x in radians) | `tan(0.0)` is 0 |

**Fig. 6.2** | Math library functions. (Part 2 of 2.)

# 6.4 Function Definitions with Multiple Parameters

Let’s consider functions with *multiple* parameters. Figures 6.3–6.5 modify class GradeBook by including a user-defined function called maximum that determines and returns the largest of three int grades. When the application executes, the main function (lines 5–13 of Fig. 6.5) creates one GradeBook object (line 8) and calls its inputGrades member function (line 11) to read three integer grades from the user. In class GradeBook’s implementation file (Fig. 6.4), lines 52–53 of member function inputGrades prompt the user to enter three integer values and read them from the user. Line 56 calls member function maximum (defined in lines 60–73). Function maximum determines the largest value, then the return statement (line 72) returns that value to the point at which function inputGrades invoked maximum (line 56). Member function inputGrades then stores maximum’s return value in data member maximumGrade. This value is then output by calling function displayGradeReport (line 12 of Fig. 6.5). [Note: We named this function displayGradeReport because subsequent versions of class GradeBook will use this function to display a complete grade report, including the maximum and minimum grades.] In Chapter 7, we’ll enhance class GradeBook to process sets of grades.
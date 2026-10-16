
# Programming in C++ for Engineering and Science

+   1. Character constants must be enclosed in single quotes. In particular, string literals cannot be assigned to variables of type char.
+   2. Values of type char are stored as their (integer) numeric codes. Assigning an integer to a char variable may produce an unexpected symbol.
+   3. String constants must be enclosed within double quotes.
+   4. Comments are enclosed within /* and */ or between // and the end of the line. Be sure that:
    • Each beginning delimiter /* has a matching end delimiter */. Failure to use these in pairs can produce strange results.
    • There is no space between the / and the * or between the two slashes.
+   5. Every { must be matched by a }.
+   6. All identifiers must be declared. Attempting to use an identifier that has not been declared will produce a compilation error. Also, remember that C++ distinguishes between uppercase and lowercase letters.
+   7. Using a variable that has not been assigned a value may produce "garbage."
+   8. Keywords, identifiers, and constants may not be broken at the end of a line, nor may they contain blanks (except, of course, a string constant may contain blanks).

+   1. List the fundamental data types provided in C++.
+   2. List the three integer type variations.
+   3. List the three real types.
+   4. A constant of a particular type is called a(n) ________.
+   5. (True or false) 0123 and 123 represent the same integer value.
+   6. (True or false) 0xA and 10 represent the same integer value.
+   7. (True or false) All real literals are treated as being of type double.
+   8. Character literals must be enclosed in ________.
+   9. (True or false) '1/n' is a valid character literal.
+   10. (True or false) '\n' is a valid character literal.
+   11. '\n' is an example of a(n) ________ sequence.

12. String constants must be enclosed in _______.

For Questions 13–20, tell whether each is a legal identifier. If is it not legal, indicate the reason.

+   13. calorie
+   14. W_D_4_0
+   15. 70mph
+   16. milesPerHour
+   17. miles per hour
+   18. miles_per_hour
+   19. ps.175
+   20. type-A

For Questions 21–40, tell whether each is an integer literal, a real literal, a character literal, or a string literal. If it is none of these, indicate the reason.

+   21. 1234
+   22. 1,234
+   23. 1.234
+   24. -1.
+   25. 123e4
+   26. 123-4
+   27. 0.123E-4
+   28. +1235
+   29. 12+34
+   30. $12.34
+   31. '12+34'
+   32. 'one'
+   33. one
+   34. "Ohm's law"
+   35. "1234"
+   36. 01234
+   37. 0x1234
+   38. E4
+   39. '#1'
+   40. '\32'

41. Write a declaration for a variable count of type int.

42. Write declarations for variables time of type unsigned, temperature of type float, and scale of type char.

43. Repeat Question 41, but initialize count to zero.

44. Repeat Question 42, but initialize time to 9999, temperature to zero, and scale to a blank.

45. Write constant declarations to associate CELSIUS_FREEZE with the integer 0 and CELSIUS_BOIL with the integer 100.

46. Write constant declarations to associate EARTH with 1.5E10 and MARS with 1.2E12.

## EXERCISES

For Exercises 1–20, determine if each is a valid C++ identifier. If it is not, give a reason.

+   1. x Axis
+   2. x-Axis
+   3. x_Axis
+   4. xAxis
+   5. carbon14
+   6. 3M
+   7. PDQ123
+   8. angle
+   9. angel
+   10. anlge
+   11. PS.175
+   12. x
+   13. 4
+   14. n/4
+   15. $M
+   16. zzzzzz
+   17. z_z_z_z_z_z
+   18. A+
+   19. R2-D2
+   20. R2_D2

For Exercises 21–40, classify each as an integer literal, a real literal, or neither. If it is neither, give a reason.

+   21. 5,280
+   22. 5280
+   23. "5280"
+   24. 528.0
+   25. 5280e0
+   26. -5280
+   27. --5280
+   28. +5280
+   29. 52+80
+   30. $52.80
+   31. 52E80
+   32. E5280
+   33. eighty
+   34. 0.528E0
+   35. .00005280
+   36. 5.2e-80
+   37. +52E+80
+   38. -(-1)
+   39. -0
+   40. -1/2

For Exercises 41–52, determine if each is a valid string literal. If it is not, give a reason.

+   41. "X"
+   42. "123"
+   43. INCH"
+   44. "square feet"
+   45. "Print \"MPH\""
+   46. "isn't"
+   47. "constant"
+   48. "$1.98"
+   49. "DON\'T"
+   50. "12 + 34"
+   51. "\'twas"
+   52. "\"A\"\"B\"\"C\""

For Exercises 53–56, write constant declarations to associate each name with the specified constant.

+   53. 40.0 with the name REGULAR_HOURS and 1.5 with the name OVERTIME_FACTOR
+   54. Planck’s constant 6.6256 × 10^-34 with the name PLANCK
+   55. FAHRENHEIT_FREEZE with the integer 32 and FAHRENHEIT_BOIL with the integer 212
+   56. 0 with ZERO, * with ASTERISK, and an apostrophe with APOSTROPHE

For Exercises 57–60, write declarations for each variable.

+   57. length and momentOfInertia of type double
+   58. population and year of type unsigned
+   59. mileage of type double, cost and distance of type unsigned
+   60. alpha and beta of type long, code of type char, and root of type double

For Exercises 61–62, write declarations to declare each variable to have the specified type and initial value.

+   61. numberOfDeposits and numberOfChecks to be of type int, each with an initial value of 0; totalDeposits and totalChecks to be of type double, each with an initial value of 0.0; and serviceCharge to be of type double with an initial value of 0.25
+   62. symbol_1 and symbol_2 to be of type char and with a blank character and a semicolon for initial value, respectively; and debug to be of type char with an initial value of T.

63. Write constant declarations that associate the current year with the name YEAR and 99999.99 with MAXIMUM_SALARY and variable declarations that declare number and prime to be of type int and scale to be of type char.

## PROGRAMMING PROBLEMS

+   1. Write a program to convert a measurement given in feet to the equivalent number of (a) yards, (b) inches, (c) centimeters, and (d) meters (1 ft = 12 in, 1 yd = 3 ft, 1 in = 2.54 cm, 1 m = 100 cm).
+   2. Write a program to convert a weight given in ounces to the equivalent number of (a) pounds, (b) tons, (c) grams, and (d) kilograms (1 lb = 16 oz, 1 ton = 2000 lb, 1 oz = 28.349523 g, 1 kg = 1000 g).
+   3. For three resistors connected in series, the total resistance is the sum of the individual resistances and by Ohm’s law, the current in the circuit is given by *amps = voltage / total_resistance*. Write a program that inputs the voltage and three resistances and then calculates and displays the current.
+   4. Proceed as in Problem 3, but for resistors connected in parallel for which the total resistance is computed using the formula

$$total\_resistance = \frac{1}{\frac{1}{resistor1} + \frac{1}{resistor2} + \frac{1}{resistor3}}$$

> “Arithmetic is being able to count up to twenty without taking off your shoes.”
> 
> — MICKEY MOUSE

> “A little inaccuracy sometimes saves tons of explanation.”
> 
> — SAKI (H. H. MUNROE)

In the preceding chapter we looked at how to represent a problem’s objects as *software objects* (also called *program entities*) using C++ type statements. This chapter focuses on the operations provided in C++ that may be used to solve a problem and how they are used to form expressions of various kinds.

## 4.1 INTRODUCTORY EXAMPLE: EINSTEIN’S EQUATION

### 4.1.1 Problem

Suppose that the professor for your physics course has assigned a large problem set that is due by the next class meeting and that many of the problems require using Einstein’s equation to calculate the amount of energy released by a quantity of matter for a given mass. Because of the time pressure, mistakes will likely be made if all of the calculations are done by hand. It would be nice to have a program that could be used to check answers.

### 4.1.2 Object-Centered Design

#### 4.1.2.1 Behavior

The program should display on the screen a prompt for the quantity of matter (i.e., its mass). It will then read this value from the keyboard. The program should then use Einstein’s equation to compute the energy that can be produced by that quantity of matter and display this value to the screen along with a descriptive label.

#### 4.1.2.2 Objects

From our behavioral description, we can identify the following objects:

| Problem Objects | Type | Kind | Name |
|---|---|---|---|
| screen | output device | variable | `cout` |
| prompt | text string | constant | none |
| quantity of matter | double | variable | *mass* |
| keyboard | input device | variable | `cin` |
| quantity of energy | double | variable | *energy* |
| descriptive label | string | constant | none |

#### 4.1.2.3 Operations

Again, from our behavioral description, we have the following operations:

+   i. Output a string (prompt, descriptive label).
+   ii. Read a nonnegative numeric value (*mass*) from the keyboard.

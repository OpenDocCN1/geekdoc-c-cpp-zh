
# Programming Projects

regulations and tells how many people must be excluded in order to meet the fire

- 6. An employee is paid at a rate of $16.78 per hour for regular hours worked in a week. Any hours over that are paid at the overtime rate of one and one-half times that. From the worker's gross pay, 6% is withheld for Social Security tax, 14% is withheld for federal income tax. 5% is withheld for state tax, and 10% per week is withheld for union dues. If the worker has three or more dependents, then an additional $35 is withheld to cover the extra cost of health insurance beyond what the employer pays. Write a program that will read in the number of hours worked in a week and the number of dependents as input and then will output the worker's gross pay, each withholding amount, and the net-take home pay for the week.

- 7. One way to measure the amount of energy that is expended during exercise is to use metabolic equivalents (MET). Here are some METS for various activities:
  - Running 6 MPH: 10 METS
  - Basketball: 8 METS
  - Sleeping: 1 MET

The number of calories burned per minute may be estimated using the formula Calories/Minute = 0.0175 × 1 MET × (Weight in kilograms)

Write a program that inputs a subject's weight in pounds, the number of METS for an activity, and the number of minutes spent on that activity, and then outputs an estimate for the total number of calories burned. One kilogram is equal to 2.2 pounds.

- 8. The Babylonian algorithm to compute the square root of a positive number **n** is as follows:

  1. Make a **guess** at the answer (you can pick n/2 as your initial guess).
  2. Compute **r = n / guess**.
  3. Set **guess = (guess + r) / 2**.
  4. Go back to step 2 for as many iterations as necessary. The closer **guess** will be to the square root of **n**.

Write a program that inputs a double for **n**, iterates through the Babylonian algorithm five times, and outputs the answer as a *double* to two decimal places. Your answer will be most accurate for values of **n**.

- 9. The video games at your arcade output coupons depending on how well you play the game. You can redeem 10 coupons for a candy bar or 3 coupons for a gumball. You prefer candy bars to gumballs. Write a program that inputs the number of coupons you win and outputs how many candy bars and gumballs you can get if you spend all of your coupons on candy bars first and any remaining gumballs.

- 10. Write a program that allows the user to enter a time in seconds and then outputs how far an object would drop if it is in freefall for length of time. Assume no friction or resistance from air and a constant acceleration of 32 feet per second to gravity. Use the equation

Distance = $\frac{1}{2} \times acceleration \times time^2$

- 11. Write a program that inputs an integer that represents a length of time in seconds. The program should then output the number of hours, minutes, and seconds that corresponds to that number of seconds. For example, if the user inputs 50391 total seconds then the program should output 13 hours, 59 minutes, and 51 seconds.

- 12. A simple rule to estimate your ideal body weight is to allow 110 pounds for the first 5 feet of height and 5 pounds for each additional inch. Write a program with a variable for the height of a person in feet and another variable for the additional inches and input values for these variables from the keyboard. Assume the person is at least 5 feet tall. For example, a person that is 6 feet and 3 inches tall would be represented with a variable that stores the number 6 and another variable that stores the number 3. Based on these values calculate and output the ideal body weight.

# 44 CHAPTER 1 C++ Basics

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_73_0.png)

# Flow of Control

## 2.1 BOOLEAN EXPRESSIONS 46

- Building Boolean Expressions 46
- Pitfall: Strings of Inequalities 47
- Evaluating Boolean Expressions 48
- Precedence Rules 50
- Pitfall: Integer Values Can be Used as Boolean Values 54

## 2.2 BRANCHING MECHANISMS 56

- if-else Statements 56
- Compound Statements 57
- Pitfall: Using = in Place of = 59
- Omitting the else 61
- Nested Statements 61
- Multway if-else Statement 62
- The switch Statement 62
- Pitfall: Forgetting a break in a switch Statement 65
- Tip: Use switch Statements for Menus 66
- Enumeration Types 66
- The Conditional Operator 67

## 2.3 LOOPS 67

- The while and do-while 68
- Increment and Decrement Operators 71
- The Comma Operator 72
- The for Statement 74
- Tip: Repeat-Times 76
- Pitfall: Semicolon in for Statement 77
- Nested Loops 80
- The break and continue 83

## 2.4 INTRODUCTION TO FILE INPUT 83

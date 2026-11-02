**2.30** *(Separating Digits in an Integer)* Write a program that inputs one five-digit number, separates the number into its individual digits and prints the digits separated from one another by three spaces each. [Hint: Use combinations of integer division and the remainder operation.] For example, if the user types in 42139, the program should print

```
4   2   1   3   9
```

**2.31** *(Table of Squares and Cubes)* Using only the techniques you learned in this chapter, write a program that calculates the squares and cubes of the numbers from 0 to 10 and uses tabs to print the following table of values:

| number | square | cube |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 1 | 1 |
| 2 | 4 | 8 |
| 3 | 9 | 27 |
| 4 | 16 | 64 |
| 5 | 25 | 125 |
| 6 | 36 | 216 |
| 7 | 49 | 343 |
| 8 | 64 | 512 |
| 9 | 81 | 729 |
| 10 | 100 | 1000 |

# ## Making a Difference

**2.32** *(Body Mass Index Calculator)* We introduced the body mass index (BMI) calculator in Exercise 1.12. The formulas for calculating BMI are

BMI = (weightInPounds × 703) / (heightInInches × heightInInches)

or

BMI = weightInKilograms / (heightInMeters × heightInMeters)

Create a BMI calculator application that reads the user’s weight in pounds and height in inches (or, if you prefer, the user’s weight in kilograms and height in meters), then calculates and displays the user’s body mass index. Also, the application should display the following information from the Department of Health and Human Services/National Institutes of Health so the user can evaluate his/her BMI:

| BMI VALUES | |
|---|---|
| Underweight: | less than 18.5 |
| Normal: | between 18.5 and 24.9 |
| Overweight: | between 25 and 29.9 |
| Obese: | 30 or greater |

> > [Note: In this chapter, you learned to use the int type to represent whole numbers. The BMI calculations when done with int values will both produce whole-number results. In Chapter 4 you’ll learn to use the double type to represent numbers with decimal points. When the BMI calculations are performed with doubles, they’ll both produce numbers with decimal points—these are called “floating-point” numbers.]
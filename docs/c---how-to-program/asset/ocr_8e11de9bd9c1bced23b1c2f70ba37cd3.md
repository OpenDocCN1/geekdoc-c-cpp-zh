Your program must use only three output statements, one of each of the following forms:

```
```c
printf( "%s", ... );
printf( "%s\n", ... );
puts( ... ); // outputs a newline
```
```

**3.40 (Powers of 3 with an Infinite Loop)** Write a program that keeps printing the powers of the integer 3, namely 3, 9, 27, 91, 273, and so on. Your loop should not terminate (i.e., you should create an infinite loop). What happens when you run this program?

**3.41 (Diameter, Circumference and Area of a Circle)** Write a program that reads the radius of a circle (as a float value) and computes and prints the diameter, the circumference and the area. Use the value 3.14159 for π.

**3.42** What’s wrong with the following statement? Rewrite it to accomplish what the programmer was probably trying to do.

```
```c
printf( "%d", --(x * y) );
```
```

**3.43 (Sides of a Triangle)** Write a program that reads three nonzero integer values and determines and prints whether they could represent the sides of a triangle.

**3.44 (Sides of a Right Triangle)** Write a program that reads three nonzero integers and determines and prints whether they could be the sides of a right triangle.

**3.45 (Factorial)** The factorial of a nonnegative integer *n* is written *n*! (pronounced “n factorial”) and is defined as follows:

*n*! = *n* · (*n* − 1) · (*n* − 2) · ⋯ · 1   (for values of *n* greater than or equal to 1)

*n*! = 1   (for *n* = 0).

For example, 5! = 5 · 4 · 3 · 2 · 1, which is 120.

+   a) Write a program that reads a nonnegative integer and computes and prints its factorial.
+   
+   b) Write a program that estimates the value of the mathematical constant *e* by using the formula:
+   
+   *e* = 1 + 1/1! + 1/2! + 1/3! + 1/4! + ⋯
+   
+   c) Write a program that computes the value of *eˣ* by using the formula:
+   
+   *eˣ* = 1 + *x*/1! + *x²*/2! + *x³*/3! + ⋯

# Making a Difference

**3.46 (World-Population-Growth Calculator)** Use the web to determine the current world population and the annual world population growth rate. Write an application that inputs these values, then displays the estimated world population after one, two, three, four and five years.

**3.47 (Target-Heart-Rate Calculator)** While exercising, you can use a heart-rate monitor to see that your heart rate stays within a safe range suggested by your trainers and doctors. According to the American Heart Association (AHA), the formula for calculating your *maximum heart rate* in beats per minute is 220 minus your age in years. Your *target heart rate* is a range that's 50–85% of your maximum heart rate. [**Note:** These formulas are estimates provided by the AHA. Maximum and target heart rates may vary based on the health, fitness and gender of the individual. Always consult a physician or a qualified health-care professional before beginning or modifying an exercise program.]

Create a program that reads the user’s birthday and the current day (each consisting of the month, day and year). Your program should calculate and display the person’s age (in years), the person’s maximum heart rate and the person’s target-heart-rate range.
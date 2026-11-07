7. Modify the roll dice program, Example 6-4, so that it allows the user to enter the desired sum of the numbers to be rolled. Also allow the user to call the `rollDice` function as many times as the user desires.

8. The following formula gives the distance between two points, $(x_1, y_1)$ and $(x_2, y_2)$ in the Cartesian plane:

$$\sqrt{(x_2-x_1)^2+(y_2-y_1)^2}$$

Given the center and a point on the circle, you can use this formula to find the radius of the circle. Write a program that prompts the user to enter the center and a point on the circle. The program should then output the circle’s radius, diameter, circumference, and area. Your program must have at least the following functions:

+   a. **distance:** This function takes as its parameters four numbers that represent two points in the plane and returns the distance between them.
+   
+   b. **radius:** This function takes as its parameters four numbers that represent the center and a point on the circle, calls the function `distance` to find the radius of the circle, and returns the circle’s radius.
+   
+   c. **circumference:** This function takes as its parameter a number that represents the radius of the circle and returns the circle’s circumference. (If r is the radius, the circumference is $2\pi r$.)
+   
+   d. **area:** This function takes as its parameter a number that represents the radius of the circle and returns the circle’s area. (If r is the radius, the area is $\pi r^2$.)

Assume that $\pi = 3.1416$.

9. Rewrite the program in Programming Exercise 15 of Chapter 4 (cell phone company) so that it uses the following functions to calculate the billing amount. (In this programming exercise, do not output the number of minutes during which the service is used.)

+   a. **regularBill:** This function calculates and returns the billing amount for regular service.
+   
+   b. **premiumBill:** This function calculates and returns the billing amount for premium service.

10. Write a program that takes as input five numbers and outputs the mean (average) and standard deviation of the numbers. If the numbers are $x_1$, $x_2$, $x_3$, $x_4$, and $x_5$, then the mean is $x = (x_1 + x_2 + x_3 + x_4 + x_5)/5$ and the standard deviation is:

$$s=\sqrt{\frac{(x_1-x)^2+(x_2-x)^2+(x_3-x)^2+(x_4-x)^2+(x_5-x)^2}{5}}$$
list and returns the sine of x, using the Taylor series (shown next)
with an accuracy of 0.0000000001.

\(sinx=x-\frac{x^3}{3!}+\frac{x^5}{5!}-\frac{x^7}{7!}+\cdots\)

Hint: Keep in mind that x is in radians, and \(\frac{x^1}{1!}=x\).

+   iii. Write a subprogram named `degrees_to_rad()` that accepts an angle
+   in degrees through its formal argument list and returns its radian
+   equivalent. It is given that \(2\pi=360^\circ\).

+   iv. Using the subprograms `my_sin()` and `degrees_to_rad()` cited above,
+   write a PHP script that displays the sinus of all integers from \(0^\circ\) to
+   \(360^\circ\).

+   2. Do the following:
+   i. Write a subprogram named `is_leap()` that accepts a year through its
+   formal argument list and returns `true` or `false` depending on
+   whether or not that year is a leap year.

+   ii. Write a subprogram named `num_of_days()` that accepts a month and
+   a year and returns the number of the days in that month. If that
+   month is February and the year is a leap year, the subprogram must
+   return the value of 29.
+   Hint: Use the subprogram `is_leap()` cited above.

+   iii. Write a subprogram named `check_date()` that accepts a day, a
+   month, and a year and returns `true` or `false` depending on whether
+   or not that date is valid.

+   iv. Using the subprograms cited above, write a PHP script that prompts
+   the user to enter a date (a day, a month, and a year) and then
+   calculates and displays the number of days that have passed
+   between the beginning of the given year and the given date.
+   Moreover, the script should validate data input and display an error
+   message when the user enters any non-data date.

+   3. In a computer game, players roll two dice. The player who gets the greatest
+   sum of dice gets one point. After ten rolls, the player that wins is the one
+   with the greatest sum of points. Do the following:
+   i. Write a subprogram named `dice()` that returns a random integer
+   between 1 and 6.

+   ii. Using the subprogram `dice()` cited above, write a PHP script that
+   prompts two players to enter their names and then each player
+   consecutively “rolls” two dice. This process repeats ten times and
+   the player that wins is the one with the greatest sum of points.

+   4. The LAV Car Rental Company has rented 40 cars, which are divided into
+   three categories: hybrid, gas, and diesel. The company charges for a car
+   according to the following table.
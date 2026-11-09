pizza, the modified application also will display the number of slices into which you can divide the pizza. For this exercise, use the number 14.13 as the area of a pizza slice.

+   a. Use Windows to make a copy of the Circle Area Solution folder. Save the copy in the ClearlyVB\Chap07 folder. Rename the copy Pizza Circle Area Solution.
+   b. Open the Circle Area Solution (Circle Area Solution.sln) file contained in the Pizza Circle Area Solution folder. Make the appropriate modifications to the interface and code. Display the number of slices with no decimal places.
+   c. Save and then start the application. Test the application using 10 as the circle’s radius. The area is 314.16 and the number of slices is 22. Now test it using 6 as the radius. The area and number of slices should be 113.10 and 8. Stop the application and close the solution.

8. In this exercise, you modify the application that you created in Exercise 8 in Chapter 6. If you did not complete Chapter 6’s Exercise 8, you will need to do so before you can complete this exercise.

**ADVANCED**

+   a. Use Windows to copy the Sun Solution folder from the ClearlyVB\Chap06 folder to the ClearlyVB\Chap07 folder.
+   b. Open the Sun Solution (Sun Solution.sln) file contained in the ClearlyVB\Chap07\Sun Solution folder. Modify the code so that it uses Decimal variables and Decimal named constants. Format the gross pay and taxes with two decimal places. Format the net pay with a dollar sign and two decimal places.
+   c. Save and then start the application. Test the application using 35.5 as the hours worked and 9.56 as the pay rate. The gross pay will be 339.38. The taxes will be 67.88, 27.15, and 6.79. The net pay will be $237.57. Notice that the total of the taxes and net pay differs by a penny from the gross pay. The “penny off” problem occurs because the ToString method rounds the gross pay and taxes before they are displayed. However, the amounts are not rounded when they are used to calculate the net pay. Stop the application.
+   d. You can fix the “penny off” problem using the Math.Round method. The method’s syntax is **Math.Round**(*number*, *decimalPlaces*). In the syntax, *number* is the number to be rounded, and *decimalPlaces* indicates the number of decimal places to include in the rounding. For example, **Math.Round**(4.658, 2) evaluates to 4.66. Use the Math.Round method to fix the “penny off” problem.
+   e. Save and then start the application. Test the application using 35.5 as the hours worked and 9.56 as the pay rate. This time the net pay is $237.56. Stop the application, then close the solution.
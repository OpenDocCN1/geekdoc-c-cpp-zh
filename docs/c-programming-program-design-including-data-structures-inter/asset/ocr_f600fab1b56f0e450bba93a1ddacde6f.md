# PROGRAMMING EXERCISES

+   1. In Chapter 10, the class `clockType` was designed to implement the time of day in a program. Certain applications, in addition to hours, minutes, and seconds, might require you to store the time zone. Derive the class `extClockType` from the class `clockType` by adding a member variable to store the time zone. Add the necessary member functions and constructors to make the class functional. Also, write the definitions of the member functions and the constructors. Finally, write a test program to test your class.

+   2. In this chapter, the class `dateType` was designed to implement the date in a program, but the member function `setDate` and the constructor do not check whether the date is valid before storing the date in the member variables. Rewrite the definitions of the function `setDate` and the constructor so that the values for the month, day, and year are checked before storing the date into the member variables. Add a member function, `isLeapYear`, to check whether a year is a leap year. Moreover, write a test program to test your class.

+   3. Chapter 10 defined the class `circleType` to implement the basic properties of a circle. (Add the function `print` to this class to output the radius, area, and circumference of a circle.) Now every cylinder has a base and height, where the base is a circle. Design a class `cylinderType` that can capture the properties of a cylinder and perform the usual operations on the cylinder. Derive this class from the class `circleType` designed in Chapter 10. Some of the operations that can be performed are as follows: calculate and print the volume, calculate and print the surface area, set the height, set the radius of the base, and set the center of the base. Also, write a program to test various operations on a cylinder.

+   4. Amanda and Tyler opened a business that specializes in shipping liquids, such as milk, juice, and water, in cylindrical containers. The shipping charges depend on the amount of the liquid in the container. (For simplicity, you may assume that the container is filled to the top.) They also provide the option to paint the outside of the container for a reasonable amount. Write a program that does the following:
+   
+      a. Prompts the user to input the dimensions (in feet) of the container (radius of the base and the height).
+      b. Prompts the user to input the shipping cost per liter.
+      c. Prompts the user to input the paint cost per square foot. (Assume that the entire container including the top and bottom needs to be painted.)
+      d. Separately outputs the shipping cost and the cost of painting.
+   
+      Your program must use the class `cylinderType` (designed in Programming Exercise 3) to store the radius of the base and the height of the container. (Note that 1 cubic feet = 28.32 liters or 1 liter = 0.0353146667 cubic feet.)
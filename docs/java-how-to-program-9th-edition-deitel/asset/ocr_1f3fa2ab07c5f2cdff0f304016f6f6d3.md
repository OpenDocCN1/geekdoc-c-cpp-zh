k) ______ is a framework for running downloaded programs outside the browser.
l) A(n) ______ document provides the information that Java Web Start needs to download and run a program.
m) The ______ enables you to manage the Java Web Start programs on your system.

# Answers to Self-Review Exercise

23.1 a) init, start, paint. b) stop. c) JApplet (or Applet). d) appletviewer. e) start. f) HTML. g) init. h) paint. i) destroy. j) <applet>, </applet>. k) Java Web Start. l) Java Network Launch Protocol (JNLP). m) Java Cache Viewer.

# Exercises

23.2 (Arithmetic) Write an applet that asks the user to enter two floating-point numbers, obtains the two numbers from the user and draws their sum, product (multiplication), difference and quotient (division). Use the techniques shown in Fig. 23.9.

23.3 (Comparing Numbers) Write an applet that asks the user to enter two floating-point numbers, obtains the numbers from the user and displays the two numbers, then displays the larger number followed by the words "is larger" as a string on the applet. If the numbers are equal, the applet should print the message "These numbers are equal." Use the techniques shown in Fig. 23.9.

23.4 (Arithmetic and Numeric Comparisons) Write an applet that inputs three floating-point numbers from the user and displays the sum, average, product, smallest and largest of these numbers as strings on the applet. Use the techniques shown in Fig. 23.9.

23.5 (Diameter, Circumference and Area of a Circle) Write an applet that asks the user to input the radius of a circle as a floating-point number and draws the circle’s diameter, circumference and area. Use the value 3.14159 for π. Use the techniques shown in Fig. 23.9. [Note: You may also use the predefined constant Math.PI for the value of π. This constant is more precise than the value 3.14159. Class Math is defined in the java.lang package, so you do not need to import it.] Use the following formulas (r is the radius):

diameter = 2r
circumference = 2πr
area = πr²

23.6 (Largest and Smallest) Write an applet that reads five integers, determines which are the largest and smallest integers in the group and prints them. Draw the results on the applet.

23.7 (Draw a Checkerboard Pattern) Write an applet that draws a checkerboard pattern as follows:

![](bbox=[0.12, 0.995, 0.9, 1.15])

23.8 (Drawing Rectangles) Write an applet that draws rectangles of different sizes and locations.

23.9 (Drawing Rectangles Based on User Input) Write an applet that allows the user to input values for the arguments required by method drawRect, then draws a rectangle using the four input values.
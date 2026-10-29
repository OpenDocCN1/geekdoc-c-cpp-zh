your first response might be "The program clearly asks you to enter integer values." Experienced programmers, however, understand that their responsibility is to ensure that a program anticipates and appropriately handles all inputs users can possibly enter. To achieve this goal, think about what can go wrong with your program as you develop it, and then have another person or group test the program thoroughly.¹

The basic approach to handling invalid data input is called user-input validation, which means checking the entered data during or immediately after it has been entered, and then giving users a way to reenter any invalid data. User-input validation is an essential part of any commercially viable program; if done correctly, it protects a program from attempting to process data that can cause computational problems. You see how to do this type of validation in Chapters 4 and 5, when you learn about C++’s selection and repetition statements.

# EXERCISES 3.4

+   1. (Practice) For the following declaration statements, write one or more statements using the cin object that causes the computer to pause while the user enters the appropriate data:
+    a. int firstnum;
+    b. double grade;
+    c. double secnum;
+    d. char keyval;
+    e. int month, years;
+       double average;
+    f. char ch;
+       int num1,num2;
+       double grade1,grade2;
+    g. double interest, principal, capital;
+       double price, yield;
+    h. char ch, letter1,letter2;
+       int num1,num2,num3;
+    i. double temp1,temp2,temp3;
+       double volts1,volts2;

+   2. (Program) a. Write, compile, and run a C++ program that displays the following prompts:
+    Enter the length of the room:
+    Enter the width of the room:
+    After each prompt is displayed, your program should use a cin object call to accept data from the keyboard for the displayed prompt. After the width of the room is entered, your program should calculate and display the area of the room. The area displayed should be calculated by using the formula area = length × width and should be included in an appropriate message.
+    b. Check the area displayed by the program written for Exercise 2a by calculating the result manually.
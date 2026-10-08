# CHAPTER 14 Sequential Access Files

# LAB 14-2 Plan and Create

In this lab, you will plan and create an algorithm for Cheryl Liu, the owner of a candy shop named Sweets-4-You. The problem specification is shown in Figure 14-6.

![](bbox=[0.311, 0.086, 0.378, 0.149])

Cheryl Liu is the owner of a candy shop named Sweets-4-You. She wants a program that uses a function to display the menu:

+   1 Add Records
2 Display Total Sales
3 Exit the program

If Cheryl selects one, the program will call a function that prompts Cheryl to enter each customer's name and amount. Function should save Cheryl's entries in a sequential access file named sales.txt. If Cheryl selects option two, the program will call a function that calculates and displays the total of the sales amounts stored in the sales.txt file. The program should end only when Cheryl selects option 3.

Figure 14-6 Problem specification for Lab 14-2

The Sweets-4-You program will use functions: `main`, `getChoice`, `addRecords`, and `displayTotal`. Figure 14-17 shows the IPO chart information C++ instructions for the `main` and `getChoice` functions. The `main` function begins by declaring and initializing an `int` variable `choice`. After calling the `getChoice` function to display the menu, the `getChoice` function prompts Cheryl to enter her choice of menu options: 1 to add records, 2 to display the total sales, or 3 to exit the program. The `getChoice` function returns Cheryl's response to the `main` function, which assigns the value to the `choice` variable. The next instruction in the `main` function is a selection structure that compares the `choice` variable with the number 1. If the choice equals 1, the `main` function calls the `addRecords` function to add one or more records to the sequential access file. When the `addRecords` function ends, the `main` function calls `getChoice` to display the menu and get another choice from the user. If the `choice` variable does not contain the number 1, the nested selection structure in the `main` function compares the `choice` variable with the number 2. If the choice contains 2, the `main` function calls the `displayTotal` function to total the sales amounts stored in the sequential access file and then display the total on the screen. When the `displayTotal` function ends, the `main` function calls the `getChoice` function once again. If the choice contains the number 3, the program ends. If the `choice` variable contains a value other than 1, 2, or 3, the `main` function simply calls the `getChoice` function.

604
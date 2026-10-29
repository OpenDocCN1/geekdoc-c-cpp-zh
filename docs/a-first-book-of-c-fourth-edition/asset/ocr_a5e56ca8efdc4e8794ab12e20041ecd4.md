Following is a sample output produced by Program 14.19:

```
Enter an integer value: abc
Invalid integer - Please reenter: 12.
Invalid integer - Please reenter: 12e
Invalid integer - Please reenter: 120
The integer entered is: 120
```

As this output shows, the getInt() function works correctly. It requests input continuously until a valid integer is entered.

# EXERCISES 14.5

+   1. **(Practice)** Write a C++ program that prompts the user to enter an integer. Have your program use cin to accept the number as an integer and use cout to display the value your program actually accepted from the data entered. Run your program four times. The first time you run the program, enter a valid integer number; the second time, enter a double-precision number; the third time, enter a character; and the fourth time, enter the value 12e34.
+   
+   2. **(Modify)** Modify the program you wrote for Exercise 1 to prompt for and accept a double-precision number. Run the program four times: First, enter an integer; second, enter a decimal number; third, enter a decimal number with an “f” as the last character entered; and fourth, enter a character. Using the output display, keep track of the number your program actually accepted from the data you entered. What happened, if anything, and why?
+   
+   3. **(For thought)**
+      a. Why do you think successful application programs contain extensive data input validity checks? *(Hint: Review Exercises 1 and 2.)*
+      b. What do you think the difference is between a data-type check and a data-reasonableness check?
+      c. A program requests that the user enter a month, day, and year. What are some reasonable checks that could be made on the data entered?
+   
+   4. **(Practice)**
+      a. Enter and run Program 14.18.
+      b. Run Program 14.18 four times, using the data listed in Exercise 1 for each run.
+   
+   5. **(Modify)** Modify Program 14.18 to display any invalid characters that were entered.
+   
+   6. **(Modify)** Modify Program 14.18 to request an integer continuously until a valid number is entered.
+   
+   7. **(Modify)** Modify Program 14.18 to remove all leading and trailing spaces from the entered string before it’s checked for validity.
+   
+   8. **(Useful activity)** Write a function that checks each digit as it’s entered, instead of checking the completed string, as in Program 14.18.
+   
+   9. **(Practice)** Enter and run Program 14.19.
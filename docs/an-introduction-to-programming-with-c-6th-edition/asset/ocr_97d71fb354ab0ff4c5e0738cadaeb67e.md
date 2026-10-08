15. As you learned in the chapter, you must be careful when comparing two real numbers for either equality or inequality, because some real numbers cannot be stored precisely in memory. To determine whether two real numbers are equal or unequal, you must test that the difference between numbers is less than some acceptable small value, such as .0001.

+   a. Follow the instructions for C++ and opening the Advanced15.cpp file. Notice that the code divides the contents of the num1 variable (10.0) by the contents of the num2 variable (3.0), storing (approximately 3.33333) in the quotient variable. An if statement is used to compare the contents of the quotient variable with the number 3.33333. The if statement displays a message that indicates whether the numbers are equal.
b. If necessary, make the system("pause") statement a comment, and save the program. Run the program. Even though the message on the screen states that the quotient is 3.33333, the message indicates that this value is not equal to 3.33333. Stop the program.

+   c. If you need to compare two real numbers for equality or inequality, first find the difference between both numbers and compare the absolute value of that to a small number, such as .0001. You can use the C++ fabs function to find the absolute value of a number. The absolute value of a number is a positive number that represents the distance the number is from 0 on the number line. For example, the absolute value of the number 5 -5 is also 5. To use the fabs function, the program must contain the #include <cmath> directive. Modify the program appropriately. Save and then run the program. Time, the message says "Yes, the quotient 3.33333 is equal to 3.33333". Stop the program.

16. Follow the instructions for C++ and opening the SwatTheBugs16.cpp file. If necessary, make the system("pause") a comment, and save the program. Run and then debug the program.

# Answers to TRY THIS Exercises

# Pencil and Paper

+   1. See Figure 5-38.

```
if (quantity == 10)
    cout << "Equal" << endl;
else
    cout << "Not equal" << endl;
//end if
```

Figure 5-38

# Step 5—Desk-check the Program

is the cout << "Enter the bill: " statement. The statement displays a prompt on the computer screen; it does not make any changes to the variables; therefore, no entry is necessary in the desk-check table. The next statement, cin >> totalBill11; allows the user to enter the total bill, and stores the user's response in the totalBill11 variable. If the user enters the number 45, the statement stores 45.0 in the variable, which is the double type. Then record 45 in the totalBill11 column in the desk-check table. As you learned in Chapter 2, programmers help it to lightly cross the previous value in a column before recording a new value; this is not a requirement. Next, the cout << "Enter the liquor charge:" statement prompts the user to enter the liquor charge. The cin >> liquor; statement waits and stores the response in the liquor variable. If the user enters the number 10, the desk-check table shows 10. The cout << "Enter the tip percentage in decimal format:" statement prompts the user to enter the percentage. cin >> tipPercent; stores the response in the tipPercent variable. If the user enters the number 2, record 2 in the desk-check table. Figure 4-15 shows the input values recorded in the program's desk-check table.

| totalBill | liquor | percent | totalNoLiquor | tip |
| :--- | :--- | :--- | :--- | :--- |
| 45.0 | 10.0 | 2 | 0.0 | 0.0 |

Figure 4-15 Input values in the program's desk-check table

The totalNoLiquor = totalBill - liquor; statement subtracts the contents of the liquor (10.0) from the contents of the totalBill11 (45.0) and stores the result (35.0) in the totalNoLiquor variable. Notice that the expression appearing on the right side of the assignment operator is evaluated, and then the result is stored in the variable whose name on the left side of the assignment operator. As a result of this statement, record 35.0 in the totalNoLiquor column in the desk-check table, as shown in Figure 4-16.

| totalBill | liquor | tipPercent | totalNoLiquor | tip |
| :--- | :--- | :--- | :--- | :--- |
| 45.0 | 10.0 | 2 | 35.0 | 0.0 |

Figure 4-16 Desk-check showing the result of the total bill without liquor charge calculation

The next statement, tip = totalNoLiquor * tipPercent; multiplies the contents of the totalNoLiquor variable (35.0) by the contents of the tipPercent variable (2) and stores the result (7.0) in the tip variable. In the desk-check table, you record the number 7.0 in the tip column, as shown in Figure 4-17.

# CHAPTER 4 Completing the Problem-Solving Process

| totalBill | liquor | tipPercent | totalNoLiquor | tip |
| --- | --- | --- | --- | --- |
| $ | $ | $ | $ | $ |
| 45.0 | 10.0 | 2 | 35.0 | 7.0 |

**Figure 4-17** Desk-check table showing the result of the tip calculation

The last statement in the program shown in Figure 4-12 displays the "Tip: $%s" message along with the contents of the tip variable on the screen. You have now completed desk-checking the program using the set of data. If you compare the row of values shown in Figure 4-13, you will notice that the results obtained when desk-checking the program are the same as the results obtained when desk-checking the algorithm. Recall, that you should perform several desk-checks (using different data) to make sure that the program works correctly. For the second desk-check, you will use 30.0, and .15 as the total bill, liquor charge, and tip percentage, respectively. This same data used in desk-check shown in Figure 4-13. Each time you check a program, keep in mind that you must complete all of the program's statements, beginning with the first statement and ending with the last statement. In this case, the first statement declares and initializes the totalBill11 variable, and the last statement displays the tip amount on the screen. The completed desk-check table is shown in Figure 4-18. Again, if you compare the fourth row of values in Figure 4-18 with the second row of values shown in Figure 4-13, you will notice that the program's results are the same as the algorithm's results.

| totalBill | liquor | tipPercent | totalNoLiquor | tip |
| --- | --- | --- | --- | --- |
| $ | $ | $ | $ | $ |
| 45.0 | 10.0 | | 35.0 | 7.0 |
| $ | $ | $ | $ | $ |
| 30.0 | 0.0 | 15 | 30.0 | 15.00 |

**Figure 4-18** Program's desk-check table showing the results of the desk-check

# Step 6—Evaluate and Modify the Program

The final step in the problem-solving process is to evaluate and modify (if necessary) the program. You evaluate a program by entering your C++ instructions (along with other instructions that you will learn about in this section) into the computer and then using the computer to run (execute) the program. While the program is running, you enter the sample data used when desk-checking the program. If the results obtained when running the program differ from those in the program's desk-check it indicates that the program contains errors, referred to as bugs. The bugs must be located and removed from the program before the program is released to the user. The programmer's job is not finished until the program runs without errors and produces the expected results.

The process of locating the bugs in a program is called debugging. Program bugs typically are caused by syntax errors or logic errors. A syntax error occurs when you break one of the programming language-rules. As learned in Chapter 3, programming language has a set of rules, called syntax, that you must follow when using the language. Most syntax errors are a type of errors occurring when entering instructions, such as ending (instead of endl) or entering a semicolon at the end of a statement. In most cases, syntax errors are easy to both locate and correct because they trigger an error message from the C++ compiler. The error message includes a description of the error and Unlike syntax errors, logic errors are much more difficult to find, they do not trigger an error message from the compiler. A logic error can occur for a variety of reasons, such as forgetting to enter an instruction or the instructions in the wrong order. result of calculation statements are correct but incorrect mathematically. For example, consider the statement average = number1 + number2 / 2 ; which is supposed to calculate the average of two numbers. The statement's syntax is correct, but it is incorrect mathematically. This is because it tells the computer to divide the contents of the number variable by 2 and then add the quotient to the contents of the number variable. (Recall that division is performed before addition in an arithmetic expression.) The correct instruction for calculating the average of two numbers is average=(number1 + number2)/2 ; The parenthesis then adds the quotient to the number1 variable before dividing the sum by 2.

In order to enter your C++ instructions into the computer, you need to have access to a text editor, more simply referred to as an editor. The instructions you enter are called source code. You save the source code in a file on a disk, giving it the file extension .cpp (which stands for C plus plus). The .cpp file is called source file. In order to run (execute) the code in the source file, you need a C++ compiler. As compiler translates high-level instructions into machine code—the Os and is the computer that generates machine code. The compiler generates the object code and saves it in a file with extension .obj (which stands for object). The file containing the object code is called the object file. After the compiler creates the object file, it invokes another program called the linker. The linker combines the object file with other machine code necessary for your C++ program to run correctly as a machine that allows the program to communicate with input and output devices. The linker produces an executable file, which is a file that contains all of the machine code necessary to run your C++ program as many times as desired without the need for translating the program again. The executable file has an extension of .exe on its filename. (The exe stands for executable.) Figure 4-19 illustrates the sequence of steps followed when translating your source code into executable code.

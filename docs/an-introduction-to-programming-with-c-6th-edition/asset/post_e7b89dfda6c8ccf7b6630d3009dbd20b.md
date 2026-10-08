
# CHAPTER 8 More on the Repetition Structure

| 1 | 1 | 1 | 1 |
| 2 | 4 | 8 | 16 | 32 | 64 |
| 3 | 9 | 27 | 81 | 243 | 729 |
| 4 | 16 | 64 | 256 | 1024 | 4096 |

Figure 8-43

10. Rewrite the code from Pencil and Paper Exercise 9 to use two while statements.

11. Rewrite the code from Pencil and Paper Exercise 9 to use two do while statements.

12. Rewrite the code from Pencil and Paper Exercise 9 to use a while statement in the outer loop.

13. Rewrite the code from Pencil and Paper Exercise 9 to use the do while statement in the nested loop.

14. The code in Figure 8-44 should display three rows of asterisks on the computer screen. The first row should contain one asterisk. The second row should contain two asterisks, and the third row should contain three asterisks. However, the code is not working correctly; it displays three asterisks on one of the three rows. Debug the code.

```cpp
for (int row = 1; row < 4; row += 1) {
    for (int asterisks = 1; asterisks <= 3; asterisks += 1) {
        cout << '*';
    } //end for
    cout << endl;
} //end for
```

Figure 8-44

## Computer

15. In this exercise, you create a program that uses two for statements to display the pattern of asterisks shown in Figure 8-45. If necessary, create a new project TryThis15 Project. Enter the C++ instructions into a source file named TryThis15.cpp. Also enter appropriate comments and any additional instructions required by the compiler. Save and then run the program. (The answers to TRY THIS Exercises are located at the end of the chapter.)

![](img/d64a28a68f49d61137bf2f3170ac40ad_322_0.png)

Figure 8-45

16. In this exercise, you create a program that uses two while statements to display the pattern of asterisks shown in Figure 8-46. If necessary, create a new project TryThis16 Project. Enter the C++ instructions into a source file named TryThis16.cpp. Also enter appropriate comments and any additional instructions required by the compiler. Save and then run the program. (The answers to TRY THIS Exercises are located at the end of the chapter).

```
******
*****
****
***
**
*

*
```

Figure 8-46

17. In this exercise, you modify the code from Computer Exercise 16. If necessary, create a new project ModifyThis17 Project. Enter (or copy) the TryThis16.cpp instructions into a source file named ModifyThis17.cpp. Change TryThis16.cpp in the first comment to ModifyThis17.cpp. Replace the two while statements with for statements and then run the program.

18. The savings calculator program is shown in Figure 8-29 in the chapter. If necessary, create a new project Introductory18 Project. Enter the C++ instructions from the figure into a source file named Introductory18.cpp. Change the filename in the first comment. Save and then run the program. The output is shown in Figure 8-30 in the chapter. Replace the do while statement with a for statement, and save and run the program.

19. The modified savings calculator program is shown in Figure 8-32 in the chapter. If necessary, create a new project Introductory19 Project. Enter the C++ instructions from the figure into a source file named Introductory19.cpp. Change the filename in the first comment. Save and then run the program. The output is shown in Figure 8-33 in the chapter. Replace the for statement with a while statement, and save and run the program.

20. In this exercise, you modify the code from Lab 8-2. If necessary, create a new project Intermediate20 Project. Enter (or copy) the C++ instructions from the Lab8-2.cpp into a source file named Intermediate20.cpp. Change the filename in the first comment. Replace both loops with posttest loops. Save and then run the program.

21. The modified savings calculator program is shown in Figure 8-32 in the chapter. If necessary, create a new project Intermediate21 Project. Enter the C++ instructions from the figure into a source file named Intermediate21.cpp. Modify the program to allow the user to enter the principal. Use a sentinel value to end the program. Save and run the program. Test the program using the following principals, followed by your sentinel value: 1000, 3000, and 10000.

# CHAPTER 8 More on the Repetition Structure

- 22. Write the code to display a table consisting of four rows and 11 columns. The first column should contain the numbers 1 through 4. The second and subsequent columns should contain the result of multiplying the number in the first column by 0 through 9. The table will look similar to the one shown in Figure 8-47. (Don't be concerned about the alignment of the numbers in each column.) Use two for statements. If necessary, create a new project named Intermediate22 Project. Enter your C++ instructions into a source file named Intermediate22.cpp. Also enter appropriate comments and any additional instructions required by the compiler. Save and run the program.

INTERMEDIATE

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 | 18 |
| 2 | 0 | 3 | 6 | 9 | 12 | 15 | 18 | 21 | 24 | 27 |
| 3 | 0 | 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 |

Figure 8-47

INTERMEDIATE

- 23. The payroll manager at Kenton wants a program that allows him to enter an unknown number of payroll amounts for three stores: Store 1, Store 2, and Store 3.
  - a. Create an IPO chart for the problem, using 30000 and 15000 for Store 1; 20000 and 16000 for Store 2; and 40000 and 12000 for Store 3.
  - b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown earlier. Then code the algorithm into a program.
  - c. Desk-check the program using the same data.
  - d. If necessary, create a new project named Intermediate23 Project. Enter your C++ instructions into a source file named Intermediate23.cpp. Also enter appropriate comments and any additional instructions required by the compiler.
  - e. Save and run the program. Test the program using the same data.

- 24. In this exercise, you modify the code from Lab 7-2. If necessary, create a new project named Intermediate24 Project. Copy the instructions from the Lab7-2.cpp into a source file named Intermediate24.cpp. Change the filename in the first comment. Modify the program to display student's total points and grade.

- 25. At the beginning of every year, Khalid receives a raise on his salary. He wants a program that calculates and displays the amount of his salary for the next three years, using rates of 3%, 4%, and 5%.
  - a. Create an IPO chart for the problem, using salaries of $30000 and $50000.
  - b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown in Exercise 8-38. Then code the algorithm into a program.
  - c. Desk-check the program using the same data.
  - d. If necessary, create a new project named Advanced25. Enter the C++ instructions into a source file named Advanced25.cpp. Also enter appropriate comments and any additional instructions required by the compiler.
  - e. Save and run the program. Test the program using the same data.

- 26. In this exercise, you modify the code from Computer Exercise 15. The modified program will allow the user to specify the loop ending value and its increment value. The ending value determines the maximum number of asterisks to display. The increment value determines the number of asterisks to repeat.
  - a. If necessary, create a new project named Advanced26. Enter (or copy) the TryThis15.cpp instructions into a source file named Advanced26.cpp. Change TryThis15.cpp in the first comment to Advanced26.cpp. Make the appropriate modifications to the program.
  - b. Save and run the program. Test the program by entering the numbers 4 and 1 as the maximum number of asterisks and increment value, respectively. The program should display four rows of asterisks as follows: one asterisk, two asterisks, three asterisks, and four asterisks.
  - c. Run the program. This time, enter the numbers 9 and 3 as the maximum number of asterisks and increment value, respectively. The program should display three rows of asterisks as follows: three asterisks, six asterisks, and nine asterisks.

- 27. In this exercise, you modify the code from Computer Exercise 16. The modified program will allow the user to display the asterisks using two different patterns. Pattern 1 contains nine rows of asterisks as follows: nine asterisks, eight asterisks, seven asterisks, six asterisks, five asterisks, four asterisks, three asterisks, two asterisks, one asterisk.

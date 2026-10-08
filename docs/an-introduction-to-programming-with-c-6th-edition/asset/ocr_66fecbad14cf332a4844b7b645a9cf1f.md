# The Area Calculator Program

| main function's variables | | getRectangleArea function's variables |
|---|---|---|
| length width area | len wid |
| 6.0 10.0 0.0 | 5.0 10.0 |

Figure 9-25 Desk-check table after the getRectangleArea function header is processed

Next, the computer processes the return len * wid; statement on Line 31 in the getRectangleArea function statement. The statement multiplies the len value by the wid's value and returns the result to the statement that called the getRectangleArea function. In this case, it returns the double 70 to the assignment on Line 21 in the main function. The statement assigns the double number to the area variable. After the return statement the function ends and the computer removes the len and wid variables from its internal memory. Figure 9-26 shows the desk-check table at this point in the program. Notice that only the main function's variables are still in the computer's internal memory.

| main function's variables | getRectangleArea function's variables no longer exist in the computer's internal memory |
|---|---|
| length width area | len wid |
| 6.0 10.0 0.0 | 5.0 10.0 |

Figure 9-26 Desk-check table after the getRectangleArea function ends

Next, the computer processes the cout statement on Line 22. The statement displays the contents of the area variable on the screen. The computer processes the system("pause"); and return 0; statements next. The system("pause") statement pauses execution, and the return 0; statement returns the number 0 to the operating system to indicate that the program ended normally. After the return 0; statement is processed, the main function ends and removes the length, width, and area variables from its internal memory. You may be wondering why the program needs to pass the contents of the length and width variables to the getRectangleArea function. Why can't the function use both in its return statement, like the return len * wid?; You might also be wondering why the computer removes the len and wid variables from memory after the getRectangleArea function ends, waits until the main function ends before it removes the length, width, and area variables. Why are the variables removed at different times and? To answer these questions, you will need to learn about the scope and lifetime of a variable. The scope and lifetime of a variable are the last topics covered in this chapter.
# CHAPTER 11

# One-Dimensional Arrays

If you already understand the bubble sort program's code, you can skip the remainder of this section and continue with the section titled Parallel One-Dimensional Arrays, which begins on Page 461.

To help you understand the bubble sort, you will desk-check the program shown in Figure 11-41. (However, refer to the TIP on this page.) The statements on Lines 11 through 16 create and initialize the arrays and five variables. Figure 11-42 shows the desk-check table after these statements are processed.

| numbers[0] | numbers[1] | numbers[2] | numbers[3] |
| :--- | :--- | :--- | :--- |
| 23 | 46 | 12 | 35 |
| sub | temp | maxSub | swap |
| 0 | 0 | 3 | Y |

Figure 11-42 Desk-check table after the declaration statements on Lines 11 through 16 are processed

The condition in the while clause on Line 19 compares the contents of the swap variable with the letter Y. The condition evaluates to true; therefore, the computer processes the instructions in the body of the loop. For two instructions on Lines 21 and 23. The instructions assign the letter N to swap variable and assign the number 0 to the sub variable. The while clause on Line 28 begins a nested loop that repeats its instructions as long as the value stored in the sub variable is less than the value stored in maxSub. At this point, the sub variable contains the number 3; therefore, the computer processes the instructions in the nested loop. The condition if (sub > numbers[0] ) evaluates to true on Line 30 determines whether the value stored in the numbers[0] is greater than the value stored in the numbers[1] variable. The condition evaluates to false, because the numbers[0] variable contains the number 23 and the numbers[1] variable contains the number 46. As a result, the instructions in the if statement's true path are skipped over and continuing with the sub += 1; statement on Line 39. The statement adds the number 1 to the contents of the sub variable, giving 1. Figure 11-43 shows the desk-check table after the nested loop instructions are processed first. The new values in the table are shaded in the figure.

| numbers[0] | numbers[1] | numbers[2] | numbers[3] |
| :--- | :--- | :--- | :--- |
| 23 | 46 | 12 | 35 |
| sub | temp | maxSub | swap |
| 0 | 0 | 3 | Y |

Figure 11-43 Desk-check table after the nested loop is processed the first time

Next, the computer evaluates the condition in the while (sub < Sub) clause on Line 28. The condition evaluates to true, because the sub variable's value (1) is less than the maxSub variable's value (3). As a result,
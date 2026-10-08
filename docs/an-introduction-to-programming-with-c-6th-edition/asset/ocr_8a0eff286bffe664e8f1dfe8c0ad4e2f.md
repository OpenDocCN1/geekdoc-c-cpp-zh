# CHAPTER 11 One-Dimensional Arrays

Lines 14 through 19. The sub variable will remain in memory until the for loop ends. Figure 11-11 shows the desk-table after the initialization argument on Line 14 has been processed.

| sales array variables | local to the for loop on Lines 14 through 19 |
|---|---|
| sales[0] sales[1] sales[2] sales[3] | sub |
| 0.0 0.0 0.0 0.0 | 0 |

Figure 11-11 Desk-table after the initialization argument on Line 14 is processed

The for clause condition argument tells the computer to check whether the value stored in the sub variable is less than 4. It is, the statements in the body of the for loop are processed. First, the cout statements on Lines 16 and Region 1, prompt the user to enter the values for the current region—in this case. Note that the current region is determined by adding the number to the value stored in the sub variable (0). This is unless, unlike the array subscript, the number goes from 1 to 4 rather than 0 through 3. The region number will always be more number than the subscript of its corresponding element in the array. In other words, Region 1's sales will be stored in the element whose subscript is 0. Likewise, Region 2's sales will be stored in the element whose subscript is 1, and the cin statement on Line 18 gets Region 1's sales from the user and stores the amount in the first element (sales[0]). 123.67 is entered in the array.

> As you learned in Chapter 7, the condition argument in a for clause is loop condition, because it specifies the requirement for processing loop instructions.

| sales[0] sales[1] sales[2] sales[3] sub |
|---|---|---|---|---|
| 0.0 0.0 0.0 0.0 | |
| 123.67 | | | |

Figure 11-12 Desk-table after Region 1's sales are entered in the array

The for contents update argument tells the computer to add the number 1 to the contents of the sub variable; the result is 1. The computer checks whether the sub variable's value is less than 4. It is, so the statements in the body of the for loop are processed again. cout statements prompt the user to enter the values for Region 2, and the cin statement stores the user's response in the second element (sales[1]). Figure 11-13 shows the sales for Region 2 (350.89) entered in the array.

| sales[0] sales[1] sales[2] sales[3] sub |
|---|---|---|---|---|
| 0.0 0.0 0.0 0.0 | |
| 123.67 350.89 | | | 1 |

Figure 11-13 Desk-table after Region 2's sales are entered in the array

Next, the computer updates the sub variable by adding the number 1 to it; the result is 2. The computer checks whether the sub variable's value is less than 4. It is, so the statements in the body of the for loop are processed
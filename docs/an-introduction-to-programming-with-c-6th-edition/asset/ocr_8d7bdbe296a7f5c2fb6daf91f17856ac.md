# CHAPTER 11 One-Dimensional Arrays

Next, the computer processes the x += 1; statement on Line 60. The increases the value in the x variable by 1, giving 4. The condition in the while clause on Line 55 checks whether the x variable is less than the number of elements stored in the numElements variable. It is, so the statement compares the value in the numbers[4] element with the value stored in the high variable. The value in the numbers[4] element (34) is not greater than the value in the high variable (84), so if the statement ends and the computer processes the x += 1; statement on Line 60. The while clause's condition increases the value in the x variable by 1, giving 5. Next than the value stored in the numElements variable. It's not, so the while loop ends and the computer processes the return statement on Line 63. The statement returns the value stored in the high variable to the getHighest function. The statement appears on Lines 30 and 31. After the getHighest function returns, the computer removes the names from each element in the array. It also removes numElements, high, and x from memory. The completed desk-table is shown in Figure 11-39.

| numbers[0] | numbers[1] | numbers[2] | numbers[3] | numbers[4] |
| --- | --- | --- | --- | --- |
| randNums[0] | randNums[1] | randNums[2] | randNums[3] | randNums[4] |
| 35 | 8 | 8 | 84 | 34 |

| removed from memory after the for loop in the main function ends | removed from memory when the displayArray function ends | removed from memory after the for loop in the displayArray function ends | removed from memory when the getHighest function ends |
| --- | --- | --- | --- |
| sub | numElements | sub | numElements | high |
| 6 | | 5 | 85 | |
| | | | 84 | 3 |
| 4 | | 5 | |

Figure 11-39 Completed desk-table for the random numbers program

The cost on Lines 30 and 31 in the main function displays the value returned by the getHighest function. The computer processes the system("pause"); and return 0; statements before the program ends. When the program ends, the computer removes the randNums array from memory.
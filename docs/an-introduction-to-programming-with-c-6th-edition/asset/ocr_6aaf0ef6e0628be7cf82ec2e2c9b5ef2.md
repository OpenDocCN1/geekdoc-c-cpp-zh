# Sorting the Data St in a One-Dimensional Array

the nested loop instructions are processed again. In the `if (numbers[sub] > numbers[sub + 1])` clause on Line 30 determines whether the value stored in `numbers[1]` is greater than the value stored in `numbers[2]` variable. In this case, the condition evaluates to true, because the `numbers[1]` contains the number 46 and the `numbers[2]` contains the number 12. Because of this, the instructions in the `if` statement's true path are processed on Lines 33 through 37. The first three instructions in the true path swap the values stored in `numbers[1]` and `numbers[2]` variables. The fourth instruction, `swap = 'Y';`, indicates that a swap was made. The last instruction in the true path, `lastSwap = swap;`, swaps the value stored in the `sub` variable—in this case, the number 1 to the `lastSwap` variable, which keeps track of the position of the last array. Next, the `sub += 1;` statement on Line 39 adds the number 1 to the contents of the `sub` variable; the result is 2. Figure 11-44 shows the desk-check table after the nested loop instructions are processed the second time. The new values are shaded in the figure.

| numbers[0] | numbers[1] | numbers[2] | numbers[3] |
|---|---|---|--|
| 23 | 42 | 46 | 35 |
| sub | | maxSub | lastSwap |
| 6 | | 3 | 6 |
| 6 | | 1 | Y |
| 7 | | | Z |

Figure 11-44 Desk-check table evaluates the condition after the nested loop is processed the second time

Next, the computer evaluates the condition to true, because the `while (sub < maxSub)` clause on Line 28. The condition evaluates the `sub` variable's value (2) is less than the `maxSub` variable's value (3). Therefore, the computer once again processes the instructions in the nested loop. The condition in the `if (numbers[sub] > numbers[sub + 1])` clause on Line 30 determines whether the value stored in the `numbers[2]` variable is greater than the value stored in the `numbers[3]` variable. The condition evaluates to true, because the `numbers[2]` variable contains the number 46 and the `numbers[3]` variable contains the number 35. As result, the computer processes the instructions in the `if` statement's true path. The first three instructions in the true path swap the values in the `numbers[2]` and `numbers[3]` variables. The fourth instruction in the true path indicates that a swap was made. The last instruction in the true path swaps the value stored in the `sub` variable (2) to the `lastSwap`. Next, the `sub += 1;` statement on Line 39 adds the number 1 to the contents of the `sub` variable; the result is 3. Figure 11-45 shows the desk-check table after the nested loop instructions are processed the third time. The new values in the table are shaded in the figure.

457
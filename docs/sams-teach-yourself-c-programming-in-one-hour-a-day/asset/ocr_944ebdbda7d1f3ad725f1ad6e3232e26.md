# Syntax

# 135

```
24:    array[ctr] = nbr;
25:    ctr++;
26:    }
27:
28:    for (ctr = 0; ctr < 5; ctr++)
29:        printf("Value %d is %d\n", ctr + 1, array[ctr] );
30:
31:    return 0;
32: }
```

# Output ▼

This program prompts you to enter 5 numbers
Each number should be from 1 to 10

Enter number 1 of 5: **3**

Enter number 2 of 5: **6**

Enter number 3 of 5: **3**

Enter number 4 of 5: **9**

Enter number 5 of 5: **2**

Value 1 is 3
Value 2 is 6
Value 3 is 3
Value 4 is 9
Value 5 is 2

# Analysis ▼

As in listings, line 1 contains a comment with a description of the program, and line 3 contains an #include statement for the standard input/output header file. Line 5 contains a declaration for an array (named array) that can hold five integer values. The function main() contains two additional local variables, ctr and nbr (lines 9 and 10). Notice that these variables are initialized to zero at the same time they are declared. Also notice that the comma operator is used as a separator at the end of line 9, allowing nbr to be declared as an int without restarting the int type command. Stating statements in this manner is a common practice for many C programmers. Lines 12 and 13 print messages stating what the program does and what is expected of the user. Lines 15 through 26 contain the first while command and its statements. Lines 18 through 22 contain a nested while loop with its own statements that are all part of the outer while.
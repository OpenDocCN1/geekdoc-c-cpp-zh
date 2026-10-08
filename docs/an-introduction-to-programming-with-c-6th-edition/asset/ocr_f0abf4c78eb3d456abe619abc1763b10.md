# Arithmetic Assignment Operators

| IPO chart information | C++ instructions |
| --- | --- |
| Input | int hours = 0; |
| hours enrolled | const int FEE_PER_HOUR = 100; |
| fee per hour (100) | const int ROOM_BOARD = 2000; |
| room & board fee (2000) | |

Processing

none

Output

total owed

int totalOwed = 0;

Algorithm

+   1. enter the hours enrolled
2. calculate the total owed by multiplying the hours enrolled by the fee per hour and adding the room board fee to the result
3. display the total owed

```
cout << "Hours enrolled: \;
cin >> hours;
totalOwed = hours * FEE_PER_HOUR +
ROOM_BOARD;
```

```
cout << "Total owed: " <<
totalOwed << endl;
```

Figure 4-28 IPO chart information and C++ instructions for the Hoover College problem

The fifth step in the problem-solving process is to desk-check. You begin by making the declared variables and named constants in a desk-check table, with their values. You desk-check the remaining C++ instructions in order, recording in the desk-check table any changes made to the variables. 4-29 shows the desk-check table for the program. The results agree with those shown in the algorithm's desk-check table for Figure 4-27.

| hours | FEE_PER_HOUR | ROOM_BOARD | totalOwed |
| --- | --- | --- | --- |
| 6 | 100 | 2000 | 6 |
| 9 | 100 | 2000 | 2300 |
| 6 | 100 | 2000 | 6 |
| 11 | 100 | 2000 | 3100 |

Figure 4-29 Completed desk-check table for the Hoover College program

The final step in the problem-solving process is to evaluate and modify (if necessary) the program. Recall that you evaluate a program by entering its instructions into the compiler and using the computer to run (execute) it. While the program is running, you enter the same data used when desk-checking the program. The method of entering the instructions and running the program on the C++ IDE you are using; or if you are not using an IDE, depends on your compiler and editor text. As mentioned earlier, Appendices D and E show you how to enter and run programs using Microsoft Visual C++ 2010 and Dev C++, respectively. However, you can enter and run the programs in this book using most C++ systems, with other
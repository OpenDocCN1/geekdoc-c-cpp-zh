all of the instructions within the loop need to be repeated the same number of times: Figure 8-14 shows the completed desk-check table, and Figure 8-15 shows a sample run of the program.

| Problem specification
Create a program that displays an asterisk on three separate lines on the computer screen, like this:
*
\*

| IPO chart information | C++ instructions |
| Input | |
| none | |
| Processing | this variable is created and initialized in the for clause |
| number of lines (counter: 1 to 3) | |
| Output | |
| asterisk (on each of 3 lines) | |
| Algorithm | |
| repeat (number of lines is less than 4) | for (int line = 1; line < 4; line += 1) {
| display asterisk | cout << '*';
| position the cursor on the next line | cout << endl;
| repeat | } // for end

![](bbox=[0.313, 0.597, 0.862, 0.715])

|  | |
| --- | |
| - | |
| - | |
| - | |
| - | |

Figure 8-14 Completed desk-check table for the asterisks program
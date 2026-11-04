Let’s consider two attributes rows and columns of a 2-dimensional pattern as variables;

+   - **row** → variable <i>type_of_integer</i> to store integer value one at a time and represents row number between 1 and 9.
+   - **col** → variable <i>type_of_integer</i> to store integer value one at a time and represents column number between 1 and 9.
+   - **spaces** → variable <i>type_of_integer</i> to store integer value one at a time and represents space character at column number between 1 and 5.
+   - **totalRows** → variable <i>type_of_integer</i> to store integer value for total number of rows <i>which is 5 by default</i>.

(row, col) value pair depicts the position of “*” character on the display screen

| | | | | | | | | |
|---|---|---|---|---|---|---|---|---|
| | | | | row=1,<br>col=5 | | | | |
| | | | row=2,<br>col=4 | row=2,<br>col=5 | row=2,<br>col=6 | | | |
| | | row=3,<br>col=3 | row=3,<br>col=4 | row=3,<br>col=5 | row=3,<br>col=6 | row=3,<br>col=7 | | |
| | row=4,<br>col=2 | row=4,<br>col=3 | row=4,<br>col=4 | row=4,<br>col=5 | row=4,<br>col=6 | row=4,<br>col=7 | row=4,<br>col=8 | |
| row=5,<br>col=1 | row=5,<br>col=2 | row=5,<br>col=3 | row=5,<br>col=4 | row=5,<br>col=5 | row=5,<br>col=6 | row=5,<br>col=7 | row=5,<br>col=8 | row=5,<br>col=9 |
| | row=6,<br>col=2 | row=6,<br>col=3 | row=6,<br>col=4 | row=6,<br>col=5 | row=6,<br>col=6 | row=6,<br>col=7 | row=6,<br>col=8 | |
| | | row=7,<br>col=3 | row=7,<br>col=4 | row=7,<br>col=5 | row=7,<br>col=6 | row=7,<br>col=7 | | |
| | | | row=8,<br>col=4 | row=8,<br>col=5 | row=8,<br>col=6 | | | |
| | | | | row=9,<br>col=5 | | | | |

The real challenge is to find the correct (row, col) positions and to print required character on the computer screen by writing a program. This will be carried out by applying <i>for-loop</i> in combination with appropriate logical conditions. Finding logical conditions in a step-by-step approach stimulates the growth for algorithmic thinking, a fundamental requirement to become a confident programmer. For this logic pattern, we can give (row, column) numeric value pairs as shown in the above table structure. It is quite easy to locate these (row, col) positions manually in the table structure. It is that much equally challenging to find logical conditions. The learner should be able to output this logic pattern in different sizes based on different input values of total number of rows. With all these understandings, we will learn in a systematic way to explore the logic of program.
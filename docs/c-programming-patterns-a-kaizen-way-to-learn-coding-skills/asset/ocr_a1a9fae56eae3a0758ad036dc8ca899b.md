# Pattern1E

Our programming job is to output this pattern on a part of the computer screen as shown in the following. We can consider the computer screen as a combination of (row, column) numeric value paired boxes which are spread all over the screen. Each box is treated as a resident of just a single character only.

![](bbox=[0.12, 0.27, 0.45, 0.6])

![](bbox=[0.55, 0.27, 0.9, 0.6])

# Analysis of output

We that the complete pattern can be easily expressed as a collection of selected (row, column) numeric value pairs. The selection of (row number, column number) numeric pairs will be based on the keyboard characters used to design the given pattern. With this numeric pair number scheme we can correctly able to locate a particular keyboard character on the computer screen. The first value in any selected numeric pair represents the row number and second value represents a column number. For example;

(2, 4) means character "*" at second row and fourth column in the table.

| | Col=1 | Col=2 | Col=3 | Col=4 | Col=5 | Col=6 | Col=7 | Col=8 | Col=9 |
|---|---|---|---|---|---|---|---|---|---|
| Row=1 | space | space | space | space | *(1,5) | space | space | space | space |
| Row=2 | space | space | space | *(2,4) | *(2,5) | *(2,6) | space | space | space |
| Row=3 | space | space | *(3,3) | *(3,4) | *(3,5) | *(3,6) | *(3,7) | space | space |
| Row=4 | space | *(4,2) | *(4,3) | *(4,4) | *(4,5) | *(4,6) | *(4,7) | *(4,8) | space |
| Row=5 | *(5,1) | *(5,2) | *(5,3) | *(5,4) | *(5,5) | *(5,6) | *(5,7) | *(5,8) | *(5,9) |

Space → space is also a character like any other character. If a non-space character or a text is displayed on the screen after a blank area or gap, it means that many space character has to be print before printing any other non-space character(s) afterwards.
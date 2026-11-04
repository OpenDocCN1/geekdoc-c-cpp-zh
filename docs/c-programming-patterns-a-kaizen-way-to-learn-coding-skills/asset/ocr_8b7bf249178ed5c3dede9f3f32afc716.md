# Pattern1D

Our programming job is to output this simple picture-based pattern on a part of the computer screen as shown in the following. Our approach will be considering computer screen as a combination of rows and columns containing small boxes. We can consider the computer screen as a combination of **(row, column)** numeric value paired boxes which are spread all over the screen. Each box is treated as a resident of just a single character only. We also know that the complete pattern can be easily expressed as a collection of **selected (row, column)** numeric value pairs.

![](bbox=[0.08, 0.31, 0.48, 0.55])

![](bbox=[0.52, 0.31, 0.92, 0.55])

# Analysis of output

We can represent computer screen in terms of rows and columns. In order to know the placement of each "*" character and space " " character on the display screen, we can give each box a numeric representation in terms of row number and a column number.

The **(row number, column number)** numeric pair can be used to represent a pattern. The first value represents the row number and second value represents a column number. For example;

> (2, 4) means character "*" at **second row** and **fourth column** in the table.

| | Col=1 | Col=2 | Col=3 | Col=4 | Col=5 |
|---|---|---|---|---|---|
| Row=1 | *(1,1) | *(1,2) | *(1,3) | *(1,4) | *(1,5) |
| Row=2 | space | *(2,2) | *(2,3) | ***(2,4)*** | *(2,5) |
| Row=3 | space | space | *(3,3) | *(3,4) | *(3,5) |
| Row=4 | space | space | space | *(4,4) | *(4,5) |
| Row=5 | space | space | space | space | *(5,5) |

> **Space → space is also a character like any other character. If a non-space character or a text is displayed on the screen after a blank area or gap, it means that many space character has to be print before printing any other non-space character(s) afterwards.**
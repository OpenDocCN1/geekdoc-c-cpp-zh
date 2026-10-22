b.
int * ptr;
int fort[2][2] = { {12}, {14,16} };
ptr = fort[0];

# 5. What is the value of **ptr and of **(ptr + 1) in each case?

a.
int (*ptr)[2];
int torf[2][2] = {12, 14, 16};
ptr = torf;

b.
int (*ptr)[2];
int fort[2][2] = { {12}, {14,16} };
ptr = fort;

# 6. Suppose you have the following declaration:
int grid[30][100];

+   a. Express the address of grid[22][56] one way.
+   b. Express the address of grid[22][0] two ways.
+   c. Express the address of grid[0][0] three ways.

# 7. Create an appropriate declaration for each of the following variables:

+   a. digits is an array of 10 ints.
+   b. rates is an array of six floats.
+   c. mat is an array of three arrays of five integers.
+   d. psa is an array of 20 pointers to char.
+   e. pstr is a pointer to an array of 20 chars.

# 8.

+   a. Declare an array of six ints and initialize it to the values 1, 2, 4, 8, 16, and 32.
+   b. Use array notation to represent the third element (the one with the value 4) of the array in part a.
+   c. Assuming C99/C11 rules are in effect, declare an array of 100 ints and initialize it so that the last element is -1; don't worry about the other elements.
+   d. Assuming C99/C11 rules are in effect, declare an array of 100 ints and initialize it so that elements 5, 10, 11, 12, and 3 are 101; don't worry about the other elements.
# What Is an Array?

173

| DO | DON'T |
|---|---|
| use arrays instead of creating several variables that store the same thing. For example, if you want to store total sales for each month of the year, create an array with 12 elements to hold sales rather than creating a sales variable each month. | DON'T forget that array subscripts start at element 0.

8

# Using Multidimensional Arrays

A multidimensional array has more than one subscript. A two-dimensional array has two subscripts, a three-dimensional array has three subscripts, and so on. There is no limit to the number of dimensions a C array can have. (There is a limit on total array size, as discussed in this lesson.)

For example, you might write a program that plays checkers. Your checkerboard contains 64 squares arranged in eight rows and eight columns. Your program could represent the board as a two-dimensional array, as follows:

```
int checker[8][8];
```

The resulting array has 64 elements: checker[0] [0], checker[0] [1], checker[0] [2]...checker[7] [6], checker[7] [7]. The structure of this two-dimensional array is illustrated in Figure 8.3.

FIGURE 8.3 A two-dimensional array has a row-and-column structure.

```
int checker[8][8];
```

| checker[0][0] | checker[0][1] | checker[0][7] |
|---|---|---|
| checker[1][0] | checker[1][1] | checker[1][7] |
| checker[2][0] | checker[2][1] | checker[2][7] |
| checker[7][0] | checker[7][1] | checker[7][7] |

Similarly, a three-dimensional array could be thought of as a cube. Four-dimensional arrays (and higher) are probably best left to your imagination. No, matter how many dimensions they have, they are stored sequentially in memory. More detail on array storage is presented in Lesson 15, "Pointers to Pointers and Arrays of Pointers."
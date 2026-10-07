# Analysis

In Lesson 6, you saw a program that used a nested for statement; this program has two nested for loops. Before you look at the for statements in detail, note that lines 7 and 8 declare variables. The first is an array named random_array, used to hold random numbers. random_array is a three-dimensional type int that is 10-by-10-by-10, giving a total of 1000 int elements (10x10x10). Imagine coming with 1000 unique variable names if you couldn't use arrays! Line 8 declares three variables, a, b, and c, to control the for loops.

This program also includes the header file stdlib.h (for standard library). It is included to provide the prototype for the rand() function used on line 22.

The bulk of the program is contained in two nests of for statements. The first is in lines 16 through 25, and the second is in lines 29 through 42. Both for nests have the same structure. They work just like the loops in Listing 6.2, but they go one deeper. In the first set of for statements, line 22 is executed repeatedly. Line 22 assigns the value of c, rand(), to an element of the random_array array, where rand() is a library function that returns a random number.

Going backward through the list, you can see that line 20 changes c from 0 to 9. This loops through the farthest right subscript of the random_array array. Line 18 loops through b, the middle subscript of the random array. Each time b changes, it loops through all the c elements. Line 16 changes variable a, which loops through the farthest left subscript. Each time this subscript changes, it loops through all 10 values of b, which in turn loops through all 10 values of c. This initializes every value in the random array to a random number.

Lines 29 through 42 contain the second set of for statements. These work like the previous for statements, but these loops print each of the values assigned previously. After 10 are displayed, 38 prints a message and waits for Enter to be pressed. Line 40 takes care of the keypress using getchar(). If Enter hasn't been pressed, getchar() waits until it is. Run this program and watch the displayed values.

# Summary

This lesson introduced numeric arrays, a powerful data storage method under the same group name. Individual items, or elements, in an array are identified using a subscript after the array name. Computer programming tasks that involve repetitive data processing lend themselves to storage
Use a 50-by-50 array floor that's initialized to zeros. Read commands from an array that contains them. Keep track of the current turtle position at all times and whether the pen is currently up or down. Assume that the turtle always starts at position 0, 0 of the floor with its pen up. The set of turtle commands your program must process are shown in the following table:

| Command | Meaning |
|---|---|
| 1 | Pen up |
| 2 | Pen down |
| 3 | Turn right |
| 4 | Turn left |
| 5, 10 | Move forward 10 spaces (or a number other than 10) |
| 6 | Print the 50-by-50 array |
| 9 | End of data (sentinel) |

Suppose that the turtle is somewhere near the center of the floor. The following “program” would draw and print a 12-by-12 square:

```
2
5,12
3
5,12
3
5,12
3
5,12
1
6
9
```

As the turtle moves with the pen down, set elements of array floor to 1s. When the 6 command is given, display an asterisk for each 1 in the array. For each zero, display a blank. Write a program to implement the turtle-graphics capabilities discussed here. Write several turtle graphics programs to draw interesting shapes. Add other commands to increase the power of your turtle-graphics language.

# 6.24 (Knight's Tour)

One of the more interesting puzzles for chess buffs is the Knight's Tour problem, originally proposed by the mathematician Euler. The question is this: Can the chess piece called the knight move around an empty chessboard and touch each of the 64 squares once and only once? We study this intriguing problem in-depth here.

The knight makes L-shaped moves (two in one direction and then one in a perpendicular direction). Thus, from a square in the middle of an empty chessboard, the knight can make eight different moves (numbered 0 through 7), as shown in the following diagram:
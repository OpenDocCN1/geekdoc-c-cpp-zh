moved up or down. Assume that the turtle always starts at position 0, 0 of the floor with its pen up. The set of turtle commands your program must process is shown in Fig. 6.25. Suppose that the turtle is somewhere near the center of the floor. The following 'program' would draw and print a 12-by-12 square:

```
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
```

As the turtle moves with the pen down, set the appropriate elements of array floor to 1s. When the 6 command (print) is given, wherever there's a 1 in the array, display an asterisk, or some other character you choose. Wherever there's a zero, display a blank. Write a program to implement the turtle graphics capabilities discussed here. Write several turtle graphics programs to draw interesting shapes. Add other commands to increase the power of your turtle graphics language.

| Command | Meaning |
| --- | --- |
| 1 | Pen up |
| 2 | Pen down |
| 3 | Turn right |
| 4 | Turn left |
| 5, 10 | Move forward 10 spaces (or a number other than 10) |
| 6 | Print the 50-by-50 array |
| 9 | End of data (sentinel) |

Fig. 6.25 | Turtle commands.

**6.24 (Knight’s Tour)** One of the more interesting puzzles for chess buffs is the Knight’s Tour problem, originally proposed by the mathematician Euler. The question is this: Can the chess piece called the knight move around an empty chessboard and touch each of the 64 squares once and only once? We study this intriguing problem in depth here.

The knight makes L-shaped moves (over two in one direction and then over one in a perpendicular direction). Thus, from a square in the middle of an empty chessboard, the knight can make eight different moves (numbered 0 through 7) as shown in Fig. 6.26.

+   a) Draw an 8-by-8 chessboard on a sheet of paper and attempt a Knight’s Tour by hand. Put a 1 in the first square you move to, a 2 in the second square, a 3 in the third, and so on. Before starting the tour, estimate how far you think you’ll get, remembering that a full tour consists of 64 moves. How far did you get? Were you close to the estimate?
+   
+   b) Now let’s develop a program that will move the knight around a chessboard. The board itself is represented by an 8-by-8 two-dimensional array board. Each square is initialized to zero. We describe each of the eight possible moves in terms of both its horizontal and vertical components. For example, a move of type 0 as shown in Fig. 6.26 consists of
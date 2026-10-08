
Display the results in tabular format. Determine whether the totals are reasonable (e.g., there are six ways to roll a 7, so approximately one-sixth of the rolls should be 7).

| | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| 6 | 7 | 8 | 9 | 10 | 11 | 12 |

**Fig. 8.26** The 36 possible sums of two dice.

## 8.18 (Game of Craps) Write an app that runs 1,000,000 games of craps (Fig. 7.8) and answers the following:

- a) How many games are won on the first roll, second roll, ..., twentieth roll and after the twentieth roll?
- b) How many games are lost on the first roll, second roll, ..., twentieth roll and after the twentieth roll?
- c) What are the chances of winning at craps? [Note: You should discover that craps is one of the finest casinos.]
- d) What is the average length of a game of craps?

## 8.19 (Airline Reservations System) A small airline has purchased a computer for its new automated reservations system. You have been asked to write an app to assign seats on each flight of the airline's only plane (capacity: 10 seats). Display the following alternatives: Please type 1 for First Class and Please type 2 for Economy. If the user uses type 1, your app should assign a seat in the first-class section (seats 1-5). If the user uses type 2, your app should assign a seat in the economy section (seats 6-10).

Use a one-dimensional array of type to represent the seating chart of plane. Initialize all the elements of the array to false to indicate that all the seats are empty. As each seat is assigned, set the corresponding element of the array to true to indicate that the seat is no longer available. Your app should not assign a seat that has already been assigned. When the economy section is full, ask the user if it's acceptable to be placed in the first-class section (and vice versa). If yes, display the message "Next flight in 3 hours."

## 8.20 (Total Sales) Write a rectangular array to solve the problem: A company has three salespeople (1 to 3) who sell five different products (1 to 5). Once a day, each salesperson passes in a slip for each type sold. Each slip contains the following:

- a) The salesperson number
- b) The product number
- c) The total value of product sold that day

Thus, each salesperson passes between 0 and 5 sales per day. Assume that the information from all of the slips for that month is written. An app will read all the information for month's sales and summarize the total sales by salesperson and by product. All totals should be stored in rectangular array. After processing all the month, display the results in tabular format, with each column representing a particular salesperson and each row representing a particular product. Cross-total each row to get the total sales of product for last month. Cross-total column to get the total sales by salesperson for last month. Your tabular output should include these cross-totals to the right of the totaled rows and below the totaled columns.

## 8.21 (Turtle Graphics) The Logo language makes the concept of turtle graphics famous. Imagine a mechanical turtle walks around the room under the control of a C# app. The turtle holds a pen in one of two positions-up or down. When the pen is up, the turtle traces shapes as it moves, and when the pen is down, the turtle moves without writing anything. In this problem, you'll simulate the operation of the turtle and create a computerized sketch.

Use a 20-20 rectangular array initialized to 0. Read commands from an array that contains them. Keep track at all times of the current position of the turtle and whether it is currently up or down. Assume the turtle starts at position (0, 0) of the floor with its pen down and move to the right. Suppose that the turtle is somewhere near the center of the floor. The following "app" would draw a 12-by-12 square, leaving the pen in the up position:

- 2
- 5,12
- 3
- 5,12
- 3
- 5,12
- 6
- 9

As the turtle moves with the pen down, set the appropriate elements of array to 1. When the 6 command (display the array) is given, wherever there's 1 in the array, display an asterisk or any character you choose. Wherever there's 0, display a blank. Write an app to implement the turtle graphics discussed here. Draw interesting shapes. Add other commands to increase the power of the turtle graphics language.

| Command | Meaning |
|---|---|
| 1 | Pen up |
| 2 | Pen down |
| 3 | Turn right |
| 4 | Turn left |
| 5,10 | Move forward 10 spaces (replace 10 for a different number of spaces) |
| 6 | Display the 20-20 array |
| 9 | End of data (sentinel) |

**Fig. 8.27** Turtle commands.

## 8.22 (Knight's Tour) One of the more interesting puzzles for chess buffs is the Knight's Tour problem originally proposed by the mathematician Euler. Can this chess piece move around an empty chessboard and touch each of the 64 squares once and only? We study this intriguing problem in depth.

The knight only L-shaped moves (two spaces in one direction and one space in a perpendicular direction). Thus, as shown in Fig. 8.28, from a square near the middle of an empty chessboard, the knight (labeled K) can make different moves (numbered 0 through 7).

- Draw an eight-by-eight chessboard on a sheet of paper, and trace a Knight's Tour by hand. Put a 1 in the starting square, a 2 in the second square, a 3 in the third and on. Before starting the tour, estimate how far you'll get, remembering that a tour consists of 64 moves. How far did you get? Was this close to your estimate?

Now let's develop an app that will move the knight around the chessboard. Each board is represented by an eight-by-eight array. Initialize to zero each of the eight possible moves in terms of their horizontal and vertical components. For example, a move of type 0, as shown in Fig. 8.28, consists of moving two squares to the right and one square vertically. A move of type 2 consists of moving one square horizontally and two squares upward. Horizontal moves to the left and vertical moves upward are indicated with negative numbers. The eight moves may be described by two one-dimensional arrays, horizontal and vertical, as follows:

![](img/57baed2319be0bb1b5f9867486f2711_399_0.png)

horizontal[0] = 2 vertical[0] = -1
horizontal[1] = 1 vertical[1] = -2
horizontal[2] = -1 vertical[2] = -2
horizontal[3] = -2 vertical[3] = 1
horizontal[4] = -1 vertical[4] = 2
horizontal[5] = 1 vertical[5] = 2
horizontal[6] = 2 vertical[7] = 1

**Fig. 8.28** The possible moves of the knight.

Let variables currentRow and currentCol indicate the row and column, respectively, of the knight's position. To make a move of type moveNumber, where moveNumber is 0 and 7, your app should use the statements:

```
currentRow += vertical[moveNumber];
currentCol += horizontal[moveNumber];
```

Write an app to move the knight around the chessboard. Keep a counter that varies from 1 to 64. Record the latest count in each square the knight moves to. Test each potential move to see if the knight has already visited that square. Test every potential move to ensure the knight does not land off the chessboard. Run the app. How many moves did the knight make?

After attempting to write and run a Knight's Tour app, you probably developed some valuable insights. We will use these insights to develop a heuristic for moving the knight. Heuristics do not guarantee success, but a carefully developed one greatly improves the chance of success. You may have observed that the outer squares are more troublesome than the squares near the center of the board. In fact, the most troublesome and inaccessible squares are the four corners.

Intuition suggests that you should move the knight to the most troublesome squares first and leave those that are easiest to get to, so that when the board gets near the end of the tour, there will be a greater chance of success.

We could develop an "accessibility heuristic" by classifying each of the squares according to how accessible it is and always moving the knight (using the knight's moves) to the most inaccessible square. We label a two-dimensional array accessibility numbers indicating how many squares each particular square is accessible. On a chessboard, each square near the center is rated as 8, each corner is rated as 2, and the other squares have accessibility numbers of 3, 4 or 6 as follows:

```
2 3 4 4 3 2
3 4 6 6 4 3
4 6 8 8 6 4
4 6 8 8 6 4
4 6 6 6 4 3
3 4 4 4 3 2
```

Write a new version of the Knight's Tour, using the accessibility heuristic. The knight should always move to the square with the lowest accessibility number. In case of a tie, the knight may move to any of the tied squares. Therefore, the tour may begin in any of the corners.[Note: As the knight moves around the chessboard and more squares become occupied, your app should reduce the accessibility numbers. In this way, any given time during the tour, each square's accessibility number will remain equal to precisely the number of squares from that square may be reached.] Run your version of app. Give it a full tour. How many full tours did you get?

Write a version of the Knight's Tour that encounters a tie between two or more squares, decides which to choose by looking ahead at the "tied squares". Your app should move to the square for which the next move would arrive at the square with the lowest accessibility number.

## 8.23 (Knight's Tour: Brute-Force Approaches) In part c Exercise 8.22, we developed a solution to the Knight's Tour problem using the "accessibility heuristic," which generates many solutions and executes efficiently. As computers continue to increase in power, we will be able to solve problems with slower computer power and relatively unsoptimized algorithms. Let's call this approach "brute-force" problem.

- a) Use random-number to enable the knight to walk around the chessboard (in random L-shaped moves) at random. Your app should run one tour and display the final chessboard. How far did the knight get?

- b) Most likely, the app in Part produced a relatively short tour. Now you modify your app to attempt 1000 tours. Use one-dimensional array to keep track of the number of tours of each length. When your app finishes the 1000 tours, it should display this information in neat tabular format. What was the best result?

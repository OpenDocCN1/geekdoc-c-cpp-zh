# 400 Chapter 8 Arrays; Introduction to Exception Handling

After attempting to write and run a Knight's Tour app, you probably developed some valuable insights. We will use these insights to develop a heuristic for moving the knight. Heuristics do not guarantee success, but a carefully developed greatly improves the chance of success. You may have observed that the outer squares are more troublesome than the squares near the center of the board. In fact, the most troublesome and inaccessible squares are the four corners.

Intuition suggests that you should move the knight to the most troublesome squares first and leave those that are easiest to get to, so that when the board gets near the end of the tour, there will be a greater chance of success.

We could develop an "accessibility heuristic" by classifying each of the squares according to how accessible it is and always moving the knight (using the knight's moves) to the most inaccessible square. We label two-dimensional array accessibility numbers indicating how many squares each particular square is accessible. On a chessboard, each of the 16 squares near the center is rated as 8, each corner square is rated as 2, and the other squares have accessibility numbers of 3, 4 or 6 as follows:

```
2 3 4 4 4 3 2
3 4 6 6 6 4 3
4 6 8 8 8 6 4
4 6 8 8 8 6 4
4 6 8 8 8 6 4
3 4 6 6 6 4 3
2 3 4 4 4 3 2
```

Write a new version of the Knight's Tour, using the accessibility heuristic. The knight should always move to the square with the lowest accessibility number. In case of a tie, the knight may move to any of the tied squares. Therefore, the tour may begin in any of the corners.[Note: As the knight moves around the chessboard and more squares become occupied, your app should reduce the accessibility numbers. In this way, any given time during the tour, each square's accessibility number will remain equal to precisely the number of squares from that square may be reached.] Run your version of your app. Give it a full tour. How many full tours did you get?

Write a version of the Knight's Tour that encounters a tie between two or more squares, decides which to choose by looking ahead at the "tied squares". Your app should move to the square for which the next move would arrive at the square with the lowest accessibility number.

8.23 (Knight's Tour: Brute-Force Approaches) In part c Exercise 8.22, we developed a solution to the Knight's Tour problem using the "accessibility heuristic," which generates many solutions and executes efficiently. As computers continue to increase in power, we will be able to solve problems with slower computer power and relatively unsoptimized algorithms. Let's call this approach "brute-force" problem.

+   a) Use random-number to enable the knight to walk around the chessboard (in random L-shaped moves) at random. Your app should run one tour and display the final chessboard. How far did the knight get?

+   b) Most likely, the app in Part produced a relatively short tour. Now you modify your app to attempt 1000 tours. Use one-dimensional array to keep track of the number of tours of each length. When your app finishes the 1000 tours, it should display this information in neat tabular format. What was the best result?
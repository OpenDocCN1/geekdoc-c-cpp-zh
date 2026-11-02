# **6.20 (Game of Craps)** Write a program that runs 1000 games of craps (without human intervention) and answers each of the following questions:

+   a) How many games are won on the first roll, second roll, …, twentieth roll and after the twentieth roll?
+   
+   b) How many games are lost on the first roll, second roll, …, twentieth roll and after the twentieth roll?
+   
+   c) What are the chances of winning at craps? [**Note:** You should discover that craps is one of the fairest casino games. What do you suppose this means?]
+   
+   d) What’s the average length of a game of craps?
+   
+   e) Do the chances of winning improve with the length of the game?

# **6.21** An *n × m* two-dimensional matrix can be multiplied by another *m × p* matrix to give a matrix whose elements are the sum of the products of the elements within a row from the first matrix and the associated elements of a column of the second matrix. Both matrices should either be square matrices, or the number of columns of the first matrix should equal the number of rows of the second matrix.

To calculate each element of the resultant matrix, multiply the first element of a given row from the first matrix and the first element of a given column in the second matrix, add that to the product of the second element of the same row and the second element of the same column, and keep doing so until the last elements of the row and column have been multiplied and added to the sum.

Write a program to calculate the product of 2 matrices and store the result in a third matrix.

# **6.22 (Total Sales)** Use a two-dimensional array to solve the following problem. A company has four salespeople (1 to 4) who sell five different products (1 to 5). Once a day, each salesperson passes in a slip for each different type of product sold. Each slip contains:

+   a) The salesperson number
+   
+   b) The product number
+   
+   c) The total dollar value of that product sold that day

Thus, each salesperson passes in between 0 and 5 sales slips per day. Assume that the information from all of the slips for last month is available. Write a program that will read all this information for last month’s sales and summarize the total sales by salesperson by product. All totals should be stored in the two-dimensional array sales. After processing all the information for last month, print the results in tabular format with each column representing a particular salesperson and each row representing a particular product. Cross total each row to get the total sales of each product for last month; cross total each column to get the total sales by salesperson for last month. Your tabular printout should include these cross totals to the right of the totaled rows and to the bottom of the totaled columns.

# **6.23 (Turtle Graphics)** The Logo language made the concept of *turtle graphics* famous. Imagine a mechanical turtle that walks around the room under the control of a C program. The turtle holds a pen in one of two positions, up or down. While the pen is down, the turtle traces out shapes as it moves; while the pen is up, the turtle moves about freely without writing anything. In this problem you will simulate the operation of the turtle and create a computerized sketchpad as well.

Use a 50-by-50 array floor which is initialized to zeros. Read commands from an array that contains them. Keep track of the current turtle position at all times and whether the pen is cur-
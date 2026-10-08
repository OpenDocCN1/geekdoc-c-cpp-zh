Display the results in tabular format. Determine whether the totals are reasonable (e.g., there are six ways to roll a 7, so approximately one-sixth of the rolls should be 7).

| | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---||}{
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| 6 | 7 | 8 | 9 | 10 | 11 | 12 |

**Fig. 8.26** The 36 possible sums of two dice.

# **8.18 (Game of Craps)** Write an app that runs 1,000,000 games of craps (Fig. 7.8) and answers the following:

+   a) How many games are won on the first roll, second roll, ..., twentieth roll and after the twentieth roll?
b) How many games are lost on the first roll, second roll, ..., twentieth roll and after the twentieth roll?
c) What are the chances of winning at craps? [Note: You should discover that craps is one of the finest casinos.
d) What is the average length of a game of craps?

**8.19 (Airline Reservations System)** A small airline has purchased a computer for its new automatedreservations system. A small airline has purchased a computer for its new automated reservations system. You have been asked to write an app to assign seats on each flight of the airline's only plane (capacity: 10 seats). Display the following alternatives: Please type 1 for First Class and Please type 2 for Economy. If the user uses type 1, your app should assign a seat in the first-class section (seats 1-5). If the user uses type 2, your app should assign a seat in the economy section (seats 6-10).

Use a one-dimensional array of type to represent the seating chart of plane. Initialize all the elements of the array to false to indicate that all the seats are empty. As each seat is assigned, set the corresponding element of the array to true to indicate that the seat is no longer available. Your app should not assign a seat that has already been assigned. When the economy section is full, ask the user person if it's acceptable to be placed in the first-class section (and vice versa). If yes, display the message "Next flight in 3 hours."

# **8.20 (Total Sales)** Write a rectangular array to solve the problem: A company has three salespeople (1 to 3) who sell five different products (1 to 5). Once a day, each salesperson passes in a slip for each type sold. Each slip contains the following:

+   a) The salesperson number
b) The product number
c) The total value of product sold that day

Thus, each salesperson passes between 0 and 5 sales per day. Assume that the information from all of the slips for that month is written. An app will read all the information for month's sales and summarize the total sales by salesperson and by product. All totals should be stored in rectangular array. After processing all the month, display the results in tabular format, with each column representing a particular salesperson and each row representing a
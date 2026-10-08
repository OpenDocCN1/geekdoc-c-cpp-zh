
# Exercises 401

- c) Most likely, the app in Part b gave you some “respectable” tours, but not full tours. Let your app run until it produces a full tour. Once again, keep a table of the number of tours of each length, and display this table when the first tour is found. How many tours did your app attempt before producing a full tour?

- d) Compare the brute-force version of the Knight's Tour with the accessibility-heuristic version. Which required a more careful study of the problem? Which algorithm was more difficult to develop? Which required more computer power? Could we be certain (in advance) of obtaining a full tour with the accessibility-heuristic approach? Could we be certain (in advance) of obtaining a full tour with the brute-force approach? Argue the pros and cons of brute-force problem solving.

**8.24 (Eight Queens)** Another puzzle for chess is the Eight Queens problem, which asks to place queens on an empty chessboard so that no queen is “attacking” any other (i.e., no two queens are in the same row, the same column or the same diagonal)? Use the thinking developed in Exercise 8.22 to formulate a heuristic for solving the Eight Queens problem. Run your app. [Hint: It is possible to assign a value to each square of the chessboard to indicate how many squares of each chessboard are “eliminated” if a queen is placed in that square. Each of the corners would be assigned the value 22, as demonstrated by Fig. 8.29. Once these elimination numbers are placed in all 64 squares, an appropriate heuristic might be as follows: Place the next queen in the square with the smallest elimination number. Why is this strategy intuitively appealing?]

![](img/57baed2319be0bb1b5f98674846f2711_401_0.png)

**Fig. 8.29** The 22 squares eliminated by placing a queen in the upper left corner.

**8.25 (Eight Queens: Brute-Force Approaches)** In this exercise, you’ll develop several brute-force approaches to solving the Eight Queens problem introduced in Exercise 8.24.

- a) Use the random brute-force technique introduced in Exercise 8.23 to solve the Eight Queens problem.

- b) Use an exhaustive technique (i.e., try all combinations of eight queens on the chessboard) to solve the Eight Queens problem.

**8.26 (Knight’s Tour: Closed-Tour Test)** In the Knight’s Tour (Exercise 8.22), a full tour occurs when the knight makes 64 moves, touching each square of the chessboard and only once. A closed tour occurs when the 64th move is one move away from the square in which the tour started. Modify the app you wrote in Exercise 8.22 to test for a closed tour if a full tour has occurred.

- a) Create a simple bool array with all elements initialized to true. Array elements with prime indices will remain true. All other array elements will eventually be set to false. Starting with array index 2, determine whether a given element is true. If so, loop through the remainder of the array and set to false every element whose index is a multiple of the index for the element value true. Continue the process with the next element value true. For array index 2, all elements beyond 2 in the array that are multiples of 2 (indices 4, 6, 8, 10, etc.) will be set to false; for array index 3, all elements multiples of 3 in the array (indices 6, 9, 12, 15, etc.) will be set to false; and so on. When this process completes, the array elements that are still true indicate that the index is a prime number. Then write an app that uses an array of 1000 elements to determine and display the prime numbers between 2 and 999. Ignore elements 0 and 1.

# 8.28 (Simulation: The Tortoise and the Hare) You will now create the classic race of the tortoise and the hare. Use random-number generation to develop a simulation of this memorable event. Our contenders begin the race at square 1 of 70. Each square represents a possible position along the race course. The finish line is at square 70. The first contender to reach or pass square 70 wins with a pair of carrots. The course weaves up the side of a slippery mountain, occasionally the contenders lose. A clock ticks each second of the clock, your app adjust the position of the animals according to the rules in Fig. 8.30. Use variables to keep track of the positions of the animals (i.e., position 1–70). Start each animal at position 1 (the "starting gate"). If an animal slips before square 1, move back to square 1.

| Animal | Move type | Percentage of the time | Actual move |
| :--- | :--- | :--- | :--- |
| Tortoise | Fast plod | 50% | 3 squares to the right |
| | Slip | 20% | 6 squares to the left |
| | Slow plod | 30% | 1 square to the right |
| Hare | Sleep | 20% | No move at all |
| | Big hop | 20% | 9 squares to the right |
| | Big slip | 10% | 12 squares to the left |
| | Small hop | 30% | 1 square to the right |
| | Small slip | 20% | 2 squares to the right |

> Fig. 8.30 Rules for adjusting the positions of the tortoise and the hare.

Generate the percentages in Fig. 8.30 by producing a random integer i in the range 1–10. For the tortoise, perform a "fast plod" when i is in the range 1–5, a "slip" when i is 6 or 7, or a "slow plod" when i is 8–10. Use a similar technique to move the hare. Begin the race by displaying

```
ON MARK, GET
AND THEY'RE OFF
```

Then, for each tick of the clock (i.e., each iteration of a loop), display a 70-position line showing the T position of the tortoise and the H position of the hare. Occasionally, the contenders will land on the same square. In this case, the tortoise bites the hare, and your app should display the other than the T, the H or a case of tie. After each line is displayed, test for whether either animal has reached or passed 70. If so, display the winner and terminate the simulation. If the tortoise wins, display TORTOISE wins! If the hare wins, display Hare wins. If both animals are on the same tick of the clock, you may want to favor the tortoise ('underdog'), or you may want to display It's tie. If neither wins, perform the loop again to simulate the next tick. When you're ready to run your app, assemble a crowd of fans to watch the race. You'll be amazed at how involved your audience gets!

**8.29 (Card Shuffling and Modifying)** Define a five-card poker hand. Then modify class DeckCards to include methods that determine whether a hand contains

- a pair
- two pairs
- three of a kind (e.g., three jacks)
- four of a kind (e.g., four aces)
- a flush (i.c., all cards of the same suit)
- a straight (i.c., five cards of consecutive values)
- a full house (i.c., two cards of one value and three cards of another value)

**8.30 (Merging Arrays)** Write a program to merge two arrays of the same size, sorted in ascending order. Test the program with relevant values.

# Special Section: Building Your Computer

In the next problems, we take a temporary diversion from the world of high-level language programming to "peer open" a computer and look at its internal structure. We introduce machine-language programming and write several machine-language programs. To make this a valuable experience, we will build a computer (through the technique of software-based simulation) on which you can execute your machine-language programs.

8.31 (Machine-Language Programming) Let's create a computer like the Simple. As its name implies, it's simple, but powerful. The Simple runs programs written in the only language it understands: Simple Machine Language, or SML for short.

The Simple contains an accumulator—a special register where information is put before the Simple uses it in calculations or evaluations in various ways. All the information in the Simple is handled in words. A word is a signed-digit decimal number, such as +3364, -1293, +0000 and -0001. The Simple is equipped with a 100-word memory, and words are referenced by their location numbers 00, 01, ..., 99.

Before running an SML program, we must load, or place, the code into the memory. The first instruction (or statement) of every SML program is always placed in location 00. The Simple will start executing that instruction.

Each instruction in SML occupies one word of the Simple's memory (hence instructions are four-digit numbers). We assume that the sign of an SML instruction is always plus, but the sign of a data may be plus or minus. In the Simple's memory contains an instruction, a value used by a program or an (hence undefined) area of memory. The first two digits of each SML instruction are the operation code specifying the operation to be performed. SML operations are counted in Fig. 8.31.

The last two digits of each instruction are the address—the address of the memory location containing the operation applies. Let's consider several simple programs. The first SML program, +1007 reads the first number from the keyboard, and then displays them. Then puts it into location 07 (which was initialized to 0). Then instruction +1008 reads the next number into location 08. The load instruction, +2007, puts the first number into the accumulator, and the add instruction, +3008, adds the second number to the number in the accumulator. All SML arith-

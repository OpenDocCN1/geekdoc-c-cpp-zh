
# Programming Projects 235

specified with only a few rules. This project asks you to write a program that allows you to specify an initial configuration. The program follows the rules of Life (listed shortly) to show the continuing behavior of the configuration.

LIFE is an organism that lives in a discrete, two-dimensional world. While the world is actually unlimited, we do not have luxury, so we restrict the array to 80 characters wide by 22 character positions high. If you have access to a larger screen, by all means use it.

This world is an array with each cell capable of holding one LIFE cell. Generations mark the passing of time. The births and deaths within the LIFE community follow this set of rules:

- 1. We define each cell to have neighbor cells. The neighbors of a cell are the cells directly above, below, to the right, to the left, diagonally to the right and left and diagonally to the right and left.
- 2. If an occupied cell has zero or one neighbor, it dies of loneliness. If an occupied cell has more than three neighbors, it dies of overcrowding.
- 3. If an empty cell has exactly three occupied neighbor cells, there is a birth of a new cell to replace the empty cell.
- 4. Births and deaths are instantaneous and occur at the changes of generation. A cell dying for whatever reason may help birth, but a newborn cell cannot resist the death of another, by using the local population.

> *** becomes then becomes *** again, and so on.

Notes: Some configurations grow from relatively small starting configurations. Others move across the region. It is recommended that text output you use a rectangular char with 80 columns and 22 rows to store the LIFE world's successive generations. We use an + to indicate a living cell and use a blank to indicate an empty (or dead) cell. If you have a screen with more rows than that, by all means use the whole screen.

Suggestions: Look for stable configurations. That is, look for communities that repeat patterns continuously. The number of configurations in the repetition is the period. There are configurations that are fixed, that is, that continue without change. A possible project is to find such configurations.

Hints: Define a void named generation that takes the array we call world, an 80-column by 22-row array of type char, which contains the initial configuration. The function scans the array and modifies the cells, marking the cells with births and deaths in accord with the rules listed previously. This involves examining each cell in turn and either killing the cell, letting it live, or if it is empty, deciding whether a cell should be born. This should be a function display that accepts the array world and displays the array on the screen. Some sort of time delay is appropriate between calls to generation and display. To do this, your program should generate and display the next generation you press Return. You are at liberty to automate this, but automation is not necessary to the program. (Wait, there is a typo in the OCR "to the program" and "you press Return" - let me re-align).

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_264_0.png)

## 236 CHAPTER 5 Arrays

press Return. You are at liberty to automate this, but automation is not necessary to the program.

- 13. A common memory matching game played by young children is to start with a deck of cards that contains identical pairs. For example, given six cards in the deck, two might be labeled "1", two might be labeled "2", and two might be labeled "3". The cards are shuffled and placed facedown on the table. The player selects two cards that are facedown, turns them faceup, and if they match they are left facedown. If the cards do not match, they are returned to their original position facedown. The game continues until all cards are facedown.

Write a program that plays the memory matching game. Use 16 cards that are laid out in a 4 × 4 square and are labeled with numbers from 1 to 8. Your program should allow the player to specify the cards through a coordinate system. For example, in the following layout:

| 1 | 2 | 3 | 4 |
|---|---|---|---|
| 1 | 8 | * | * |
| * | * | * | * |
| 3 | * | 8 | * |
| 4 | * | * | * |

all of the cards are facedown for the pair of 8's, which has been located at coordinates (1,1) and (2,3). To hide the cards that have been temporarily placed up, output a large number. Hint: Use a 2D array for the arrangement and another 2D array that indicates whether a card is facedown.

- 14. You have collected reviews from four reviewers where the movies are numbered 100–105. Each reviewer rated the movies with a range from 1 (terrible) to 5 (excellent). The reviews are shown in the following table:

| 100 | 101 | 102 | 103 | 104 | 105 |
|---|---|---|---|---|---|
| 0 | 3 | 2 | 5 | 1 | 2 |
| 1 | 4 | 2 | 1 | 4 | 2 |
| 2 | 5 | 1 | 4 | 4 | 1 |
| 3 | 1 | 4 | 2 | 2 | 3 |

Write a program that stores this data in a 2D array. Your program should allow the user to input three movies. The program should then find which reviewer are closest to the user's input and predict the other two.

- 15. Traditional password entry schemes are susceptible to "shoulder surfing" in which an attacker watches an unsuspecting user enter their PIN and uses it later. One way to combat this is with a randomized system. In this system, the user enters a response based on a randomly generated five-digit PIN (00000-99999). Each digit is assigned a random number of 1, 2, or 3. For example, if the actual PIN is 12345, the user would be presented with:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| 3 | 2 | 3 | 1 | 1 | 3 | 2 | 2 | 1 | 3 |

Your program should simulate the authentication process. Store the actual PIN in your number. The program should use an array to assign random digits from 0 to 9. Output the random digits to the screen, input the response from the user, and output whether or not the user's response matches the PIN. This does not reveal the password even if an attacker intercepts the entry because 23113 could correspond to other PINs such as 69440 or 70439. The next time the user logs in, a sequence of random numbers would be generated:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 2 | 3 | 3 | 1 | 2 | 2 | 3 | 3 | 3 |

- 16. Do Programming Project 5.14 instead of only four reviewers up to 1000 and store the reviews in a text file. While your program should support up to 1000 reviewers, the actual number of reviewers stored in the text file could vary from 1 to 1000. The only movies that are reviewed are numbered from 100 to 105 as in Programming Project 1.4. You are welcome to design the format used to store the reviews in the text file. After the reviews are read from the text file, your program should input three movies and make predictions for the remaining two as in Programming Project 5.14.

## Programming Projects 237

17. Programming Project 2.12 asked you to enforce Benjamin's Law. An easier way to write the program is to use an array to store the digit counts. Each digit, count [0] might store the number of times 0 is the first digit (if it is possible in your data set), count [1] might store the number of times 1 is the first digit, and so forth. Redo Programming Project 2.12 using arrays.

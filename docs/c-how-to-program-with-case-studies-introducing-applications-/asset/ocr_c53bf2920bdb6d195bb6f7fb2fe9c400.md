# Self Check

1 (Fill-In) A common use of an array of pointers is to form an array of strings, referred to simply as a ________.
**Answer:** string array.

2 (True/False) The characters of the strings in this section’s suit array are stored directly in the array’s elements.
**Answer:** False. Though the array appears to contain four strings, each element actually contains the address of the corresponding string’s first character. The actual letters and terminating null characters are stored elsewhere in memory.

# 7.11 Random-Number Simulation Case Study: Card Shuffling and Dealing

Let’s use random number generation to develop a card shuffling and dealing simulation program, which can then be used to implement programs that play card games. To reveal some subtle performance problems, we’ve intentionally used suboptimal shuffling and dealing algorithms. In this chapter’s exercises and in Chapter 10, we develop more efficient algorithms.

Using the top-down, stepwise refinement approach, we develop a program that will shuffle a deck of 52 playing cards, then deal each card. The top-down approach is particularly useful in attacking more complex problems than you’ve seen in earlier chapters.

# Representing a Deck of Cards as a Two-Dimensional Array

We use a 4-by-13 two-dimensional array deck to represent the deck of playing cards:

![](bbox=[0.22, 0.86, 0.85, 0.96])

The rows correspond to the suits—row 0 corresponds to hearts, row 1 to diamonds, row 2 to clubs and row 3 to spades. The columns correspond to the cards’ face values. Columns 0 through 9 correspond to ace through ten, and columns 10 through 12 correspond to jack, queen and king. We’ll load string array suit with character strings representing the four suits, and load string array face with character strings representing the 13 face values.
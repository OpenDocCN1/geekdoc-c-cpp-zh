
- e) Determine whether the hand contains a flush (i.e., all five cards of the same suit).
- f) Determine whether the hand contains a straight (i.e., five cards of consecutive face values).

## 7.13 (Project: Card Shuffling and Dealing—Which Poker Hand is Better?)

Use the functions developed in Exercise 7.12 to write a program that deals two five-card poker hands, evaluates each, and determines which is the better hand.

## 7.14 (Project: Card Shuffling and Dealing—Simulating the Dealer)

Modify the program developed in Exercise 7.13 so that it can simulate the dealer. The dealer's five-card hand is dealt "face down" so the player cannot see it. The program should then evaluate the dealer's hand, and based on the quality of the hand, the dealer should draw one, two or three more cards to replace the corresponding number of unneeded cards in the original hand. The program should then reevaluate the dealer's hand. [Caution: This is a difficult problem!]

## 7.15 (Project: Card Shuffling and Dealing—Allowing Player's to Draw Cards)

Modify the program developed in Exercise 7.14 so that it can handle the dealer's hand automatically, but the player is allowed to decide which cards of the player's hand to replace. The program should then evaluate both hands and determine who wins. Now use this new program to play 20 games against the computer. Who wins more games, you or the computer? Have one of your friends play 20 games against the computer. Who wins more games? Based on these games' results, refine your poker-playing program (this, too, is a difficult problem). Play 20 more games. Does your modified program play a better game?

## 7.16 (Card Shuffling and Dealing Modification: High-Performance Shuffle)

In Fig. 7.16, we intentionally used an inefficient card shuffling algorithm with the possibility of indefinite postponement. In this problem, you'll create a high-performance shuffling algorithm that avoids indefinite postponement.

Modify the program of Fig. 7.16 as follows. Begin by initializing the deck array as shown below:

| Unshuffled array |  |  |  |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|  | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 1 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 |
| 2 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 | 36 | 37 | 38 | 39 |
| 3 | 40 | 41 | 42 | 43 | 44 | 45 | 46 | 47 | 48 | 49 | 50 | 51 | 52 |

Modify the shuffle function to loop row-by-row and column-by-column through the array, touching every element once. Each element should be swapped with a randomly selected element of the array. Print the resulting array to determine whether the deck is satisfactorily shuffled. The following is a sample set of shuffled values:

### Sample shuffled array

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 19 | 40 | 27 | 25 | 36 | 46 | 10 | 34 | 35 | 41 | 18 | 2 | 44 |
| 1 | 13 | 28 | 14 | 16 | 21 | 30 | 8 | 11 | 31 | 17 | 24 | 7 | 1 |
| 2 | 12 | 33 | 15 | 42 | 43 | 23 | 45 | 3 | 29 | 32 | 4 | 47 | 26 |
| 3 | 50 | 38 | 52 | 39 | 48 | 51 | 9 | 5 | 37 | 49 | 22 | 6 | 20 |

You may want your program to call the shuffle function several times to ensure a satisfactory shuffle.

Although the approach in this problem improves the shuffling algorithm, the dealing algorithm still requires searching the deck array for card 1, then card 2, then card 3, and so on. Worse yet, even after the dealing algorithm locates and deals the card, the algorithm still searches through the remainder of the deck. Modify the program of Fig. 7.16 so that once a card is dealt, no further attempts are made to match that card number, and the program immediately proceeds with dealing the next card. In Chapter 10, we develop a dealing algorithm that requires only one operation per card.

## 7.17 What does this program do, assuming the user enters two strings of the same length?

```c
// ex07_19.c
// What does this program do?
#include <stdio.h>
#define SIZE 80

void mystery1(char *s1, const char *s2); // prototype

int main(void) {
    char string1[SIZE]; // create char array
    char string2[SIZE]; // create char array

    puts("Enter two strings: ");
    scanf("%39s%39s", string1, string2);
    mystery1(string1, string2);
    printf("%s", string1);
}

// What does this function do?
void mystery1(char *s1, const char *s2) {
    while (*s1 != '\0') {
        ++s1;
    }

    for (; *s1 = *s2; ++s1, ++s2) {
        ; // empty statement
    }
}
```

## 7.18 What does this program do?

```c
// ex07_20.c
// what does this program do?
#include <stdio.h>
#define SIZE 80

size_t mystery2(const char *s); // prototype

int main(void) {
    char string[SIZE]; // create char array

    puts("Enter a string: ");
    scanf("%79s", string);
    printf("%d\n", mystery2(string));
}

// What does this function do?
size_t mystery2(const char *s) {
    size_t x;

    // Loop through string
    for (x = 0; *s != '\0'; ++s) {
        ++x;
    }

    return x;
}
```

## 7.19 Find the error in each of the following program segments. If the error can be corrected, explain how.

Find the error in each of the following program segments. If the error can be corrected, explain how.

- a) int *number;
      printf("%d\n", *number);
- b) float *realPtr;
      long *integerPtr;
      integerPtr = realPtr;
- c) int * x, y;
      x = y;
- d) char s[] = "this is a character array";
      int count;
      for (; *s != '\0'; ++s) {
          printf("%c ", *s);
      }
- e) short *numPtr, result;
      void *genericPtr = numPtr;
      result = *genericPtr + 7;
- f) float x = 19.34;
      float xPtr = &x;
      printf("%f\n", xPtr);
- g) char *s;
      printf("%s\n", s);

## 7.20 (Maze Traversal)

The following grid is a two-dimensional array representation of a maze. The # symbols represent the maze's walls, and the periods (.) represent squares in the possible paths through the maze.

![](img/43d318ad505997c339a3ea78d716d162_415_0.png)

The Wikipedia page https://en.wikipedia.org/wiki/Maze_solving_algorithm lists several algorithms for finding a maze's exit. A simple algorithm for walking through a maze guarantees finding the exit (assuming there's an exit). Place your right hand on the wall to your right, and begin walking forward. Never remove your hand from the wall. If the maze turns to the right, you follow the wall to the right. As long as you do not remove your hand from the wall, eventually you'll arrive at the maze's exit. If there's not an exit, you'll eventually arrive back at the starting location. There may be a shorter path than the one you've taken, but you're guaranteed to get out of the maze.

Write recursive function mazeTraverse to walk through the maze. The function should receive as arguments a 12-by-12 character array representing the maze and the maze's starting location. As mazeTraverse attempts to locate the exit from the maze, it should place the character X in each square in the path. The function should display the maze after each move so the user can watch as the maze is solved.

## 7.21 (Generating Mazes Randomly)

Write a function mazeGenerator that takes as an argument a two-dimensional 12-by-12 character array and randomly produces a maze. The function should also provide the starting and ending locations of the maze. Try your function mazeTraverse from Exercise 7.20 using several randomly generated mazes.

## 7.22 (Mazes of Any Size)

Generalize functions mazeTraverse and mazeGenerator of Exercises 7.20–7.21 to process mazes of any width and height.

## 7.23 What does this program do, assuming that the user enters two strings of the same length?

```c
// ex07_26.c
// What does this program do?
#include <stdio.h>
#define SIZE 80

int mystery3(const char *s1, const char *s2); // prototype

int main(void) {
    char string1[SIZE]; // create char array
    char string2[SIZE]; // create char array

    puts("Enter two strings: ");
    scanf("%79s%79s", string1, string2);
    printf("The result is %d\n", mystery3(string1, string2));
}

int mystery3(const char *s1, const char *s2) {
    int result = 1;

    for (; *s1 != '\0' && *s2 != '\0'; ++s1, ++s2) {
        if (*s1 != *s2) {
            result = 0;
        }
    }

    return result;
}
```

## Arrays of Function Pointers

### 7.24 (Arrays of Function Pointers) Rewrite the program of Fig. 6.17 to use a menu-driven interface. The program should offer the user four options as follows:

```
Enter a choice:
   0  Print the array of grades
   1  Find the minimum grade
   2  Find the maximum grade
   3  Print the average on all tests for each student
   4  End program
```

One restriction on using arrays of pointers to functions is that all the pointers must have the same type. The pointers must be to functions of the same return type that receive arguments of the same type. For this reason, the functions in Fig. 6.17 must be modified so that they each return the same type and take the same parameters. Modify functions minimum and maximum to print the minimum or maximum value and return nothing. For option 3, modify function average of Fig. 6.17 to output the average for each student (not a specific student). Function average should return nothing and take the same parameters as printArray, minimum and maximum. Store the pointers to the four functions in array processGrades and use the choice made by the user as the subscript into the array for calling each function.

### 7.25 (Calculating Circle Circumference, Circle Area or Sphere Volume Using Function Pointers) Using the techniques from Fig. 7.18, create a menu-driven program.

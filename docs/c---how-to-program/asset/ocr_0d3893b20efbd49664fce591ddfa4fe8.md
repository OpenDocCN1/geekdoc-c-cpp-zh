| | |
|---|---|
| Six of Diamonds | Five of Hearts |
| Ace of Spades | Six of Hearts |
| Nine of Diamonds | Queen of Clubs |
| Eight of Spades | Nine of Clubs |
| Deuce of Clubs | Six of Clubs |
| Ace of Clubs | Jack of Clubs |
| Four of Clubs | Eight of Clubs |
| Four of Spades | Seven of Spades |
| Seven of Diamonds | Seven of Clubs |
| King of Spades | Ten of Diamonds |
| Jack of Hearts | Ace of Hearts |
| Jack of Spades | Ten of Clubs |
| Eight of Diamonds | Deuce of Diamonds |
| Ace of Diamonds | Nine of Spades |
| Four of Hearts | Deuce of Hearts |
| King of Diamonds | Ten of Spades |
| Three of Hearts | Ten of Hearts |

**Fig. 7.25** | Sample run of card dealing program. (Part 2 of 2.)

# ## 7.12 Pointers to Functions

A pointer to a function contains the *address* of the function in memory. In Chapter 6, we saw that an array name is really the address in memory of the first element of the array. Similarly, a function name is really the starting address in memory of the code that performs the function’s task. Pointers to functions can be *passed* to functions, *returned* from functions, *stored* in arrays and *assigned* to other function pointers.

# ### 7.12.1 Sorting in Ascending or Descending Order

To illustrate the use of pointers to functions, Fig. 7.26 presents a modified version of the bubble sort program in Fig. 7.15. The new version consists of `main` and functions `bubble`, `swap`, `ascending` and `descending`. Function `bubbleSort` receives a pointer to a function—either function `ascending` or function `descending`—as an *argument*, in addition to an integer array and the size of the array. The program prompts the user to choose whether the array should be sorted in *ascending* or in *descending* order. If the user enters 1, a pointer to function `ascending` is passed to function `bubble`, causing the array to be sorted into *increasing* order. If the user enters 2, a pointer to function `descending` is passed to function `bubble`, causing the array to be sorted into *decreasing* order. The output of the program is shown in Fig. 7.27.

```
```c
1  // Fig. 7.26: fig07_26.c
2  // Multipurpose sorting program using function pointers.
3  #include <stdio.h>
4  #define SIZE 10
5
```
```

**Fig. 7.26** | Multipurpose sorting program using function pointers. (Part 1 of 3.)
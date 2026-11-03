
the deck. We've chosen to program these operations separately because normally cards are dealt after they're shuffled (not while they're being shuffled).

## Implementing the Card Shuffling and Dealing Program

The card shuffling and dealing program is shown in Fig. 7.24, and a sample execution is shown in Fig. 7.25. Conversion specifier %s is used to print strings of characters in the calls to printf. The corresponding argument in the printf call must be a pointer to char (or a char array). The format specification "%5s of %-8s" (line 68) prints a character string right justified in a field of five characters followed by " of " and a character string left justified in a field of eight characters. The minus sign in %-8s signifies left justification. There's a weakness in the dealing algorithm. Once a match is found, the two inner for statements continue searching the remaining elements of deck for a match. We correct this deficiency in this chapter's exercises and in a Chapter 10 case study.

```c
// Fig. 7.24: fig07_24.c
// Card shuffling and dealing.
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SUITS 4
#define FACES 13
#define CARDS 52

// prototypes
void shuffle(unsigned int wDeck[][FACES]); // shuffling modifies wDeck
void deal(unsigned int wDeck[][FACES], const char *wFace[],
 const char *wSuit[]); // dealing doesn't modify the arrays

int main(void)
{
 // initialize deck array
 unsigned int deck[SUITS][FACES] = {0};

 srand(time(NULL)); // seed random-number generator
 shuffle(deck); // shuffle the deck

 // initialize suit array
 const char *suit[SUITS] =
 {"Hearts", "Diamonds", "Clubs", "Spades"};

 // initialize face array
 const char *face[FACES] =
 {"Ace", "Deuce", "Three", "Four",
 "Five", "Six", "Seven", "Eight",
 "Nine", "Ten", "Jack", "Queen", "King"};

 deal(deck, face, suit); // deal the deck
}
```

```c
// shuffle cards in deck
void shuffle(unsigned int wDeck[][FACES])
{
    // for each of the cards, choose slot of deck randomly
    for (size_t card = 1; card <= CARDS; ++card) {
        size_t row; // row number
        size_t column; // column number

        // choose new random location until unoccupied slot found
        do {
            row = rand() % SUITS;
            column = rand() % FACES;
        } while(wDeck[row][column] != 0);

        // place card number in chosen slot of deck
        wDeck[row][column] = card;
    }
}

// deal cards in deck
void deal(const unsigned int wDeck[][FACES], const char *wFace[],
          const char *wSuit[])
{
    // deal each of the cards
    for (size_t card = 1; card <= CARDS; ++card) {
        // loop through rows of wDeck
        for (size_t row = 0; row < SUITS; ++row) {
            // loop through columns of wDeck for current row
            for (size_t column = 0; column < FACES; ++column) {
                // if slot contains current card, display card
                if (wDeck[row][column] == card) {
                    printf("%5s of %-8s", wFace[column], wSuit[row],
                           card % 2 == 0 ? '\n' : '\t'); // 2-column format
                }
            }
        }
    }
}
```

Fig. 7.24 | Card shuffling and dealing. (Part 2 of 2.)

|  |  |
|---|---|
| Nine of Hearts | Five of Clubs |
| Queen of Spades | Three of Spades |
| Queen of Hearts | Ace of Clubs |
| King of Hearts | Six of Spades |
| Jack of Diamonds | Five of Spades |
| Seven of Hearts | King of Clubs |
| Three of Clubs | Eight of Hearts |
| Three of Diamonds | Four of Diamonds |
| Queen of Diamonds | Five of Diamonds |

Fig. 7.25 | Sample run of card dealing program. (Part 1 of 2.)

|  |  |
|---|---|
| Six of Diamonds | Five of Hearts |
| Ace of Spades | Six of Hearts |
| Nine of Diamonds | Queen of Clubs |
| Eight of Spades | Nine of Clubs |
| Deuce of Clubs | Six of Clubs |
| Deuce of Spades | Jack of Clubs |
| Four of Clubs | Eight of Clubs |
| Four of Spades | Seven of Spades |
| Seven of Diamonds | Seven of Clubs |
| King of Spades | Ten of Diamonds |
| Jack of Hearts | Ace of Hearts |
| Jack of Spades | Ten of Clubs |
| Eight of Diamonds | Deuce of Diamonds |
| Ace of Diamonds | Nine of Diamonds |
| Four of Hearts | Deuce of Hearts |
| King of Diamonds | Ten of Spades |
| Three of Hearts | Ten of Hearts |

Fig. 7.25 | Sample run of card dealing program. (Part 2 of 2.)

## 7.12 Pointers to Functions

A pointer to a function contains the address of the function in memory. In Chapter 6, we saw that an array name is really the address in memory of the first element of the array. Similarly, a function name is really the starting address in memory of the code that performs the function's task. Pointers to functions can be passed to functions, returned from functions, stored in arrays and assigned to other function pointers.

### 7.12.1 Sorting in Ascending or Descending Order

To illustrate the use of pointers to functions, Fig. 7.26 presents a modified version of the bubble sort program in Fig. 7.15. The new version consists of main and functions bubble, swap, ascending and descending. Function bubbleSort receives a pointer to a function—either function ascending or function descending—as an argument, in addition to an integer array and the size of the array. The program prompts the user to choose whether the array should be sorted in ascending or in descending order. If the user enters 1, a pointer to function ascending is passed to function bubble, causing the array to be sorted into increasing order. If the user enters 2, a pointer to function descending is passed to function bubble, causing the array to be sorted into decreasing order. The output of the program is shown in Fig. 7.27.

```c
// Fig. 7.26: fig07_26.c
// Multipurpose sorting program using function pointers.
#include <stdio.h>
#define SIZE 10
```

Fig. 7.26 | Multipurpose sorting program using function pointers. (Part 1 of 3.)

```c
// prototypes
void bubble(int work[], size_t size, int (*compare)(int a, int b));
int ascending(int a, int b);
int descending(int a, int b);

int main(void)
{
    // initialize unordered array a
    int a[SIZE] = { 2, 6, 4, 8, 10, 12, 89, 68, 45, 37 };
    printf("%s", "Enter 1 to sort in ascending order\n" "Enter 2 to sort in descending order: ");
    int order; // 1 for ascending order or 2 for descending order
    scanf("%d", &order);

    puts("\nData items in original order");

    // output original array
    for (size_t counter = 0; counter < SIZE; ++counter) {
        printf("%5d", a[counter]);
    }

    // sort array in ascending order; pass function ascending as an
    // argument to specify ascending sorting order
    if (order == 1) {
        bubble(a, SIZE, ascending);
        puts("\nData items in ascending order");
    }
    else { // pass function descending
        bubble(a, SIZE, descending);
        puts("\nData items in descending order");
    }

    // output sorted array
    for (size_t counter = 0; counter < SIZE; ++counter) {
        printf("%5d", a[counter]);
    }

    puts("\n");
}

// multipurpose bubble sort; parameter compare is a pointer to
// the comparison function that determines sorting order
void bubble(int work[], size_t size, int (*compare)(int a, int b))
{
    void swap(int *element1Ptr, int *element2ptr); // prototype

    // loop to control passes
    for (unsigned int pass = 1; pass < size; ++pass) {
        // loop to control number of comparisons per pass
        for (size_t count = 0; count < size - 1; ++count) {
```

```c
// if adjacent elements are out of order, swap them
if ((*compare)(work[count], work[count + 1])) {
    swap(&work[count], &work[count + 1]);
}
}
}

// swap values at memory locations to which element1Ptr and
// element2Ptr point
void swap(int *element1Ptr, int *element2Ptr)
{
    int hold = *element1Ptr;
    *element1Ptr = *element2Ptr;
    *element2Ptr = hold;
}
```

```c
// determine whether elements are out of order for an ascending
// order sort
int ascending(int a, int b)
{
    return b < a; // should swap if b is less than a
}
```

```c
// determine whether elements are out of order for a descending
// order sort
int descending(int a, int b)
{
    return b > a; // should swap if b is greater than a
}
```

Fig. 7.26 | Multipurpose sorting program using function pointers. (Part 3 of 3.)

Enter 1 to sort in ascending order
Enter 2 to sort in descending order: 1

Data items in original order
    2   6   4   8  10  12  89  68  45  37
Data items in ascending order
    2   4   6   8  10  12  37  45  68  89

Enter 1 to sort in ascending order
Enter 2 to sort in descending order: 2

Data items in original order
    2   6   4   8  10  12  89  68  45  37
Data items in descending order
  89  68  45  37  12  10   8   6   4   2

Fig. 7.27 | The outputs of the bubble sort program in Fig. 7.26.

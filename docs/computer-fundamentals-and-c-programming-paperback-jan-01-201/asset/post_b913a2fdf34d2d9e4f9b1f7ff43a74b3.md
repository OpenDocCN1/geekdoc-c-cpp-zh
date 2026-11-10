
```c
/* array_search.c: Saves in an array some integers from the keyboard.
                Also sequentially searches the array. */
#include <stdio.h>
int main(void)
{
    int i = 0, imax, num, arr[128];
    char is_found;
    /* Input the integers */
    printf("Key in some integers (q to quit): ");
    while (scanf("%d", &arr[i++]) == 1)   /* Becomes 0 with non-digit */
        ;
    /* Remove the 'q' and other trailing characters from input */
    while (getchar() != '\n')
        ;
    imax = i - 1;                        /* Save i before it is reused */
    /* Search the array for a number */
    for (; printf("Integer to search (q to quit): "); ) {
        if (scanf("%d", &num) == 0)      /* When non-digit is input */
            break;
        is_found = 'n';                  /* Set default to 'n' */
        for (i = 0; i < imax; i++) {     /* Cycle through array elements */
            if (num == arr[i]) {         /* If number found in array ... */
                is_found = 'y';          /* ... abandon search */
                break;
            }
        }
        is_found == 'n' ? printf("%d not found\n", num) :
                          printf("%d stored in arr[%d]\n", num, i);
    }
    return 0;
}
```

| PROGRAM 10.8: array_search.c |
| :--- |
| Key in some integers (q to quit): 5 10 15 20 25 31 q<br>Enter an integer to search for: 20<br>20 stored in arr[3]<br>Enter an integer to search for: 21<br>21 not found<br>Enter an integer to search for: q |

**PROGRAM OUTPUT: array_search.c**

When using the binary search technique, we didn't need more than nine guesses to arrive at the number 67. On the other hand, a sequential search could require up to 100 guesses. We'll now understand the algorithm for binary search on arrays before developing a program that implements this algorithm.

### 10.10.1 The Binary Search Algorithm

Let’s search a sorted array *A* of *n* elements for the number *x*. Let *start* and *end* represent the two ends (indexes) of the search domain. Because this domain shrinks by half every time a search is made on the array, the *start* and *end* points progressively move closer to each other. The search algorithm thus involves the following steps:

- 1. Set the initial values of *start* to 1 and *end* to *n*.
- 2. Check whether *start* <= *end* in every iteration. If this condition fails, go to Step 7.
- 3. Set the mid-point of the search domain as *mid* = (*start* + *end*) / 2 and compare the value of *x* to *A*[*mid*].
- 4. If *x* < *A*[*mid*], the number belongs to the lower half of the range, which means that *end* has to be shifted to the left. Set *end* = *mid* - 1 and go to Step 2.
- 5. If *x* > *A*[*mid*], the number belongs to the upper half of the range, which means that *start* has to be shifted to the right. Set *start* = *mid* + 1 and go to Step 2.
- 6. If you have come here, it means that *x* = *A*[*mid*]. The search is successful and the algorithm is terminated.
- 7. If you have come here (from Step 2), the search is unsuccessful and the algorithm is terminated.

Every time we move to Step 2—either from Step 4 or Step 5—the difference between *start* and *end* shrinks. For a search to be successful, *start* must remain equal to or less than *end*. If *start* eventually exceeds *end*, it means that the search has failed. Since the search algorithm discards half of the data in every iteration, binary search is more efficient than sequential search, where efficiency is related to the number of iterations required to complete a lookup. We’ll consider some sample figures after we have discussed the next program.

### 10.10.2 binary_search.c: Implementation of the Algorithm

Program 10.9 is a simple implementation of the algorithm that was just discussed. It searches a sorted array of 10 elements that are initialized at the time of declaration. The program uses an outer *while* loop to repeatedly accept an integer from the keyboard, and then uses an inner *while* loop to perform a lookup of the array. For your benefit, the program prints the adjusted *start* and *end* points (SP and EP) in every iteration.

The first *if* construct inside the outer *while* loop validates num, the number that is input. Like some of the previous programs, this program also ends when the input is not a number. The *continue* statement in the *else-if* section prevents the remaining statements from being executed if the number falls outside the permitted range.

The binary search algorithm is implemented in the inner *while* loop. Before this loop is entered, the variables *start* and *end* are set to the first and last index of the array, respectively. Every iteration of the loop sets a new mid-point (mid) by averaging *start* and *end*. The element with mid as index is then compared to num, the search value. If this comparison fails in one iteration, either *start* or *end* is adjusted, bringing the two closer to each other. This also changes mid which thus moves closer to the search target.

The output shows how the start and end points are adjusted with every iteration. If the search eventually succeeds, the loop terminates abnormally using the **break** route. However, if the number doesn't exist in the array, the loop terminates normally because of the eventual failure of the control expression. Observe how the number 66 could be found in the first iteration itself, while both 22 and 87 needed four iterations before 22 was found but not 87.

```c
/* binary_search.c: Uses the binary search mechanism for searching a sorted
   array. Progressively narrows the search domain by
   adjusting the start and end points of search. */

#include <stdio.h>
#define SIZE 10
int main(void)
{
    short num, start, mid, end;
    short arr[SIZE] = {11, 22, 33, 44, 55, 66, 77, 88, 99, 110};

    /* Search the array for a number */
    while (printf("Integer to search (q to quit): ")) {
        if (scanf("%hd", &num) == 0)        /* When non-digit is input */
            break;
        else if (num < arr[0] || num > arr[SIZE - 1]) {
            printf("Number outside range\n");
            continue;
        }

        start = 0; end = SIZE;
        while (start <= end) {
            mid = (start + end) / 2;
            printf("(SP: %hd, EP: %hd) ", start, end);

            if (arr[mid] < num)
                start = mid + 1;                /* Advance the start point */
            else if (arr[mid] > num)
                end = mid - 1;                  /* Move back the end point */
            else
                break;                          /* Search successful ... */
                                                /* ... array index = mid */
        }

        /* We now know whether the search was successful or not */
        if (arr[mid] == num)                    /* From previous break */
            printf("\nNumber found at index %hd\n", mid);
        else
            printf("\nNumber not found\n");     /* From normal loop termination */
    }

    return 0;
}
```

**PROGRAM 10.9: binary_search.c**

```
Integer to search (q to quit): -10
Number outside range
Integer to search (q to quit): 22
[SP: 0, EP: 10]  [SP: 0, EP: 4]  [SP: 0, EP: 1]  [SP: 1, EP: 1]
Number found at index 1
Integer to search (q to quit): 66
[SP: 0, EP: 10]
Number found at index 5
Integer to search (q to quit): 33
[SP: 0, EP: 10]  [SP: 0, EP: 4]
Number found at index 2
Integer to search (q to quit): 87
[SP: 0, EP: 10]  [SP: 6, EP: 10]  [SP: 6, EP: 7]  [SP: 7, EP: 7]
Number not found
Integer to search (q to quit): q
```

**PROGRAM OUTPUT: binary_search.c**

Using the binary search technique, we needed a maximum of four iterations to complete a lookup of an array of 10 elements. The corresponding figure for a sequential search is 10. The power of binary search can be assessed from the following rule:

> *The number of iterations needed to search a sorted array of n elements is the number of bits needed to represent n in binary.*

Thus, a 1000-element array needs 10 iterations (compared to 1000 for sequential search). The gulf between the two widens as the size of the array increases, showing how enormously efficient binary search can be. Now think of this: a sorted array of 4 billion elements can be searched in only 32 iterations!

**Note:** The array must be sorted for binary search to work.

## 10.11 `count_chars.c`: FREQUENCY COUNT OF DATA ITEMS

We often need to know the frequency of occurrence of each item in the data. For instance, a calligraphist may like to know the usage of letters in a text book. A demographic expert may want to study the age-wise distribution of people. A weather expert may like to know the number of days a city has experienced humidity exceeding 90%. These tasks can’t be handled by variables because you need too many of them. Arrays are useful counting devices and can handle these jobs easily.

A single array can count the frequency of occurrence of several quantities using one of two techniques. The simplest implementation uses the quantity itself as the index of the array (provided it is integral and positive). Whenever this quantity occurs in the data, the program merely increments the element having that quantity as the index. The other technique is to use a two-dimensional array to store both the number and its count. The following program uses the first technique and Section 10.13 examines the second one.

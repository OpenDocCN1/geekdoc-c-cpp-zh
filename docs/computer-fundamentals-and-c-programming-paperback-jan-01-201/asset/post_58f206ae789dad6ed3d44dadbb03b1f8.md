
digit-letter from digits. For instance, if remainder is 15 from a division by 16, digits[remainder] is 'F'. This value is stored in digit_arr, which is finally reversed by the second for loop. The last for loop simply reads this converted array.

```c
/* decimal2anybase.c: Extends decimal2binary.c to convert a number to any base.
   Reverses an array without using a second one. */
#include <stdio.h>
int main(void)
{
    char digit_arr[80];
    char digits[16] = {'0','1','2','3','4','5','6','7','8','9',
                       'A','B','C','D','E','F'};
    short i, j, imax, temp, base, remainder;
    long quotient;

    printf("Enter number to convert and base: ");
    scanf("%ld%hd", &quotient, &base);
    for (i = 0; quotient > 0; i++) {      /* Divide repeatedly */
        remainder = quotient % base;
        quotient /= base;
        digit_arr[i] = digits[remainder];   /* Select digit from array */
    }
    imax = i;                              /* Number of digits to be printed */

    /* Reverse the array before printing the digits */
    for (i = 0, j = imax - 1; i < imax / 2; i++, j--) {
        temp = digit_arr[i];
        digit_arr[i] = digit_arr[j];
        digit_arr[j] = temp;
    }
    for (i = 0; i < imax; i++)
        printf("%c ", digit_arr[i]);
    return 0;
}
```

|  |  |  |
|---|---|---|
| PROGRAM 10.6: **decimal2anybase.c** |  |  |
| Enter number to convert and base: **12 2**<br>1 1 0 0 |  | 2³ + 2² = 12 |
| Enter number to convert and base: **127 2**<br>1 1 1 1 1 1 1 |  | Seven 1s—127 |
| Enter number to convert and base: **255 8**<br>3 7 7 |  | 3 × 8² + 7 × 8¹ + 7 × 8⁰ = 255 |
| Enter number to convert and base: **255 16**<br>F F |  | 15 × 16¹ + 15 × 16⁰ = 255 |

PROGRAM OUTPUT: **decimal2anybase.c**

## 10.8 SORTING AN ARRAY (SELECTION)

Sorting refers to the ordering of data in ascending or descending sequence. Large lists like a telephone directory must be sorted for them to be useful. Arrays are often sorted either to present information in a specified sequence or to fulfill a requirement of other operations (like a search). The technique used in sorting numbers is different from the one used in sorting strings. In this section, we'll discuss the theory and programming techniques related to the sorting of numeric data. Sorting of character strings is examined in Chapter 13.

There are several algorithms for sorting arrays. Three of the common ones are known as *bubble sort*, *selection sort* and *insertion sort*. Because they have some common features, knowledge of one algorithm will help you understand the others. In this section, we'll examine the algorithm for selection sort before we develop a program that implements this algorithm.

Consider a numeric array, arr, which needs to be sorted in ascending order. Sorting is done by repeatedly scanning the array in multiple passes, where the start point of each pass progressively moves from arr[0] to arr[1], arr[2], and so forth. If a number is found to be lower than the start element of that pass, then the two numbers are interchanged. Thus, at the end of each pass, the start element has the lowest number among the elements encountered in that pass. A total of n - 1 passes are required for an array of n elements, where each pass encounters one fewer element compared to its previous pass.

Let's now implement this algorithm in Program 10.7, which sorts a set of integers input from the keyboard. The sorting operation is carried out with a nested `for` loop. The outer loop determines the start point of each pass, while the inner loop scans the elements following the start element. We'll examine the exact sequence of events that occur in the first two iterations and the last iteration of the outer loop.

### Outer loop: First iteration

The outer loop begins the scan by selecting the first element as the start point (i = 0). Next, the inner loop scans all remaining elements starting from the second element (j = i + 1). In each iteration, it compares the value of the scanned element to the start element and interchanges them if the start element is greater than the other. For this purpose, it makes use of the temporary variable, tmp. After the inner loop has completed its scan, control reverts to the outer loop for the second iteration.

### Outer loop: Second iteration

The outer loop now selects the second element as the start point (i = 1). The inner loop now performs the scan for all elements except the first and second (j = 2), comparing each element to the second element and interchanging them if the relational test is satisfied.

### Outer and inner loops: Last iteration

With every iteration of the outer loop, the start point progressively shifts from the first element to the one preceding the last element. At this point, the inner loop iterates only once by comparing this element to the last one and interchanging if necessary. Both loops have now completed their run and the sort action has been completed.

For your benefit, the program contains an additional `for` loop which prints the contents of the array after the inner `for` loop completes a single pass. The output shows how each pass moves the lowest number encountered in that pass to the left. Eventually, the last line of diagnostic output shows a sorted array in place.

```c
/* sort_selection.c: Sorts a one-dimensional array using a nested for loop.
   Algorithm used: selection sort. */
#include <stdio.h>
int main(void)
{
    short i, j, k, imax, tmp;
    short arr[100];

    printf("Key in some integers (q to quit): ");
    for (i = 0; scanf("%hd", &arr[i]) == 1; i++)
        ;

    printf("Status of array after each iteration ...\n");
    imax = i;                         /* Number of elements used */
    for (i = 0; i < imax - 1; i++) {  /* Last element not considered */
        for (j = i + 1; j < imax; j++) /* Scanning remaining elements */
            if (arr[i] > arr[j]) {     /* If start element is larger ... */
                tmp = arr[i];
                arr[i] = arr[j];       /* ... interchange the ... */
                arr[j] = tmp;          /* ... elements */
            }

        /* This for loop displays the array contents after each pass.
           You can remove it after you have understood selection sort. */
        for (k = 0; k < imax; k++)     /* Displaying progress */
            printf("%3hd", arr[k]);
        printf("\n");
    }

    printf("Final sorted output ...\n");
    for (i = 0; i < imax; i++)
        printf("%3hd", arr[i]);
    printf("\n");
    return 0;
}
```

### PROGRAM 10.7: **sort_selection.c**

```text
Key in some integers (q to quit): 55 4 27 1 66 34 11 q
Status of array after each iteration ...
  1 55 27 4 66 34 11
  1  4 55 27 66 34 11
  1  4 11 55 66 34 27
  1  4 11 27 66 55 34
  1  4 11 27 34 66 55
  1  4 11 27 34 55 66
Final sorted output ...
  1  4 11 27 34 55 66
```

PROGRAM OUTPUT: **sort_selection.c**

**Note:** Since a character string doesn’t have a numeric value (even though its individual characters have), sorting a set of strings is based on a different principle altogether. Starting with the first character, the ASCII value of each character of *string1* is compared to its peer in *string2*. The sort stops when the first mismatch occurs. We need to use `strcmp` (a string-handling function) to make this comparison, so the topic will be visited in Chapter 13.

## 10.9 `array_search.c`: PROGRAM TO SEQUENTIALLY SEARCH AN ARRAY

Searching is a common operation performed on arrays. We often search an array for a number. Depending on the application, we may ignore this number or increment a counter if the number exists in the array. If it doesn’t exist, we may add the number to the array. The simplest search technique sequentially scans all array elements and terminates the search when a match is found. A more efficient technique uses a sorted array to conduct a binary search. Both techniques are discussed in this chapter.

Program 10.8 sequentially searches an array that can hold up to 128 integers. A user first keys in a number of integers before searching the array for a particular integer. In case a match is found, the program prints the array element along with the index. This technique is adequate for small arrays.

With `scanf` running in a loop, a set of six integers are keyed in before the input is terminated with q. Using the notation `&arr[i++]`, `scanf` saves these integers in the array `arr`. `getchar` then performs its usual cleanup job to get rid of the q and other non-numeric characters that may remain in the system buffer.

Next, a search routine runs in a nested for loop to search this array for another user-input integer. If a match is found, the variable `is_found` is set to 'y' and the inner loop is terminated with `break`. If no match is found, the loop terminates normally and `is_found` remains unchanged at 'n'. Control in either case moves down to the conditional expression which evaluates the status of `is_found` and selects the appropriate `printf` expression. The next iteration of the outer loop then prompts the user for another integer.

## 10.10 BINARY SEARCH

Sequential search is slow and is acceptable only for searching small arrays. When working with large data volumes, we need to use the *binary search* mechanism. In this scheme, the array is sorted before it is subjected to a search. A binary search halves the search domain every time it is invoked. The number of loop iterations needed is thus reduced, making binary search more efficient than sequential search. Every serious programmer should understand this search mechanism and know how to implement it in their programs.

The principle used in binary search is simple, and you may have already used it in a number guessing game. You ask a person to guess a number between 1 and 100. You then compute the mid-point of this range (50), and then ask whether the number lies in the lower or upper half of the range. The next question halves the selected range even further, and in only a few guesses, the range reduces to a single number—the one that was guessed. The range could typically follow this progression:

`1–100,  50–100,  50–75,  63–75,  63–69,  66–69,  66–68,  67–68,  67`

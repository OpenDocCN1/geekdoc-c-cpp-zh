
- 60
- 26
- 55
- 34
- 28

The numbers in sorted order

26
28
34
42
55
60

In effect, binary search splits the array in half and then repeats the algorithm on the half that must contain the value that it is searching for, if it is there at all.

## Binary searching

The drawbacks of sequential search can be eliminated if it becomes possible to eliminate large portions of the list from consideration in subsequent iterations. The binary search method does just that; it halves the size of the list to search in each iteration.

Binary search can be explained simply by the analogy of searching for a page in a book. Suppose a reader is searching for page 90 in a book of 150 pages. The reader would first open the book at random towards the latter half of the book. If the page number is less than 90, the reader would open at a page to the right; if it is greater than 90, the reader would open at a page to the left, repeating the process till page 90 was found. As can be seen, by the first instinctive search, the reader dramatically reduced the number of pages to be searched.

Binary search requires sorted data to operate on, since the data may not be contiguous like the pages of a book. It is not possible to guess in which quarter of the data set the required item may be. So, the array is divided in the centre each time.

Binary search will first be illustrated with an example before going on to formulate the algorithm and analysing it.

- In binary search, implement the following procedure:
  - Look at the middle element of the list.
  - If it is the value being searched, then the job is done.
  - If the value that is being searched is smaller than the middle element, then continue with the bottom half of the list.
  - If the value that is being searched is larger than the middle element, then continue with the top half of the list.

### EXAMPLE

- 2. Consider the array

1 2 3 4 5 6 7 8 9

Construct the binary search algorithm for finding the Key = 7.

*1st iteration*

HIGH = 8, LOW = 0; because the array index begins with ‘0’ and ends with ‘8’
MID = 4, Array[4] = 5, 5<7 : TRUE
LOW = 5
New List = 6 7 8 9

*2nd iteration*

HIGH = 8, LOW = 5
MID = 6, Array[6] = 7, 7<7 : FALSE
HIGH = 6
New List = 6 7

*3rd iteration*

HIGH = 6, LOW = 5
MID = 5, Array[5] = 6, 6<7 : TRUE
LOW = 6
New List = 7

*4th iteration*

HIGH = 6, LOW = 6
MID = 6, Array[MID] = Array[6] = 7 == Key
then Found = TRUE

**Tabular illustration** Table 11.1 shows an example of the operation of the binary search algorithm. The rows of the table, starting from the top, are the array indices, the data stored at the indexed location, and the index values used for high (H), low (L), and middle (M) at each iteration of the algorithm. If the target value is 52, its location is found in the third iteration.

**Implementation of binary search algorithm** This represents the binary search method to find a required item in a list sorted in increasing order.

**Table 11.1 Depiction of binary search algorithm**

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Data | 23 | 27 | 29 | 32 | 34 | 41 | 46 | 47 | 49 | 52 | 55 | 68 | 71 | 74 | 77 | 78 |
| 1st iteration | L |  |  |  |  |  | M |  |  |  |  |  |  |  |  | H |
| 2nd iteration |  |  |  |  |  |  |  | L |  |  |  | M |  |  |  | H |
| 3rd iteration |  |  |  |  |  |  |  | L | M | H |  |  |  |  |  |  |

### EXAMPLE

- 3. Sort an array LIST of size N and find the position of the target value T.

**Algorithm:** The algorithm determines the position of T in the LIST.

- 1. START
- 2. PRINT “ENTER THE NO. OF ELEMENTS IN THE ARRAY”
- 3. INPUT N
- 4. I=0
- 5. PRINT “ENTER ARRAY ELEMENT IN ASCENDING ORDER”
- 6. INPUT LIST(I)
- 7. I=I+1
- 8. IF I<N THEN GOTO STEP 5
- 9. PRINT “ENTER THE ELEMENT TO SEARCH”
- 10. INPUT T
- 11. HIGH = N - 1
- 12. LOW = 0
- 13. FOUND = 0
- 14. MID = (HIGH + LOW) / 2
- 15. IF T = LIST[MID]
      FOUND = 1
      ELSE IF T < LIST[MID]
          HIGH = MID-1
      ELSE
          LOW = MID+1
- 16. IF (FOUND =0) and (HIGH >= LOW) THEN GOTO STEP 14
- 17. IF FOUND =0 THEN PRINT “NOT FOUND”
- 18. ELSE PRINT “FOUND AT”, MID.
- 19. STOP

The C program for this algorithm is as follows:

```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int a[30],n,i,t,low,mid,high,found=0;
    printf("\n Enter the NO. of elements in the array:");
    scanf("%d",&n);
    if(n>30)
    {
        printf("\n Too many Numbers");
        exit(0);
    }
    printf("\n Enter the elements of the array:");
    for(i=0; i < n; i++)
        scanf("%d", &a[i]);
    printf("\n Enter the element to search :");
    scanf("%d",&t);
    low = 0;
    high = n - 1;
    while(high >= low)
    {
        mid = (low + high) / 2;
        if(a[mid] == t)
        {
            found = 1;
            break;
        }
        else if (t < a[mid])
            high = mid - 1;
        else
            low = mid + 1;
    }
    if(found==0)
        printf("\n NOT FOUND");
    else
        printf("\n FOUND AT %d",mid);
    return 0;
}
```

### Output

```text
Enter the number of elements in the array: 9
Enter the elements of the array:
1
2
3
4
5
6
7
8
9
Enter the element to search: 7
FOUND AT 6
Enter the number of elements in the array 9
Enter the elements of the array:
1
2
3
4
5
6
7
8
9
Enter the element to search: 11
NOT FOUND
```

Here is a slightly bigger example on the use of arrays. Suppose one wants to investigate the behaviour of rolling a pair of dice. The total roll value can range from 2 to 12, and how often each roll comes up is to be counted. An array is to be used to keep track of the counts: a[2] will count how many times 2 have been rolled, etc.

The simulation of a roll of a dice is done by calling C’s random number generation function, rand(). Each time rand() is called, it returns a different, pseudo-random integer. The values that rand() returns typically span a large range, so C’s modulus (or remainder) operator % will be used to produce random numbers in the required range. The expression rand() % 6 produces random numbers in the range 0 to 5, and rand() % 6 + 1 produces random numbers in the range 1 to 6.

```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int i;
    int d1, d2;
    int a[13]; /* uses [2..12] */
    for(i = 2; i <= 12; i = i + 1)
        a[i] = 0;

    for(i = 0; i < 100; i = i + 1)
    {
        d1 = rand() % 6 + 1;
        d2 = rand() % 6 + 1;
        a[d1 + d2] = a[d1 + d2] + 1;
    }
    for(i = 2; i <= 12; i = i + 1)
        printf("%d: %d\n", i, a[i]);
    return 0;
}
```

The header `<stdlib.h>` has to be included because it contains the necessary declarations for the rand() function. The array of size 13 has to be declared so that its highest element will be a[12]. Space for a[0] and a[1] will be wasted; this is no great loss. The variables d1 and d2 contain the roll values of the two individual dice; they are added together to decide which cell of the array to increment in the line `a[d1 + d2] = a[d1 + d2] + 1;`

After 100 rolls, the array is printed out. Typically, mostly 7’s are seen as output, and relatively few 2’s and 12’s. However, using the % operator to reduce the range of the rand() function is not always a good idea.

## Check Your Progress

- 1. Given the array declaration

    ```c
    int myArray[] = {0, 2, 4, 6, 8, 10};
    ```

    What is the value of `myArray[myArray[2]]`?

    **Output 8**

- 2. `#include <stdio.h>`

    ```c
    main()
    {
        float a[10];
        printf("%d", sizeof(a));
    }
    ```

    What is the output of this program?

    **Output 40**

- 3. `#include <stdio.h>`

    ```c
    main()
    {
        int a[5], i;
        for(i=0; i<5; ++i)
            printf("%d", a[i]);
    }
    ```

    What is the output of this program?

    **Output Garbage**

- 4. An array has been declared as `int a[] = {1, 2, 3, 4, 5, ...};` How can you find the number of elements (i.e., size) of the array without manually counting them?

    **Output** `printf("%d", sizeof(a)/sizeof(a[0]));`

## Points

- Single operations, which involve entire arrays, are not permitted in C.
- Neither can all elements of an array be set at once nor can one array be assigned to another.
- For an array of length L and data type X, the compiler allocates L * sizeof(X) bytes of contiguous space in memory.
- It is not possible to declare an array using a variable for the size.

## 11.3 STRINGS: ONE-DIMENSIONAL CHARACTER ARRAYS

Strings in C are represented by arrays of characters. The end of the string is marked with a special character, the null character, which is a character whose bits are all zero, i.e., a NUL (not a NULL). (The null character has no relation except in name to the null pointer. In the ASCII character set, the null character is named NUL.) The null or string-terminating character is represented by another character escape sequence, \0.

Although C does not have a string data type, it allows string constants. For example, “hello students” is a string constant.

### 11.3.1 Declaration of a String

Strings can be declared like one-dimensional arrays. For example,

```c
char str[30];
char text[80];
```

illustrates this feature.

### 11.3.2 String Initialization

Character arrays or strings allow a shorthand initialization, for example,

```c
char str[9] = "I like C";
```

which is the same as

```c
char str[9] = {'I',' ','l','i','k','e',' ','C','\0'};
```

Whenever a string, enclosed in double quotes, is written, C automatically creates an array of characters containing that

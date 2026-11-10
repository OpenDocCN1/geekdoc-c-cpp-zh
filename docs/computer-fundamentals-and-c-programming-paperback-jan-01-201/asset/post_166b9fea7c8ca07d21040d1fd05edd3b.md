
```c
/* insert_element.c: Inserts element at specified location in an array. */
#include <stdio.h>
int main (void)
{
    short i, j, num, new_value, arr[20];

    printf("Number of integers to input? ");
    scanf("%hd", &num);

    printf("Key in %hd numbers: ", num);
    for (i = 0; i < num; i++)
        scanf("%hd", &arr[i]);

    printf("Enter desired index at insertion and inserted value: ");
    scanf("%hd%hd", &j, &new_value);

    /* Section for shifting elements to right and insertion of element */
    for (i = num; i > j; i--)            /* arr[num] is last element plus one */
        arr[i] = arr[i - 1];              /* Moves a group of elements to right */
    arr[i] = new_value;                   /* Inserts new value at index j */

    for (i = 0; i <= num; i++)            /* Now <= because of an extra element */
        printf("%hd ", arr[i]);
    return 0;
}
```

PROGRAM 10.3: **insert_element.c**

```text
Number of integers to input? 6
Key in 6 numbers: 11 22 33 55 66 77
Enter desired index at insertion and inserted value: 3 44
11 22 33 44 55 66 77
```

PROGRAM OUTPUT: **insert_element.c**

### 10.5.2  `delete_element.c`: Deleting an Element from an Array

Deletion of an element is equally simple and can be achieved with a similar but inverse line of reasoning. Just move to the specified location as before, and then shift to the left all elements from that location to the end of the array. Program 10.4 achieves this task. This time we use the technique discussed in Section 10.4 which populates an array without knowing the number of elements needed. This program too is well-documented, so no further explanation is provided.

Large arrays are often sorted for faster access. Insertion and deletion of elements in a sorted array require additional programming effort. Because a user can’t specify the insertion or deletion point for a sorted array, the program has to locate it. After you have learned to search an array, these tasks will be within your grasp.

```c
/* delete_element.c: Deletes element at specified location in an array. */
#include <stdio.h>
int main (void)
{
    short i, j, num, arr[20];
    printf("Key in numbers and press [Ctrl-d]:\n");
    num = 0;
    while (scanf("%hd", &arr[num]) == 1)
        num++;                        /* Number of items read = num */
    printf("\nEnter index at deletion point: ");
    scanf("%hd", &j);
    for (i = j; i < num - 1; i++)     /* Now num - 1 because of deleted element */
        arr[i] = arr[i + 1];          /* Moves a group of elements to left */
    for (i = 0; i < num - 1; i++)
        printf("%hd ", arr[i]);
    return 0;
}
```

PROGRAM 10.4: delete_element.c

```text
Key in numbers and press [Ctrl-d]:
11 22 33 44 55 66 77
[Ctrl-d] or [Ctrl-z]
Enter index at deletion point: 3
11 22 33 55 66 77
```

PROGRAM OUTPUT: delete_element.c

## 10.6 REVERSING AN ARRAY

This section discusses two techniques of reversing an array. This is easily achieved with two arrays, but since large arrays can take up a lot of space, we must also be able to perform the task using a single array. Both techniques are discussed in the following sections.

### 10.6.1 Reversing with Two Arrays

The simplest method of reversing the contents of an array is to use a second array to hold the new values. The sequence goes like this: read the first element of array1 and save it to the last element of array2, save the next element of array1 to the one previous to the last element of array2, and so on. This simple code segment does the job:

```c
short i, size = 7, brr[7];
short arr[] = {1, 3, 6, 9, 11, 22, 5};
for (i = 0; i < size; i++)            /* Reversing array */
    brr[size - 1 - i] = arr[i];
for (i = 0; i < size; i++)                  /* Printing reversed array */
    printf("%d ", brr[i]);
```

OUTPUT: 5 22 11 9 6 3 1

In this and the next example, we have chosen to use a variable (size) to store the number of elements of the array. A serious programmer, however, will use **#define SIZE 7** instead. Since this size is one more than the value of the last subscript, we need to subtract one from it before assigning an element of the first array to the second array.

### 10.6.2  Reversing with a Single Array

An array of *n* elements can be reversed without using a second array. This technique uses an intermediate variable to reverse the first and *n*th (last) element, the second and (*n* − 1)th element, and so on. This process is carried out *n* / 2 times. If *n* is even, the exchange is completed for all elements, but if *n* is odd, the middle element is unaffected. This is the case anyway, so program logic doesn’t depend on whether *n* is even or odd. The following code does the job:

```c
short i, j, temp, size = 7;
short arr[7] = {1, 3, 6, 9, 11, 22, 5};
for (i = 0, j = size - 1; i < (size / 2); i++, j--) {
    temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
for (i = 0; i < size; i++)                  /* Printing reversed array */
    printf("%d ", arr[i]);
```

OUTPUT: 5 22 11 9 6 3 1

The comma operator in *exp1* and *exp3* of the combined expression of the first **for** loop is responsible for the lean loop body. This loop swaps two values using *temp* as the intermediate variable. The subscript *i* is incremented from 0 to (*size* - 1) / 2, while *j* is simultaneously decremented from the last subscript (*size* - 1). The original array is, however, lost in the process. Because this technique saves memory, we’ll henceforth use it for any job related to array reversal.

## 10.7  TWO PROGRAMS REVISITED

Some of the previous programs used a loop to generate one or more values in every iteration. Because all of these values couldn’t be saved, action on each value was taken the moment it was generated and before the next iteration could begin. Now that we have an array to store all values, we can use these values even *after* the loop has completed execution. Let us now revisit two of these programs to make them flexible enough to handle multiple requirements.

### 10.7.1  extract_digits2.c: Saving Digits of an Integer

Program 10.5 is an improvement over its predecessor (Program 8.3), which extracts the digits from an integer. This program, however, stores all extracted digits in an array and then reverse-reads the array to print the digits in the normal sequence. With minor modifications to the code, you can manipulate these digits in any manner you want. You can print them in any sequence, add or multiply them.

```c
/* extract_digits2.c: Modifies a previous program to save the digits of an
                        integer in an array for manipulation in any manner. */
#include <stdio.h>
int main(void)
{
    unsigned int number;
    short i = 0, digit_arr[10];

    printf("Key in an integer: ");
    scanf("%d", &number);
    while (number != 0) {
        digit_arr[i++] = number % 10;         /* Saves last digit */
        number = number / 10;                 /* Removes last digit */
    }
    i--;
    while (i >= 0)                            /* Printing the digits ... */
        printf("%hd ", digit_arr[i--]);       /* ... in normal sequence */
    printf("\n");

    return 0;
}
```

PROGRAM 10.5: **extract_digits2.c**

```text
Key in an integer: 1357926
1 3 5 7 9 2 6
```

PROGRAM OUTPUT: **extract_digits2.c**

### 10.7.2  decimal2anybase.c: Converting from Decimal to Any Base

The concepts behind the reversal of an array can be gainfully employed in the task of converting a number from one base to another. In Chapter 8, decimal-to-binary conversion was attempted twice by reverse-reading an array of remainders. Program 10.6 extends the scope by converting from decimal to any base not exceeding 16. Instead of reverse-reading an array, the program reverses the array itself using the technique discussed previously.

The program uses two arrays of type char. digit_arr stores the remainders and digits stores the character representation of all hex digits. For decimal and octal numbers, the program needs to use only the first 10 and 8 elements, respectively, of this array.

The number to be converted and the required base are first taken from user input. This number is repeatedly divided by the base. Using remainder as subscript, the program extracts the appropriate

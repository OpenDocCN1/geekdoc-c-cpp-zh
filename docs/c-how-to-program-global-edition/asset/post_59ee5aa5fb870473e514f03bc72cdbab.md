
## Common Programming Error 6.5

Referring to an element outside the array bounds.

## Error-Prevention Tip 6.1

When looping through an array, the array index should never go below 0 and should always be less than the total number of elements in the array (size − 1). Make sure the loop-continuation condition prevents accessing elements outside this range.

## Error-Prevention Tip 6.2

Programs should validate the correctness of all input values to prevent erroneous information from affecting a program's calculations.

## 6.4.6 Graphing Array Element Values with Histograms

Our next example (Fig. 6.8) reads numbers from an array and graphs the information in the form of a bar chart (or histogram)—each number is printed, then a bar consisting of that many asterisks is printed beside the number. The nested for statement (lines 18–20) draws the bars. Note the use of puts("") to end each histogram bar (line 22).

```c
// Fig. 6.8: fig06_08.c
// Displaying a histogram.
#include <stdio.h>
#define SIZE 5

// function main begins program execution
int main(void)
{
    // use initializer list to initialize array n
    int n[SIZE] = {19, 3, 15, 7, 11};

    printf("%s%13s%17s\n", "Element", "Value", "Histogram");

    // for each element of array n, output a bar of the histogram
    for (size_t i = 0; i < SIZE; ++i) {
        printf("%7u%13d ", i, n[i]);
        for (int j = 1; j <= n[i]; ++j) { // print one bar
            printf("%c", '*');
        }
    }

    puts(""); // end a histogram bar with a newline
}
```

| Element | Value | Histogram |
|---|---|---|
| 0 | 19 | ******************* |
| 1 | 3 | *** |
| 2 | 15 | *************** |
| 3 | 7 | ******* |
| 4 | 11 | *********** |

Fig. 6.8 | Displaying a histogram.

capability we have is outputting a string with printf. A string such as "hello" is really an array of individual characters in C.

### 6.5.1 Initializing a Character Array with a String

Character arrays have several unique features. A character array can be initialized using a string literal. For example,

```
char string1[] = "first";
```

initializes the elements of array string1 to the individual characters in the string literal "first". In this case, the size of array string1 is determined by the compiler based on the length of the string. The string "first" contains five characters plus a special string-termination character called the null character. Thus, array string1 actually contains six elements. The escape sequence representing the null character is '\0'. All strings in C end with this character. A character array representing a string should always be defined large enough to hold the number of characters in the string and the terminating null character.

### 6.5.2 Initializing a Character Array with an Initializer List of Characters

Character arrays also can be initialized with individual character constants in an initializer list, but this can be tedious. The preceding definition is equivalent to

```
char string1[] = {'f', 'i', 'r', 's', 't', '\0'};
```

### 6.5.3 Accessing the Characters in a String

Because a string is really an array of characters, we can access individual characters in a string directly using array index notation. For example, string1[0] is the character 'f' and string1[3] is the character 's'.

### 6.5.4 Inputting into a Character Array

We also can input a string directly into a character array from the keyboard using scanf and the conversion specifier %s. For example,

```
char string2[20];
```

creates a character array capable of storing a string of at most 19 characters and a terminating null character. The statement

```
scanf("%19s", string2);
```

the end of the array string2. (In Section 6.13, we revisit the potential security issue raised by inputting into a character array and discuss the C standard's scanf_s function.) It's your responsibility to ensure that the array into which the string is read is capable of holding any string that the user types at the keyboard. Function scanf does not check how large the array is. Thus, scanf can write beyond the end of the array.

### 6.5.5 Outputting a Character Array That Represents a String

A character array representing a string can be output with printf and the %s conversion specifier. The array string2 is printed with the statement

```
printf("%s\n", string2);
```

Function printf, like scanf, does not check how large the character array is. The characters of the string are printed until a terminating null character is encountered. [Consider what would print if, for some reason, the terminating null character were missing.]

### 6.5.6 Demonstrating Character Arrays

Figure 6.10 demonstrates initializing a character array with a string literal, reading a string into a character array, printing a character array as a string and accessing individual characters of a string. The program uses a for statement (lines 22–24) to loop through the string1 array and print the individual characters separated by spaces, using the %c conversion specifier. The condition in the for statement is true while the counter is less than the size of the array and the terminating null character has not been encountered in the string. In this program, we read only strings that do not contain whitespace characters. We'll show how to read strings with whitespace characters in Chapter 8. Notice that lines 17–18 contain two string literals separated only by whitespace. The compiler automatically combines such string literals into one—this is helpful for making long string literals more readable.

```
1 // Fig. 6.10: fig06_10.c
2 // Treating character arrays as strings.
3 #include <stdio.h>
4 #define SIZE 20
5 
6 // function main begins program execution
7 int main(void)
8 {
9     char string1[SIZE]; // reserves 20 characters
10    char string2[] = "string literal"; // reserves 15 characters
11
12    // read string from user into array string1
13    printf("%s", "Enter a string (no longer than 19 characters): ");
14    scanf("%19s", string1); // input no more than 19 characters
15
16    // output strings
17    printf("string1 is: %s\nstring2 is: %s\n"
18    "string1 with spaces between characters is:\n",
19    string1, string2);
```

Fig. 6.10 | Treating character arrays as strings. (Part I of 2.)

// Fig. 6.11: fig06_11.c
// Static arrays are initialized to zero if not explicitly initialized.
#include <stdio.h>

void staticArrayInit(void); // function prototype
void automaticArrayInit(void); // function prototype

// function main begins program execution
int main(void)
{
    puts("First call to each function:");
    staticArrayInit();
    automaticArrayInit();

    puts("\n\nSecond call to each function:");
    staticArrayInit();
    automaticArrayInit();
}

// function to demonstrate a static local array
void staticArrayInit(void)
{
    // initializes elements to 0 before the function is called
    static int array1[3];

    puts("\nValues on entering staticArrayInit:");

    // output contents of array1
    for (size_t i = 0; i < 2; ++i) {
        printf("array1[%u] = %d ", i, array1[i]);
    }

    puts("\nValues on exiting staticArrayInit:");

    // modify and output contents of array1
    for (size_t i = 0; i < 2; ++i) {
        printf("array1[%u] = %d ", i, array1[i] += 5);
    }
}

// function to demonstrate an automatic local array
void automaticArrayInit(void)
{
    // initializes elements each time function is called
    int array2[3] = {1, 2, 3};

    puts("\n\nValues on entering automaticArrayInit:");

    // output contents of array2
    for (size_t i = 0; i < 2; ++i) {
        printf("array2[%u] = %d ", i, array2[i]);
    }
}

```
54 puts("\nValues on exiting automaticArrayInit:");

56 // modify and output contents of array2
57 for (size_t i = 0; i < 2; ++i) {
58 printf("array2[%u] = %d ", i, array2[i] += 5);
59 }
60 }
```

First call to each function:
Values on entering staticArrayInit:
array1[0] = 0 array1[1] = 0 array1[2] = 0
Values on exiting staticArrayInit:
array1[0] = 5 array1[1] = 5 array1[2] = 5

Values on entering automaticArrayInit:
array2[0] = 1 array2[1] = 2 array2[2] = 3
Values on exiting automaticArrayInit:
array2[0] = 6 array2[1] = 7 array2[2] = 8

Second call to each function:
Values on entering staticArrayInit:
array1[0] = 5 array1[1] = 5 array1[2] = 5 — values preserved from last call
Values on exiting staticArrayInit:
array1[0] = 10 array1[1] = 10 array1[2] = 10

Values on entering automaticArrayInit:
array2[0] = 1 array2[1] = 2 array2[2] = 3 — values reinitialized after last call
Values on exiting automaticArrayInit:
array2[0] = 6 array2[1] = 7 array2[2] = 8

Fig. 6.11 | Static arrays are initialized to zero if not explicitly initialized. (Part 2 of 2.)

## 6.7 Passing Arrays to Functions

To pass an array argument to a function, specify the array's name without any brackets. For example, if array hourlyTemperatures has been defined as

```
int hourlyTemperatures[HOURS_IN_A_DAY];
```

the function call

```
modifyArray(hourlyTemperatures, HOURS_IN_A_DAY)
```

passes array hourlyTemperatures and its size to function modifyArray.

Recall that all arguments in C are passed by value. C automatically passes arrays to functions by reference (again, we'll see in Chapter 7 that this is not a contradiction)—the called functions can modify the element values in the callers' original arrays. The array's name evaluates to the address of the array's first element. Because the starting address of the array is passed, the called function knows precisely where the array is stored. Therefore, when the called function modifies array elements in its function body, it's modifying the actual elements of the array in their original memory locations.

Figure 6.12 demonstrates that "the value of an array name" is really the address of the first element of the array by printing array, &array[0] and &array using the %p conver-

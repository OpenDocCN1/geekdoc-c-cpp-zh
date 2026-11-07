
which increments the appropriate frequency counter, based on the value of the expression `responses[answer]`. When the counter variable `answer` is 0, `responses[answer]` is 1, so `++frequency[responses[answer]];` is interpreted as `++frequency[1];`, which increments `frequency[1]`. When `answer` is 1, the value of `responses[answer]` is 2, so `++frequency[responses[answer]];` is interpreted as `++frequency[2];`, which increments `frequency[2]`. When `answer` is 2, the value of `responses[answer]` is 5, so `++frequency[responses[answer]];` is interpreted as `++frequency[5];`, which increments `frequency[5]`, and so on.

### Invalid Survey Responses

Regardless of the number of survey responses processed, only a 6-element frequency array is required (ignoring element zero) to summarize the results. But what if the data contained an invalid value such as 13? In this case, the program would attempt to add 1 to `frequency[13]`, which is outside the array's bounds. C has no array bounds checking to prevent a program from referring to an element that does not exist. So, an executing program can "walk off" either end of an array without warning—a security problem we discuss in Section 6.13. Programs should validate that all input values are correct to prevent erroneous information from affecting a program's calculations.

### Validate Array Subscripts

Referring to an element outside the array bounds is a logic error. When looping through an array, the array subscript should never go below 0 and should always be less than the total number of array elements—the array's size minus one. You should ensure that all array references remain within the bounds of the array.

### 6.4.6 Graphing Array Element Values with Bar Charts

Our next example (Fig. 6.6) reads numbers from an array and graphs the information in a bar chart. We display each number followed by a bar consisting of that many asterisks. The nested `for` statement (lines 17–19) displays the bars by iterating `n[i]` times and displaying one asterisk per iteration. Line 21 ends each bar.

```c
// fig06_06.c
// Displaying a bar chart.
#include <stdio.h>
#define SIZE 5

// function main begins program execution
int main(void) {
    // use initializer list to initialize array n
    int n[SIZE] = {19, 3, 15, 7, 11};

    printf("%s%13s%17s\n", "Element", "Value", "Bar Chart");

    // for each element of array n, output a bar of the bar chart
    for (size_t i = 0; i < SIZE; ++i) {
        printf("%7zu%13d%8s", i, n[i], "");

        for (int j = 1; j <= n[i]; ++j) { // print one bar
            printf("%c", '*');
        }

        puts(""); // end a bar with a newline
    }
}
```

| Element | Value | Bar Chart |
|---|---|---|
| 0 | 19 | ******************* |
| 1 | 3 | *** |
| 2 | 15 | *************** |
| 3 | 7 | ******* |
| 4 | 11 | *********** |

**Fig. 6.6** | Displaying a bar chart. (Part 2 of 2.)

### 6.4.7 Rolling a Die 60,000,000 Times and Summarizing the Results in an Array

In Chapter 5, we stated that we'd show a more elegant way to write Fig. 5.5's dice-rolling program. Recall that the program rolled a single six-sided die 60,000,000 times and displayed the face counts. Figure 6.7 is an array version of Fig. 5.5. Line 17 replaces Fig. 5.5's entire 20-line switch statement. Once again, we use a frequency array in which we ignore element 0, so we can use the face values as subscripts into the array.

```c
// Fig06_07.c
// Roll a six-sided die 60,000,000 times
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define SIZE 7

// function main begins program execution
int main(void) {
    srand(time(NULL)); // seed random number generator

    int frequency[SIZE] = {0}; // initialize all frequency counts to 0

    // roll die 60,000,000 times
    for (int roll = 1; roll <= 60000000; ++roll) {
        size_t face = 1 + rand() % 6;
        ++frequency[face]; // replaces entire switch of Fig. 5.5
    }

    printf("%s\t%s\n", "Face", "Frequency");

    // output frequency elements 1-6 in tabular format
    for (size_t face = 1; face < SIZE; ++face) {
        printf("%4zu\t%7d\n", face, frequency[face]);
    }
}
```

| Face | Frequency |
|------|-----------|
| 1 | 9997167 |
| 2 | 10003506 |
| 3 | 10001940 |
| 4 | 9995833 |
| 5 | 10000843 |
| 6 | 10000711 |

**Fig. 6.7** | Roll a six-sided die 60,000,000 times. (Part 2 of 2.)

## Self Check

1. **(Code)** Rewrite the following code segment to define seven-element `double` array `m` and initialize each of its elements to 10:

```c
int n[5]; // n is an array of five integers
// set elements of array n to 0
for (size_t i = 0; i < 5; ++i) {
    n[i] = 0; // set element at location i to 0
}
```

Answer:

```c
double m[7]; // m is an array of 7 doubles
// set elements of array m to 10.0
for (size_t i = 0; i < 7; ++i) {
    m[i] = 10.0; // set element at location i to 10.0
}
```

2. **(Multiple Choice)** Which of the following statements a), b) or c) is true?

- a) For an `int` array, if you provide fewer initializers than there are elements in the array, the remaining elements are initialized to 0.
- b) It's a syntax error to provide more initializers in an array initializer list than there are array elements—for example, `int n[3] = {32, 27, 64, 18};` is a syntax error, because there are four initializers but only three array elements.
- c) If the array size is omitted from a definition with an initializer list, the compiler determines the number of elements based on the number of elements in the initializer list. So, the following creates the three-element `int` array `s`:

  ```c
  int s[] = {10, 20, 30};
  ```

- d) All of the above statements are true.

Answer: d.

## 6.5 Using Character Arrays to Store and Manipulate Strings

Arrays can hold data of any type, though all the elements of a given array must have the same type. We now discuss storing strings in character arrays. So far, the only string-processing capability we have is outputting a string with `printf`. A string such as `"hello"` is really an array of individual characters, plus one more thing.

### 6.5.1 Initializing a Character Array with a String

Character arrays have several unique features. A character array can be initialized using a string literal. For example,

```c
char string1[] = "first";
```

initializes the elements of array `string1` to the individual characters in the string literal `"first"`. In this case, the compiler determined array `string1`'s size based on the string's length. The string `"first"` contains five characters plus a *string-terminating null character*. So, `string1` actually contains six elements. The escape sequence representing the null character is `'\0'`. All strings end with this character. A character array representing a string should always be defined large enough to hold the string's number of characters and the terminating null character.

### 6.5.2 Initializing a Character Array with an Initializer List of Characters

Character arrays also can be initialized with individual character constants in an initializer list, but this can be tedious. The preceding definition is equivalent to

```c
char string1[] = {'f', 'i', 'r', 's', 't', '\0'};
```

### 6.5.3 Accessing the Characters in a String

You can access a string's individual characters directly using array subscript notation. So, `string1[0]` is the character `'f'`, `string1[3]` is `'s'` and `string1[5]` is `'\0'`.

### 6.5.4 Inputting into a Character Array

The following definition creates a character array capable of storing a string of *at most 19 characters* and *a terminating null character*:

```c
char string2[20];
```

The statement

```c
scanf("%19s", string2);
```

reads a string from the keyboard into `string2`. You pass the array name to `scanf` without the `&` used with non-string variables. The `&` is normally used to provide `scanf` with a variable's *location* in memory so that a value can be stored there. In Section 6.7, when we discuss passing arrays to functions, we'll discuss why the `&` is not necessary for array names.

It's your responsibility to ensure that the array into which the string is read is capable of holding any string that the user types at the keyboard. Function `scanf` does *not* check how large the array is. It will read characters until a *space*, *tab*, *newline* or *end-of-file indicator* is encountered. The string `string2` should be no longer than 19 characters to leave room for the terminating null character. If the user types 20 or more characters, your program may crash or create a security vulnerability called a buffer overflow. For this reason, we used the conversion specification `%19s`. This tells `scanf` to read a maximum of 19 characters, preventing it from writing characters into memory beyond the end of `string2`. (In Section 6.13, we revisit the potential security issue raised by inputting into a character array and discuss the C standard's `scanf_s` function.)

### 6.5.5 Outputting a Character Array That Represents a String

A character array representing a string can be output with `printf` using the `%s` conversion specification. For example, you can print the character array `string2` with

```c
printf("%s\n", string2);
```

Like `scanf`, `printf` does not check how large the character array is. It displays the string's characters until it encounters a terminating null character. [Consider what would print if, for some reason, the terminating null character were missing.]

### 6.5.6 Demonstrating Character Arrays

Figure 6.8 demonstrates initializing a character array with a string literal, reading a string into a character array, printing a character array as a string and accessing a string's individual characters. The program uses a `for` statement (lines 20–22) to loop through the `string1` array and print the individual characters separated by spaces, using the `%c` conversion specification. The condition in the `for` statement is true while the counter is less than the array's size and the terminating null character has not been encountered in the string. This program reads only strings that do not contain whitespace characters. We'll show how to read strings containing whitespace characters in Chapter 8.

```c
// fig06_08.c
// Treating character arrays as strings.
#include <stdio.h>
#define SIZE 20
```

**Fig. 6.8** | Treating character arrays as strings. (Part 1 of 2.)


- 3. Write the code to declare a dynamic pointer and allocate storage to store a one-dimensional array of 80,000 elements of data type float.
- 4. Write a program to declare a dynamic pointer and allocate storage to store a two-dimensional array of $50 \times 60$ of data type float. Also write the code to input data to the dynamic array and output the data from the dynamic array.

## 10.5 Character Strings and Pointers

Character strings may be manipulated using pointers and dynamic pointers. Dynamic pointers are used when the character strings vary greatly in length. Storage for variable length strings may be allocated using the malloc() function from the stdlib.h library header file.

The dynamic storage allocation function malloc() is a single argument function, the argument being the number of bytes needed to store a single variable, whereas the dynamic storage allocation function calloc() is a two-argument function with the first argument being the number of storage cells and the second argument being the size of each storage cell. The function malloc() is generally used to allocate storage for strings.

### 10.5.1 Dynamic Storage of Character Strings

Smooth arrays are not efficient for storing strings, which vary greatly in their lengths. They should be allocated storage from the free store with their addresses assigned to a pointer variable of type char.

The following code shows the allocation of storage from free store by using the dynamic storage allocation function malloc(). In order to allocate exactly the right amount of storage for each string, the string must be input into a static char array of maximum size, the actual length of the string determined, the right amount of storage allocated using the dynamic storage allocation function malloc(), and the character string copied into it. To keep track of all the strings, their pointers are stored in a character pointer array. The function malloc() is used rather than calloc() to store a character string because a character string may be manipulated as a unit.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
```

#define NUMSTR 4
#define STLNG 80
int main() {
    int i;
    char strname[STLNG]; /* an input buffer for the string */
    char *strptr[NUMSTR]; /* an array of string pointers */
    printf("Input strings:\n");
    for(i= 0; i<NUMSTR; i++) {
        gets(strname);
        strptr[i] = (char *)malloc(strlen(strname) + 1);
        strcpy(strptr[i],strname);
    }
    printf("Output strings:\n");
    for(i= 0; i<NUMSTR; i++) {
        puts(strptr[i]);
    }
    return 0;
}
```

Input strings:
AAAAAAA
BBBBBBBBBBBBBB
EEEE
PPPPPPPPPPPPPPPP

Output strings:
AAAAAAA
BBBBBBBBBBBBBB
EEEE
PPPPPPPPPPPPPPPP

Each time the dynamic storage allocation function malloc() is called, it allocates a single block of storage and returns its address, which is cast to datatype char* and stored in the pointer array. This function is in the library stdlib.h, which must be included as #include <stdlib.h>. The other functions, strlen() and strcpy(), are in the string.h library, which must be included as #include <string.h>.

# Storage at the time the program terminates is allocated as follows:

| | 4 |
| :--- | :--- |
| str | P | P | P | P | P | P | P | P | P | P | P | \0 | | | | |
| strptr | A | A | A | A | A | A | A | \0 |
| | B | B | B | B | B | B | B | B | B | B | \0 |
| | E | E | E | E | \0 |
| | P | P | P | P | P | P | P | P | P | P | P | P | P | \0 |

With a maximum string length of 80 characters it would take 320 bytes of memory to store these strings in a static array. Using dynamic arrays, 48 bytes are needed for the strings, 80 more for the buffer, and 16 for the pointer array for a total of 144 bytes.

### 10.5.2 Passing Strings to Functions as Dynamic Arrays

A character string stored in dynamic storage may be passed to a function using the dynamic pointer and the string may be printed in the function. The following code shows the output of such a string.

```
#include <stdio.h>
void funcoutput(char *);
int main() {
	char str[20] = "COMPUTATION";
	char *chrptr;
	chrptr = (char *) malloc(strlen(str) + 1);
	strcpy(chrptr, str);
	funcoutput(chrptr);
	return 0;
}
```

```
void funcout(char *strptr)
{
    printf("String: %s\n", strptr);
    return;
}
```

The output is as as follows:

String: COMPUTATION

Notice that the dynamic storage is allocated using the function malloc( ). The string is copied from strname to the dynamic storage pointed to by the dynamic pointer chrptr. The dynamic string pointer is passed to the function and the string is printed in the function.

When strings are being stored as dynamic arrays, their pointers are in a static array. The string pointer array may be passed to a function and the strings manipulated inside the function. The following code shows the input and output of dynamic character strings in an array.

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void funinput(char *strptr[ ], int NUMSTR);
void funcout(char *strptr[ ], int NUMSTR);

int main()
{
    const int NUMSTR = 5;
    int i;
    char *strptr[NUMSTR];
    funinput(strptr, NUMSTR);
    funcout(strptr, NUMSTR);
    return 0;
}

void funinput(char *strptr[ ], int NUMSTR)
{
    const int STRLNG = 80;
    int i;
    char strname[STRLNG];
```

```
for(i = 0; i < NUMSTR; i++)
{
    gets(strname);
    strptr[i] = (char *) malloc(strlen(strname) + 1);
    strcpy(strptr[i], strname);
}
return;
}
```

```
void funcoutput(char *strptr[], int NUMSTR)
{
    int i;
    printf("\nOUTPUT STRING:\n");
    for(i = 0; i < NUMSTR; i++)
    {
        printf("%2d ", strlen(strptr[i]));
        puts(strptr[i]);
        printf("\n");
    }
    return;
}
```

Input Data:
AAXXXXAAAA
XXX YYYYYYYPPPP
KPPKKK LLKLLKLLLL KKKKK
LLLLLL
BBBBBBBBBBBBBBBBBBPPPPBBBB

Output Data:
OUTPUT STRING:
12 AAXXXXAAAA
17 XXX YYYYYYYPPPP
27 KPPKKK LLKLLKLLLL KKKKK
7 LLLLLL
31 BBBBBBBBBBBBBBBBBPPPPBBBB

Notice that the input data contains strings with embedded spaces and since trailing blanks are ignored, the strings are of different lengths. The input function gets() inputs strings from a data up to and including the line feed and stores them in strname, which has space for 80 characters. This is a temporary buffer to hold the variable length strings. The strings are copied into dynamic storage, which is allocated just enough to hold each string. The address of each string is assigned to an element of the array of string pointers. The dynamic storage allocation function malloc() is used to allocate storage from free store to store each variable length string. The string copy function strcpy is used to copy each string from the buffer strname to the free storage allocated by the malloc() function. From this point on, strings may be manipulated using the pointer array, which contains the addresses of the strings stored in free store.

### 10.5.3 Review Questions

- 1. Indicate whether the following statements are true or false.
  a. If there is not much variability in length of the character strings they may be stored in smooth arrays.
  b. To store strings with large variability in length, dynamic storage should be used.
  c. The dynamic storage allocation function malloc( ) may be used to allocate to store strings.

## 10.6 Sample Programs

These sample programs demonstrate the use of pointers for manipulating single variables and one- and two-dimensional arrays. Also, some of the programs presented in this section use dynamic storage for manipulation of one- and two-dimensional arrays and character strings.

### 10.6.1 Tensile Stress

Problem Create a table that shows stress in a rectangular steel bar with width w, thickness t, and length l subject to varying tensile loads. Ask the user for the range of loads and the increment.

Data

Input the cross-section dimensions.
Input the minimum load, maximum load, and increment size.

Method

Compute the cross-sectional area.
Compute the number of values in the table.

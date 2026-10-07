
strings. (These functions are covered in Lesson 18.) To pass a string to one of these functions, you pass the array name. The same is true of the string display functions printf() and puts(), discussed later in the chapter.

You might have noticed that "strings stored in an array" was mentioned a moment ago. Does this imply that some strings aren't stored in arrays? Indeed it does, and the next section explains why.

# Strings Without Arrays

From the preceding section, you know that a string is defined by the character array’s name and a null character. The array’s name is a type char pointer to the beginning of string. The null marks the string’s end. The actual space occupied by the string in array is incidental. In fact, the only purpose the array serves is to provide allocated space for the string.

If you could find some memory storage space without allocating an array? You could then store a string with its terminating null character instead. A pointer to its first character could serve to specify the string’s beginning as if the string were in allocated array. How do you go about finding memory space? There are two methods: One allocates space for a literal string when the program is compiled, the other uses the malloc() function to allocate space while the program is executing, process known as dynamic allocation.

# Allocating String Space at Compilation

The start of a string, as mentioned earlier, is indicated by a pointer to a variable of type char. You might recall how to declare such a pointer:

```
char *message;
```

This statement declares a pointer to a variable of type char named message. It doesn’t point to anything, but what if you changed the pointer declaration to read:

```
char *message = "Great Caesar’s Ghost!";
```

When this statement executes, the string Great Caesar’s Ghost! (with a terminating null character) is stored somewhere in memory, and the pointer message is initialized to point to the first character of the string. Don’t worry, handled automatically by the compiler. When defined, message is a pointer to the string and can be used as such.

The preceding declaration/initialization is equivalent to the following, and the two notations *message and message[] also are equivalent; both mean “a pointer to to":

```
char message[] = "Great Caesar’s Ghost!";
```

This method of allocating space for string storage is fine when you know what string you need when writing the program. What if the program has varying storage needs, depending on user input or other factors that are unknown when you write the program? You use the malloc() function, which lets you allocate storage space on-the-fly.

# The malloc() Function

The malloc() function is one of C's memory allocation functions. When you call malloc(), you pass the number of bytes of memory needed. malloc() finds and reserves a block of memory of the required size and returns the address of the first byte in the block. You don't need to worry about where the memory is found; it is handled automatically.

The malloc() returns an address, and its return type is a pointer to type void. Why? A pointer to void is compatible with all data types. Because the memory allocated by malloc() can be used to store any of C's data types, the void return type is appropriate.

# Syntax

# The malloc() Function

```
#include <stdlib.h>
void *malloc(size_t size);
```

malloc allocates a block of memory that is the number of bytes stated in size. By allocating memory as malloc() instead of at once when a program starts, you can use a computer's memory more efficiently. When using malloc(), you need to include the stdlib.h header file. Some compilers have other header files that can be included; for portability, however, it's best to include stdlib.h.

malloc() returns a pointer to the allocated block of memory. If malloc() cannot allocate the required amount of memory, it returns null. Whenever you try to allocate memory, you should always check the return value, even if the amount of memory to be allocated is small.

# Example 1

```
#include <stdlib.h>
#include <stdio.h>
int main( void )
{
    /* allocate memory for a 100-character string */
    char *str;
    str = (char *) malloc(100);

    if (str == NULL)
    {
        printf("Not enough memory to allocate buffer\n");
        exit(1);
    }
    printf("String was allocated!\n" );
    return 0;
}
```

# Example 2

```c
/* allocate memory for an array of 50 integers */
int *numbers;
numbers = (int *) malloc(50 * sizeof(int));
```

# Example 3

```c
/* allocate memory for an array of 10 float values */
float *numbers;
numbers = (float *) malloc(10 * sizeof(float));
```

# Using the malloc() Function

You can use malloc() to allocate memory to store a single type char. First, declare a pointer to type char:

char *ptr;

Next, call malloc() and pass the size of the wanted memory block. Because a type char usually occupies 1 byte, you need a block of 1 byte. The value returned by malloc() is assigned to the pointer:

ptr = malloc(1);

This statement allocates a memory block of 1 byte and assigns its address to ptr. Unlike variables that are declared in the program, this block of memory has no name. The pointer can reference the variable. For example, to store the character 'x' there, you would write

*ptr = 'x';

Allocating storage for a single type of char is almost identical to using malloc() to allocate space for a single type char. The main difference is that you need to know the amount of space to allocate—the maximum number of characters in the string. For example, say you want to allocate space for a string of 99 characters, 1 for the terminating null character, for a total of 100. First, you declare a pointer to type char, and then you call malloc():

# Syntax 223

```
char *ptr;
ptr = malloc(100);
```

Now ptr points to a reserved block of 100 bytes that can be used for string storage and manipulation. You can use ptr just as though your program had explicitly allocated space with the following array declaration:

```
char ptr[100];
```

Using malloc() lets your program allocate storage space as needed in demand. Of course, available space is not unlimited; it depends on the amount of memory installed in your computer and on the program's other storage requirements. If not enough memory is available, malloc() returns null (0). Your program should test the return value of malloc() so you know the memory requested was allocated successfully. You always should test malloc()'s return value against the symbolic constant NULL, which is defined in stdlib.h. Listing 10.3 illustrates the use of malloc(). Any program using malloc() #include the header file stdlib.h.

# TIP

> Literal values were used to allocate space for characters in the examples above. You should always multiply the size of the data type you are allocating space for the amount of space you want. The previous allocations assumed that a character was stored in just 1 byte. If a character is stored in more than 1 byte, then the previous examples overwrite other areas of memory:

```
ptr = malloc(100);
```

should actually be declared as

```
ptr = malloc(100 * sizeof(char));
```

# Input
LISTING 10.3 malloc.c: Using the malloc() Function to Allocate Storage Space for String Data

```c
1: /* malloc.c--Demonstrates the use of malloc() to allocate storage /*
2: /* space for string data. */
3:
4: #include <stdio.h>
5: #include <stdlib.h>
6:
7: char count, *ptr, *p;
8:

# LESSON 10 Working with Characters

```c
9: int main( void )
10: {
11:     * Allocate a block of 35 bytes. Test for success. */
12:     * The exit() library function terminates the program. */
13:
14:     ptr = malloc(35 * sizeof(char));
15:
16:     if (ptr == NULL)
17:     {
18:         puts("Memory allocation error.");
19:         return 1;
20:     }
21:
22:     * Fill the string with values 65 through 90, */
23:     * which are the ASCII codes for A-Z. */
24:
25:     * p is a pointer used to step through the string. */
26:     * You want ptr to remain pointed at the start */
27:     * of the string. */
28:
29:     p = ptr;
30:
31:     for (count = 65; count < 91; count++)
32:         *p++ = count;
33:
34:     * Add the terminating null character. */
35:
36:     *p = '\0';
37:
38:     * Display the string on the screen. */
39:
40:     puts(ptr);
41:
42:     free(ptr);
43:
44:     return 0;
45: }
```

# Output ▼

ABCDEFGHIJKLMNOPQRSTUVWXYZ

# Analysis ▼

This program uses malloc() in a simple way. Although the program seems long, it's filled with comments. Lines 1, 2, 11, 12, 22 through 27, 34, and 38 are all comments that detail everything the program does. Line 5 includes the stdlib.h header file needed for malloc(), and line 4 includes the stdio.h header file for the puts() functions.

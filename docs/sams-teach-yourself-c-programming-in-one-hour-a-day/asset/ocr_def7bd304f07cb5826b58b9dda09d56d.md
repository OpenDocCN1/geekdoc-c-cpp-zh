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

```
1: /* malloc.c--Demonstrates the use of malloc() to allocate storage /*
2: /* space for string data. */
3:
4: #include <stdio.h>
5: #include <stdlib.h>
6:
7: char count, *ptr, *p;
8:
```
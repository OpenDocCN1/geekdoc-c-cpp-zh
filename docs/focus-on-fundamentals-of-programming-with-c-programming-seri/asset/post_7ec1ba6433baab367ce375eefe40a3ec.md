
- i) Output the first and last name of all employees who make more than $35,000 per year, have been with the company for at least 5 years, and who are over 30 years old.

- j) Give a 10% raise to all employees who make less than $350.00 per week and output the first and last name and new salary for each of the employees who received the raise.

- k) (Extra Credit) Sort the structures according to zip codes and output the first and last name and zip code for each of the employees.

Here is a C function, strsub(), that grabs a substring, sub, from a string, buf, given the start and end index within the string.

```
void strsub(char buf[], char sub[], int start, int end) {
    int i, j;
    for (j=0, i=start; i<=end; i++, j++) {
        sub[j] = buf[i];
    }
    sub[j] = '\0';
}
```

This function might be useful when you read a line of data from the file and need to grab the different information from the line of data to place into the fields of the struct. Remember that arrays use zero-based indexing.

```
while (!feof(fp)) {
    fgets(buf, MAX, fp);
    strsub(buf, workers[i].first, 0, 6);
    strsub(buf, workers[i].initial, 8, 8);
    strsub(buf, workers[i].last, 10, 18);
    ...
}
```

You can assume the following declaration:

```
#define MAX 100
```

The following three functions from the C library, stdlib.h and string.h, might be useful for the lab:

- atoi() - converts a string to an integer
- atof() - converts a string to a float
- strcmp() - compares two strings

For the extra credit portion of the lab you will need to modify the sorting algorithm that we looked at to work with structs.

The contents of payfile.txt are given below:

| ADA | A AGUSTA | 33 BABBAGE ROAD | LOVELACE | GB 19569 | 28 F 2 | 350.50 |
| --- | --- | --- | --- | --- | --- | --- |
| ISSAC | A ASIMOV | 99 FICTION WAY | AMHERST | MA 63948 | 58 M 6 | 423.88 |
| HUMPHRY | R BOGART | 71 SAM STREET | HOLLYWOOD | CA 48482 | 56 M 5 | 366.00 |
| ALBERT | G EINSTEIN | 94 ENERGY WAY | PRINCETON | NJ 47474 | 67 M 8 | 780.00 |
| EMMYLOO | L HARRIS | 66 COUNTRY ROAD | NASHVILLE | TN 72647 | 38 F 2 | 767.42 |
| JAMES | T KIRK | 11 SPACE STREET | VULCAN | CA 82828 | 46 M 1 | 235.70 |
| TED | L KOPPLEMAN | 55 ABC PLACE | WASHINGTON | DC 37376 | 48 M 9 | 909.44 |
| DAVID | T LETTERMAN | 14 WNBC AVENUE | NEW YORK | NY 19338 | 47 M 5 | 445.65 |
| STEVIE | R NICKS | 31 MUSIC ROAD | CHICAGO | IL 23459 | 38 F 8 | 460.88 |
| MONTY | P PYTHON | 76 SILLY STREET | LONDON | GB 80939 | 44 M 2 | 320.50 |
| ROGER | R RABBIT | 15 LOONEY TOONS | HOLLYWOOD | CA 91343 | 24 M 4 | 259.53 |
| SALLY | W RIDE | 21 COLUMBIA WAY | HOUSTON | TX 91123 | 30 F 9 | 707.80 |
| ROD | Q SERLING | 11 TWILIGHT ZONE | SAN DIEGO | CA 93939 | 56 M 1 | 440.00 |
| LUKE | R SKYWALKER | 43 MILKY WAY | NEW YORK | NY 12343 | 35 M 5 | 660.00 |

Remember that the main() function should appear as the first function in the program. Be sure to use function prototypes for each of the functions that are used in your program.

Output from your program should be sent to the terminal window (your screen) as well as the requested csis.txt output file. Be sure to read the document on Capturing Program Output. Your full name must appear as a comment in the source file that contains main(). Be sure to include the csis.txt output file in your zip archive.

# Dynamic Allocation of Variables
## Dynamic Arrays - Advanced

## Dynamic Allocation of Variables

Dynamic variables are variables that can be created and disposed of as a program executes. When a variable is needed, storage is reserved for it. When it is no longer needed, the storage is released. Therefore, the storage for these dynamic variables that are no longer in use is available for other purposes. There is no predefined limit to the number of dynamic variables that can be created.

We reference a dynamic variable not by name but through a pointer. Remember a pointer is a variable that contains the address (location) in memory of the dynamic variable it references. Every new dynamic variable created has an associated pointer to reference it. So when we allocate storage for a dynamic variable, our method of accessing the variable is through a pointer.

In order to create a dynamic variable of type integer, it is first necessary to declare a pointer variable that can hold its address. The declaration:

```
int *p;
```

declares the variable p to be a pointer variable whose values will be pointers to (contain the address of) dynamic variables of type int.

But a pointer variable is of no use unless there is something for it to point to. In order to create a dynamic variable, we use the malloc() function as follows:

```
int *p;
p = (int *) malloc(sizeof(int));
```

malloc() dynamically allocates variable-sized blocks of memory from the heap and allows a program to allocate memory explicitly as it's needed. By definition, malloc() returns a void * and therefore must be cast to the appropriate type of the pointer that will receive the address on the heap of the new dynamic variable, in this case int *. It is our responsibility to tell malloc() exactly how much storage to allocate for the dynamic variable, in this case sizeof(int) bytes. malloc() is prototyped in both the alloc.h and stdlib.h header files.

If malloc() is successful, it returns a pointer to the newly allocated block of memory. Otherwise, if not enough space exists for the new block of storage, malloc() returns NULL, which is a special value that any pointer variable may have. The NULL pointer does not reference a storage location.

We say that malloc() creates a new dynamic variable of type int and gives the address of the new dynamic variable to pointer p. This dynamic variable is then referred to as “the thing pointed to by p” or *p.

```
*p = 5;
printf("%d\n", *p);
```

In fact, *p can be used anyplace that it is appropriate to use a variable of type int. When a dynamic variable is no longer needed, we can use the free() function to free the memory space allocated to the dynamic variable:

```
free(p);
```

free() deallocates a block of memory allocated by a previous call to malloc(). It destroys the dynamic variable referenced by pointer p. The storage allocated to this variable is returned (recycled) to be assigned to some other dynamic variable. Accordingly, any further reference to *p is illegal. free() is also prototyped in alloc.h and stdlib.h.

See if you can follow the pointers in the following program.

```
// dynamic.c

#include <stdio.h>
#include <alloc.h>

int main(void) {
    int *p, *q;

    p = (int *) malloc(sizeof(int));
    *p = 3;
    q = (int *) malloc(sizeof(int));
    *q = 5;
    printf("*p = %d\t*q = %d\n", *p, *q);
    free(p);
    p = q;
    printf("*p = %d\t*q = %d\n", *p, *q);
    *q = 7;
    printf("*p = %d\t*q = %d\n", *p, *q);
    q = (int *) malloc(sizeof(int));
    *q = 9;
    printf("*p = %d\t*q = %d\n", *p, *q);
    *p = *q;
    printf("*p = %d\t*q = %d\n", *p, *q);
    free(p);
    p = q;
    printf("*p = %d\t*q = %d\n", *p, *q);
    free(p);
    printf("*p = %d\t*q = %d\n", *p, *q);
    return 0;
}
```

The output to the above program is:

```
*p = 3      *q = 5
*p = 5      *q = 5
*p = 7      *q = 7
*p = 7      *q = 9
*p = 9      *q = 9
*p = 9      *q = 9
```

Note that the last statement in the program is illegal although the C compiler will not complain about it! In the preceding statement, free(p), the dynamic variable that pointer p points to is disposed of. It is therefore illegal to dereference the pointer p. If you do, your program will become unstable. Although the C compiler will not find the error, you can be sure that the error will be found after you have shipped the 100,000th copy of your program!

There is another reason that the last statement in the program is illegal. It is because pointer q is being dereferenced! You might be wondering why this would be illegal since we have not executed a free(q) statement. Well, at least not directly. At the time we execute the free(p) statement, both pointers p and q are pointing to the same memory location, to the same dynamic variable. Therefore, after executing free(p), pointer q is no longer pointing to a dynamic variable. Its storage has already been reclaimed. It is therefore illegal to dereference both pointers p and q at this point in the program.

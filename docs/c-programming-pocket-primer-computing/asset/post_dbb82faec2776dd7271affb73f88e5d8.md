
## THE FGETS() FUNCTION (C11 COMPLIANT)

This section contains a code sample that shows you how the behavior of the fgets() function differs from the gets() function (discussed in the next section). Whether or not you read the code samples, make sure you remember to use the fgets() function and *never* use the gets() function.

Listing 2.17 displays the contents of the C program `testfgets.c` that illustrates the use of the fgets() function.

### LISTING 2.17: testfgets.c

```c
#include <stdio.h>
#define MAX 10
int main()
{
    char buf[MAX];
    fgets(buf, MAX, stdin);
    printf("string is: %s\n", buf);
    return 0;
}
```

The code is very simple: users are prompted to enter a string and that string is re-displayed at the command prompt. Now compile the code in Listing 2.17 as follows:

```
gcc -std=c11 testfgets.c -o testfgets
```

Launch the executable and enter a string:

```
$ ./testfgets
this is a long string and let's see what happens
prompt.
```

Now compile the code in Listing 2.18 as follows:

```
gcc -std=c11 testgets.c -o testgets
```

Launch the executable and enter a string:

```
$ ./testgets
warning: this program uses gets(), which is unsafe.
Enter a string: this is a long string and let's see what happens
string is: this is a long string and let's see what happens
Segmentation fault: 11
```

> NOTE  The unsafe message is displayed only when you launch the executable and not during the compilation/link step.

There is one significant impediment to using the safe string functions: although safe functions (such as `strcpy_s` and `strtok_s` and others) are specified by the C standard since C11, they are actually optional in C11 because all standard library implementations are not required to provide optional features. Hence, in order to get `strcpy_s` and `strtok_s` and all the other safe string functions into your system, you will need to either 1) find a library that implements them all, or 2) implement them yourself.

Finally, the following websites allow you to copy/paste code snippets into their Web pages in order to check for C11 compliance:

- https://godbolt.org/
- https://wandbox.org/

## READING A SINGLE CHARACTER FROM THE COMMAND LINE

Listing 2.19 displays the contents of `ReadSingleChar.c` that illustrates how to use the `getchar()` function to read a single character from standard input and then print that character using the `putchar()` function in a C program.

### LISTING 2.19: ReadSingleChar.c

```c
#include <stdio.h>

int main()
{
    int c;

    printf( "Enter a value :");
    c = getchar();

    printf( "\nYou entered: ");
    putchar( c );

    return 0;
}
```

Listing 2.19 contains a `main()` function that declares the integer variable `c`, followed by a `printf()` statement that prompts users for input. After users press a key on the keyboard, the built-in `getchar()` C function assigns that value to the variable `c`. The next portion of code displays the value that users entered at the keyboard. A sample invocation of launching the code in Listing 2.19 is here:

```
Enter a value :f
You entered: f
```

## READING AN UNFORMATTED LINE FROM THE COMMAND LINE

Listing 2.20 displays the contents of `ReadLine.c` that illustrates how to read a line of text from the keyboard and displays its length.

### LISTING 2.20: ReadLine.c

```c
#include <string.h>
#include <stdio.h>

char line[100];

int main()
{
    printf("Enter a line: ");
    fgets(line, sizeof(line), stdin);
    printf("The length of the line is: %d\n", strlen(line));

    return (0);
}
```

Listing 2.20 declares a character array `line` of length 100, followed by a `main()` function with a `printf()` statement that prompts users for input. This time users can enter more than one character (i.e., a complete sentence whose length is at most 99). After users provide their input, the built-in `fgets()` C function assigns that input to the variable `line`. The next portion of code displays the length of the input string that users entered at the keyboard. A sample invocation of launching the code in Listing 2.20 is here:

```
Enter a line: this is a simple input line
The length of the line is: 28
```

**Another invocation of launching the code in Listing 2.20 is here:**

```
Enter a line: abcd
The length of the line is: 5
```

Notice that the string abcd is only four characters: where does the extra character come from? The function fgets() also includes the end-of-line `'\n'` in the string (i.e., the fifth character).

The sizeof() function also provides a convenient way of limiting the number of characters read to the maximum number that the variable can hold.

Here’s an interesting question: given an array myarr of an unknown primitive data type and unknown length, how can you determine the number of items in the array?

The simple (elegant?) answer involves the sizeof() operator, as shown here:

```
// myarr is defined elsewhere
int len = sizeof(myarr)/sizeof(myarr[0]);
```

Since the elements of the array myarr have the same data type, they all have the same size, which means that the length of the array myarr is a multiple of the size of the first (or any other) element in the array. This operator will be discussed in more detail in Chapter 6.

## READING A FORMATTED LINE FROM THE COMMAND LINE

Listing 2.21 displays the contents of `ReadFormattedLine.c` that illustrates how to read a formatted line from standard input via the `scanf()` function in a C program.

### LISTING 2.21: ReadFormattedLine.c

```c
#include <stdio.h>

int main( )
{
    char str[100];
    int i, numfilled;

    printf(" Enter a string and an int :");
    numfilled = scanf("%s %d", str, &i);

    printf("\nNumber of filled values: %d\n",numfilled);
    printf("\nYou entered values for the string and the int");
    printf("\nYou entered the string %s and the number %d ", str, i);

    return 0;
}
```

Listing 2.21 contains a `main()` function that declares a character array `str` of length 100 and also declares an integer-valued variable `i`. Next, a `printf()` statement prompts users for input. This time users can enter a string and an integer, after which the built-in `scanf()` C function assigns the input string to `str` and the input integer to `i`.

There are two points to keep in mind. First, if you enter a string and press the <RETURN> key, the program seems to “hang” as it waits for you to enter a number. Second, any additional input beyond the number that you enter is ignored (see examples below).

After users provide their input, the `printf()` function displays the values of both of these variables. A sample invocation of launching the code in Listing 2.21 is here:

```
Enter a string and an int: abc 3

Number of filled values: 2

You entered values for the string and the int
You entered the string abc and the number 3
```

Another sample invocation of launching the code in *Listing 2.21* is here:

```
Enter a string and an int: abc 3 4 5

Number of filled values: 2

You entered values for the string and the int
You entered the string abc and the number 3
```

## THE BEHAVIOR OF THE SCANF() FUNCTION (OPTIONAL)

The behavior of the `scanf()` function in *Listing 2.21* depends on the type of input that is provided. Specifically, if the provided input does not match the format string, the variables are never initialized. The C specification is very clear: as soon as there is a character from the input that does not match the “current part” of the format string that the `scanf()` function is trying to match, the matching process stops *immediately* without reading any more characters or assigning values to any more variables. In addition, anything that happens after the failure of the matching process is “undefined behavior.”

For example, consider what happens when users provide the following input values after launching the code in *Listing 2.21*:

```
Enter a string and an int: abc x y z

Number of filled values: 1

You entered values for the string and the int
You entered the string abc and the number 1
```

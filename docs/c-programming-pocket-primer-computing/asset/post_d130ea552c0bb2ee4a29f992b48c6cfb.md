
Listing 3.2 displays the contents of BreakContinue.c that shows you how to use the break and continue statements in a for loop in C.

### LISTING 3.2: BreakContinue.c

```c
#include <stdio.h>

int main()
{
    int max=5;

    for(int i=0; i<max; i++)
    {
        if(i == 3 ) continue;
        if(i == 4 ) break;
        printf("i : %d\n", i);
    }

    return 0;
}
```

Listing 3.2 contains a for loop with conditional logic that checks the value of the loop variable i. If the value of i equals 3, the code “skips” to the top of the loop and increments the value of i. If the value of i equals 4, the code exits the loop and effectively ends the execution of the C program.

Thus, the only time that the printf() statement is executed is when the variable i equals 0, 1, or 2. The output from launching the C program in Listing 3.2 is here:

i : 0
i : 1
i : 2

## CHECKING FOR LEAP YEARS

As a quick reminder, a *leap year* is a positive (integer-valued) year that satisfies the following two conditions:

- the year is a multiple of four, and
- if the year is a century then the year must be a multiple of 400

Examples of leap years include: 400, 1492, 1776, 2000, 2012, and 2472 (note that the centuries are multiples of 400). Examples of years that are not leap years include: 100, 1370, 1510, 1900, and 2011 (note that the centuries are *not* multiples of 400).

Listing 3.3 displays the contents of `LeapYear.c` that illustrates how to use if-else logic in a C program to determine if a particular year is a leap year.

### LISTING 3.3: LeapYear.c

```c
#include <stdio.h>

int main()
{
    int years[6] = {1900, 1953, 1958, 2000, 2004, 2006};
    int year=0, leapyear=0;

    int len = sizeof(years)/sizeof(years[0]);

    for(int i=0; i<len; i++)
    {
        year = years[i];

        if( year % 4 == 0)
        {
            leapyear = 1;
        }
        // "leap centuries" must be multiples of 400
        if( (year % 100 == 0) && (year % 400 != 0) )
        {
            leapyear = 0;
        }
        else // not a multiple of 4
        {
            leapyear = 0;
        }

        if( leapyear == 0)
        {
            printf("%d: not a leap year\n",year);
        }
        else
        {
            printf("%d: leap year\n",year);
        }

    }

    return 0;
}
```

Listing 3.3 defines the “flag” variable leapyear, along with the integer-valued array years that contains six positive integers. Next, a for loop iterates through the elements of the years array in order to determine which year (if any) is a leap year.

The outer if statement checks if the current year is a multiple of 4: if so then it's a leap year (and leapyear is set to 1); if not, then the else clause sets leapyear to 0 (because it's not a leap year).

There is an additional check that must be performed. The inner if statement checks if the current year is a multiple of 100 and not a multiple of 400: if this is the case, then the current year is not a leap year, so the variable leapyear must be set to 0 (because its value has already been set to 1 by the outer if statement).

The bottom portion of the for loop contains conditional logic that displays the appropriate message based on the value of the variable leapyear.

The output from Listing 3.3 is here:

1900: not a leap year
1953: not a leap year
1958: not a leap year
2000: leap year
2004: leap year
2006: not a leap year

## CHECKING ALPHABETIC TYPES

Letters and numbers have an ASCII value, and it's possible to check their type. Listing 3.4 displays the contents of Alphabetic.c that illustrates how to check for alphabetic characters in C.

### LISTING 3.4: Alphabetic.c

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
    int ch;

    for (ch = 0x7c; ch <= 0x82; ch++) {
        printf("%#04x  ", ch);

        if (isascii(ch))
        {
```

### LISTING 3.5

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char ch, str1[] = "This is a String";
    int lcount=0, ucount=0;

    int len1 = strlen(str1);

    for(int i=0; i<len1; i++)
    {
        ch = str1[i];
        if(('a' <= ch) && (ch <= 'z'))
        {
            lcount++;
        }
        else if (('A' <= ch) && (ch <= 'Z'))
        {
            ucount++;
        }
    }

    printf("Original:  %s\n",str1);
    printf("Lower count: %d\n",lcount);
    printf("Upper count: %d\n",ucount);

    return 0;
}
```

Listing 3.5 starts by defining the character string str1, and then initializing the integer-valued variable len1 with the length of the string str1. The next section in Listing 3.5 contains a for loop whose loop variable i iterates between 0 and len1, and initializes the variable ch with the character that is in the ith position of the str1 array.

Next, conditional logic checks if ch is between the letters "A" and "Z," in which case the variable lcount

### LISTING 3.6

```c
{
  ch = line[i];

  if(isblank(ch))
  {
    printf("%c is a blank\n", ch);
  }
  else if(isdigit(ch))
  {
    printf("%c is a digit\n", ch);
  }
  else if(isupper(ch))
  {
    printf("%c is uppercase\n", ch);
  }
  else if(islower(ch))
  {
    printf("%c is uppercase\n", ch);
  }
  else if(ispunct(ch))
  {
    printf("%c is punctuation\n", ch);
  }
  else
  {
    printf("%c is other type\n", ch);
  }

  return 0;
}
```

Listing 3.6 defines a string variable line, followed by a for loop that iterates through each character in the string line. Next, the if/else conditional logic invokes the built-in C functions isblank(ch), isdigit(ch), isupper(ch), islower(ch), and ispunct(ch) to check if a character is a blank, a digit, an uppercase letter, a lowercase letter, or punctuation, respectively. If the conditional check is true, then the appropriate text message is printed.

The output from compiling and executing the code in Listing 3.6 is here:

A is uppercase
b is uppercase
c is uppercase
3 is a digit
  is a blank
: is punctuation

Listing 3.6 contains an assortment of built-in functions for testing the type of a given character. In addition, C supports the following useful built-in character-related functions:

- iscntrl() Tests for control characters.
- isgraph() Tests for printable characters excluding the space.
- isprint() Tests for printable characters including the space.
- ispunct() Tests for punctuation characters as defined in the locale.
- isspace() Tests for white-space characters.
- isxdigit() Tests for wide hexadecimal digits 0 through 9, a through f, or A through F.

## WORKING WITH ARRAYS

As you saw in Chapter 1, an array declaration in C requires the type of the elements and the number of elements required by an array:

```
type arrayName [ arraySize ];
```

The preceding code snippet is for defining a one-dimensional array. The value of arraySize must be an integer constant greater than zero, and the type can be any valid C data type. For example, to declare a 10-element array called balance of type double, use this statement:

```
double balance[10];
```

As you can see, the balance array can hold as many as 10 double numbers, and the following subsections contain examples of working with the balance array.

### Initializing Arrays

C arrays start with an index value of 0, and the index value of the last element in the array is the array size minus 1. C allows you to initialize the values in an array in two ways: either one element at a time or via a single statement. An example of the latter is here:

```
double balance[5] = {1.5, 2.0, 3.4, 997.0, 25.0};
```

Notice that the number of values inside the pair of braces { } equals the number that is specified inside the square brackets [ ]. You can also omit the size of the array, and the compiler will handle the initialization, an example of which is here:

```
double balance[] = {1.5, 2.0, 3.4, 997.0, 25.0, -123, 777};
```

After initializing an array, you can also update the value of an element, as shown here:

```
balance[2] = 3000.0;
```

### Array Values

Access an array element via the index of the element in the array. For example, suppose the balance array is initialized as above:

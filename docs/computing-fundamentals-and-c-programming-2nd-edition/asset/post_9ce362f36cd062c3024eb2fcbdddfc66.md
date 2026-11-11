
## WORKED-OUT PROBLEM 10.2

Write a program to read a line of text containing a series of words from the terminal.

The program shown in Fig. 10.2 can read a line of text (up to a maximum of 80 characters) into the string **line** using **getchar** function. Every time a character is read, it is assigned to its location in the string **line** and then tested for **newline** character. When the **newline** character is read (signalling the end of line), the reading loop is terminated and the **newline** character is replaced by the null character to indicate the end of character string.

When the loop is exited, the value of the index c is one number higher than the last character position in the string (since it has been incremented after assigning the new character to the string). Therefore, the index value c-1 gives the position where the **null** character is to be stored.

**Program**

```c
#include <stdio.h>
main()
{
    char line[81], character;
    int c;
    c = 0;
    printf("Enter text. Press <Return> at end\n");
    do
    {
        character = getchar();
        line[c] = character;
        c++;
    }
    while(character != '\n');
    c = c - 1;
    line[c] = '\0';
    printf("%s\n", line);
}
```

**Output**

```
Enter text. Press <Return> at end
Programming in C is interesting.
Programming in C is interesting.
Enter text. Press <Return> at end
National Centre for Expert Systems, Hyderabad.
National Centre for Expert Systems, Hyderabad.
```

**Fig. 10.2** *Program to read a line of text from terminal*

```c
string1[i] = '\0';
printf("\n");
printf("%s\n", string1);
printf("Number of characters = %d\n", i);
}
```

**Output**

```
Enter a string
?Manchester

Manchester
Number of characters = 10

Enter a string
?Westminster

Westminster
Number of characters = 11
```

**Fig. 10.3** *Copying one string into another*

## WORKED-OUT PROBLEM 10.4

The program in Fig. 10.4 shows how to write a program to find the number of vowels and consonants in a text string. Elucidate the program and flow chart for the program.

**Algorithm**

- Step 1 – Start
- Step 2 – Read a text string (str)
- Step 3 – Set vow = 0, cons = 0, i = 0
- Step 4 – Repeat steps 5-8 while (str[i]!='\0')
- Step 5 – if str[i] == 'a' OR str[i] == 'A' OR str[i] == 'e' OR str[i] == 'E' OR str[i] == 'i' OR str[i] == 'I' OR str[i] == 'o' OR str[i] == 'O' OR str[i] == 'u' OR str[i] == 'U' goto Step 6 else goto Step 7
- Step 6 – Increment the vowels counter by 1 (vow=vow+1)
- Step 7 – Increment the consonants counter by 1 (cons=cons+1)
- Step 8 – i = i + 1
- Step 9 – Display the number of vowels and consonants (vow, cons)
- Step 10 – Stop

### Flow Chart

![](img/11b034a94fc590add0a7808250a38792_359_0.png)

**Program**

```c
#include <stdio.h>
#include <conio.h>
#include <string.h>
void main()
{
    char str[30];
    int vow=0,cons=0,i=0;
    clrscr();
    printf("Enter a string: ");
    gets(str);
    while(str[i] != '\0')
    {
        if(str[i]=='a' || str[i]=='A' || str[i]=='e' || str[i]=='E' || str[i]=='i'
           || str[i]=='I' || str[i]=='o' || str[i]=='O' || str[i]=='u' || str[i]=='U')
            vow++;
        else
            cons++;
        i++;
    }
    printf("\nNumber of Vowels = %d",vow);
    printf("\nNumber of Consonants = %d",cons);
    getch();
}
```

**Output**

```
Enter a string: Chennai
Number of Vowels = 3
Number of Consonants = 4
```

**Fig. 10.4** *Program to find the number of vowel and consonants in a text string*

## 10.4 WRITING STRINGS TO SCREEN

### Using printf Function

We have used extensively the **printf** function with `%s` format to print strings to the screen. The format `%s` can be used to display an array of characters that is terminated by the null character. For example, the statement

```c
printf("%s", name);
```

can be used to display the entire contents of the array **name**.

We can also specify the precision with which the array is displayed. For instance, the specification

```
%10.4s
```

indicates that the *first four characters* are to be printed in a field width of 10 columns.

However, if we include the minus sign in the specification (e.g., `%-10.4s`), the string will be printed left-justified. The Program 10.4 illustrates the effect of various `%s` specifications.

## WORKED-OUT PROBLEM 10.5

Write a program to store the string “United Kingdom” in the array country and display the string under various format specifications.

The program and its output are shown in Fig. 10.5. The output illustrates the following features of the %s specifications.

- 1. When the field width is less than the length of the string, the entire string is printed.
- 2. The integer value on the right side of the decimal point specifies the number of characters to be printed.
- 3. When the number of characters to be printed is specified as zero, nothing is printed.
- 4. The minus sign in the specification causes the string to be printed left-justified.
- 5. The specification %.ns prints the first n characters of the string.

**Program**

```c
main()
{
    char country[15] = "United Kingdom";
    printf("\n\n");
    printf("*123456789012345*\n");
    printf(" ------- \n");
    printf("%15s\n", country);
    printf("%5s\n", country);
    printf("%15.6s\n", country);
    printf("%-15.6s\n", country);
    printf("%15.0s\n", country);
    printf("%.3s\n", country);
    printf("%s\n", country);
    printf(" ------- \n");
}
```

**Output**

```
*123456789012345*
-------
United Kingdom
        United Kingdom
         United
United
Uni
United Kingdom
-------
```

**Fig. 10.5** *Writing strings using %s format*

The **printf** on UNIX supports another nice feature that allows for variable field width or precision. For instance

`printf("%*.*s\n", w, d, string);`

prints the first **d** characters of the string in the field width of **w**.
This feature comes in handy for printing a sequence of characters. Program 10.5 illustrates this.

## WORKED-OUT PROBLEM 10.6

Write a program using for loop to print the following output:

```
C
CP
CPr
CPro
.....
.....
CProgramming
CProgramming
.....
.....
CPro
CPr
CP
C
```

The outputs of the program in Fig. 10.6, for variable specifications %12.*s, %.*s, and %*.1s are shown in Fig. 10.7, which further illustrates the variable field width and the precision specifications.

**Program**

```c
main()
{
    int c, d;
    char string[] = "CProgramming";
    printf("\n\n");
    printf("----------------\n");
    for( c = 0 ; c <= 11 ; c++ )
    {
        d = c + 1;
        printf("%-12.*s|\n", d, string);
    }
    printf("----------------|\n");
    for( c = 11 ; c >= 0 ; c-- )
    {
        d = c + 1;
        printf("%-12.*s|\n", d, string);
    }
    printf("----------------\n");
}
```

**Output**

```
    C
    CP
    CPr
```

Then,

```
x = ASCII value of '7' - ASCII value of '0'
  = 55 - 48
  = 7
```

The C library supports a function that converts a string of digits into their integer values. The function takes the form

```c
x = atoi(string);
```

**x** is an integer variable and **string** is a character array containing a string of digits. Consider the following segment of a program:

```c
number = "1988";
year = atoi(number);
```

**number** is a string variable which is assigned the string constant "1988". The function **atoi** converts the string "1988" (contained in **number**) to its numeric equivalent 1988 and assigns it to the integer variable **year**. String conversion functions are stored in the header file **`<stdlib.h>`**.

## WORKED-OUT PROBLEM 10.7

Write a program which would print the alphabet set a to z and A to Z in decimal and character form.

The program is shown in Fig. 10.8. In ASCII character set, the decimal numbers 65 to 90 represent upper case alphabets and 97 to 122 represent lower case alphabets. The values from 91 to 96 are excluded using an **if** statement in the **for** loop.

**Program**

```c
main()
{
    char c;
    printf("\n\n");
    for( c = 65 ; c <= 122 ; c = c + 1 )
    {
        if( c > 90 && c < 97 )
            continue;
        printf("%4d - %c ", c, c);
    }
    printf("\n");
}
```

**Output**

|   |   |   |   |   |   |
|---|---|---|---|---|---|
| 65 - A | 66 - B | 67 - C | 68 - D | 69 - E | 70 - F |
| 71 - G | 72 - H | 73 - I | 74 - J | 75 - K | 76 - L |
| 77 - M | 78 - N | 79 - O | 80 - P | 81 - Q | 82 - R |
| 83 - S | 84 - T | 85 - U | 86 - V | 87 - W | 88 - X |
| 89 - Y | 90 - Z | 97 - a | 98 - b | 99 - c | 100 - d |
| 101 - e | 102 - f | 103 - g | 104 - h | 105 - i | 106 - j |
| 107 - k | 108 - l | 109 - m | 110 - n | 111 - o | 112 - p |
| 113 - q | 114 - r | 115 - s | 116 - t | 117 - u | 118 - v |
| 119 - w | 120 - x | 121 - y | 122 - z |  |  |

*Fig. 10.8  Printing of the alphabet set in decimal and character form*

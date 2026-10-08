
## 3.4.1 Standard Input and Output

The standard input of characters is from a keyboard, and the standard output is to a monitor or a printer. The following sections show the standard input and output character data.

### Input of Character Data
The input function scanf is used to input characters from a keyboard. The input statement to input characters into the character variables ch1, ch2, and ch3 is as follows:

```c
scanf("%c%c%c",&ch1, &ch2, &ch3);
```

Notice that the format specifier %c is used in the format control string, because the variables ch1, ch2, and ch3 are declared as char variables. The address of the character variables must be specified in the input statement.

When the characters XYZ are entered the they are stored in ASCII as decimal codes as follows:

| Input | Storage | Meaning |
|---|---|---|
| X | ch1 -> 88 | 'X' |
| | ch2 -> 89 | 'Y' |
| Z | ch3 -> 90 | 'Z' |

There are no blanks between the characters XYZ as they are typed so no blanks are used between specifications in the format.

### Output of Character Data
The output function printf can be used to output characters to a monitor or a printer. The output statement to output the characters to the screen from the variables ch1, ch2, and ch3 is as follows:

```c
printf("%c %c %c",ch1, ch2, ch3);
```

Notice that the format specifier %c is used in the format control string, because the variables ch1, ch2, and ch3 are declared as char variables. To display or print characters you must use the %c format specifier.

The output appears on the screen as follows:

X Y Z

If the format specifier %d rather than %c, the output will appear as the ASCII decimal number as follows:

```c
printf("%d %d", ch1, ch2, ch3);
```

The output is as follows:

88 89 90

Notice that the format specifier %c understands the decimal number as an ASCII character code, and the format specifier %d simply prints the decimal numbers, which are the internal representations of the characters.

## 3.4.2 File Input and Output

Character data stored in a file on a disk can be input into the program. Data from a program can be written to a data file on an external storage device. The following examples show the input and output of character data.

### Input of Character Data from a Data File
The statements needed to input character data from a data file are as follows:

```c
FILE *inptr;
```

```c
inptr = fopen("myfile7.dat", "r");
```

```c
char ch1, ch2, ch3, ch4;
```

```c
fscanf(inptr,"%c%c%c%c", &ch1, &ch2, &ch3, &ch4);
```

The data read from the data file is as follows:

| myfile7.dat | |
|---|---|
| inptr -> 3 XY | |
| ch1 | ch2 | ch3 | ch4 |
| Character | 3 | | X | Y |
| ch1 | ch2 | ch3 | ch4 |
| ASCII code | 51 | 32 | 88 | 89 |

This data is read from the data file7.dat and stored in the variables ch1, ch2, ch3, and ch4 as shown. In the data file there is a blank space between the character 3 and the character X. Digits read using %c specification are stored as characters. The ASCII code is also stored for a blank space.

### Output of Character Data to a Data File
The statements needed to output character to a data file are as follows:

```c
char ch1='3', ch2=' ', ch3='X', ch4='Y';
```

```c
FILE *outptr;
```

```c
outptr = fopen("myfile8.dat", "w");
fprintf(outptr, "%c%c%c%c", ch1, ch2, ch3, ch4);
```

The data contained in character variables ch1, ch2, ch3, and ch4 is written to a data file myfile8.dat as follows:

![](img/8356e6c3bfe3b10354682c60b1e74b1d_179_0.png)

## 3.4.3 Unformatted Input and Output

getchar() and putchar() are the unformatted library functions for the input and output of characters from standard input and output devices. The getchar() function gets a single character from the keyboard, and the putchar() function places a single character in an output buffer, which will be displayed when the enter key is pressed on the keyboard. The getchar() function has no arguments, and the putchar() function has one argument. The getchar() function returns the value that it gets from a keyboard and stores it in internal form as an integer in the ASCII code. The following examples show the input and output of characters.

### getchar Function
The getchar() reads one character from the standard input. The function getchar() returns the EOF if there is no character to read. The EOF is indicated interactively by entering "ctrl Z" or "ctrl C". The EOF has a character code of -1, while all of the other characters have positive character. The following example shows the input of a character:

```c
char ch;
while((ch = getchar()) != EOF) {
    putchar(ch);
}
```

### putchar Function
The getchar() reads one character from the standard input. The function getchar() returns the EOF if there is no character to read. The EOF is indicated interactively by entering "ctrl Z" or "ctrl C". The EOF has a character code of -1, while all of the other characters have positive character.

## 3.4 Input and Output of Characters

```
The program displays the following output
5 6 7
```

The first three statements in Program 2.18 i.e.,

```
#define FIVE 5
#define SIX FIVE+1
#define SEVEN SIX+1
```

are macro definitions. They comprise of identifiers (i.e., FIVE, SIX and SEVEN) and their corresponding set-of-characters (i.e., 5, FIVE+1 and SIX+1). There may be any number of spaces between the identifier and the set-of-characters, but once the set-of-characters begins, there should not be any space in between them. They can be terminated by a new line.

During preprocessing, the identifiers (also referred to as the macro templates) are replaced by their respective set-of-characters (also referred to as the macro expansion), and assigning 5 for FIVE, 6 for SIX and so on.

Similarly, you can display messages using the #define directives. If the identifiers FIVE, SIX and SEVEN are encountered in the program following the macro definition, they are replaced by 5, 6 and 7 respectively. However, if the identifiers are encountered before the macro definition they are not replaced.

# Program 2.19 :

```
/* macro2.c */
#define A "X is Big"
#define B "Y is Big"
void main()
{
    int X, Y;
    printf("\n Enter value for X and Y : ");
    scanf("%d %d", &X, &Y);
    if (X > Y)
    printf(A);
    else
    printf(B);
}
```

```
The program displays the following output
Enter value for X and Y : 2 1
X is Big
```

From the output we see that x is greater than y and the program displays the message.

Before displaying the message the compiler preprocesses the identifier A and substitutes the string X is Big. Note that the string (set-of-characters) is enclosed in double quotes, hence for the compiler, the printf() function will actually appear to be

```
printf("X is Big") ;
```
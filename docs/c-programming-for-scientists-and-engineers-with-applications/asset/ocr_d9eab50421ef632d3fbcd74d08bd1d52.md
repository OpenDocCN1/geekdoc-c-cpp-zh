# 3.4 Input and Output of Characters

ter. The following example shows the input of a character using the
getchar( ) function.

```
char ch;
97 meaning a
getchar( );nch
```

Enter the character a, it is stored in ch as 97, because the ASCII code for character
a is 97. The getchar( ) function converts the character to ASCII and returns the
corresponding ASCII code.

putchar Function The following example shows the output of a character using
tputchar( ) function.

```
char ch;
88 meaning X
putchar(ch);
ch
```

The char variable ch contains the ASCII code for character X as shown. This out-
p statement displays the character X on the CRT screen as shown.
The example example shows the input and output of the following string of
characters.

Input string: COMPUTERS ARE ELECTRONIC

```
char ch;
while(( ch = getchar( )) != '\n')
putchar(ch);
```

When this code is executed it asks for the input from the keyboard. Then the char-
acters above are entered from the keyboard one after the other. After all the
characters are entered, the carriage return is entered. The output of the characters
entered is displayed on the screen as follows:

Output string: COMPUTERS ARE ELECTRONIC

In C, an assignment such as ch = getchar( ) has a value, the same value that
is being assigned.
When the character data is entered the getchar( ) function inputs the charac-
ters by one into the variable ch and then the output function putchar( )
writes the character contained in the variable ch to an output buffer. When the
```
char name;
name = getchar();
```

Will assign the character 'H' to the variable name when we press the key H on the keyboard. Since getchar is a function, it requires a set of parentheses as shown.

# EXAMPLE 1.23 The program in Fig. 1.76 shows the use of getchar function in an interactive environment.

The program displays a question of YES/NO type to the user and reads the user's response in a single character (Y or N). If the response is Y or y, it outputs the message

My name is BUSY BEE

otherwise, outputs

You are good for nothing

NOTE: There is one line space between the input text and output message.

```
Program
#include <stdio.h>
main()
{
char answer;
printf("Would you like to know my name?\n");
printf("Type Y for YES and N for NO: ");
answer = getchar(); /* .... Reading a character.... */
if(answer == 'Y' || answer == 'y')
printf("\n\nMy name is BUSY BEE\n");
else
printf("\n\nYou are good for nothing\n");
}

Output
Would you like to know my name?
Type Y for YES and N for NO: Y
My name is BUSY BEE
Would you like to know my name?
Type Y for YES and N for NO: n
You are good for nothing
```

Fig. 1.76 Use of getchar function to read a character from keyboard

The getchar function may be called successively to read the characters contained in a line of text. For example, the following program segment reads characters from keyboard one after another until the 'Return' key is pressed.

```
char character;
character = ' ';
while(character != '\n')
{
    character = getchar();
}
```
# Example 3.13

Write a program to read the name of a person and display it on the screen.

# Solution 3.13

The required program listing (Program: name.c) is shown in Figure 3.23. The user entered name is read by scanf and stored in character array name and then displayed on the screen.

```
/*------------------------------------------------
NAME
====
This program shows how strings can be used in a program

Author: Dogan Ibrahim
File : name.c
Date : December 2020
--------------------------------------------------*/
#include <stdio.h>

int main(void)
{
 char name[30];

 printf("\nEnter your name: ");
 scanf("%s", name);

 printf("Your name is %s\n", name);

 return 0;
}
```

Figure 3.23 Program name.c

An example run of the program is shown in Figure 3.24.

```
Enter your name: John Smith
Your name is John
pi@raspberrypi:~ $
```

Figure 3.24 An example run of the program

Notice that even though we entered the name as John Smith, it is displayed as John only. This is because the scanf function terminates while reading a text when white space is encountered. The solution to this problem is to use the fgets function to read text with white spaces, or to change the scanf function as follows so that the text is read until the
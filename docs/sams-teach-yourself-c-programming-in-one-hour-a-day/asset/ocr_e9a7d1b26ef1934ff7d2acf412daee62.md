# Analysis

This program uses a switch statement with cases based on the choices of onscreen menu. Line 14 calls the menu the first time and sets a value in a command variable from it. If the value is anything other than 5, a while loop is executed. This while loop primarily a switch statement that executes different code base based on the command selected from the menu. When the appropriate case is executed, the menu is replayed and a new command is obtained on line 56.

Having "fall through" parts of a switch construction can be useful at times. Say, for example, that you want the block of statements executed if one of several values are encountered. Simply omit the break statements and list all the case templates before the statements matches any of the case conditions, execution "fall through" the following case statements until it reaches the block of code you execute, as shown in Listing 13.8.

# Input

Listing 13.8 Another Way to Use the switch Statement

```
/* Another use of the switch statement. */
#include <stdio.h>
#include <stdlib.h>

int main( {
	int reply;
	while (1) {
		puts("nEnter value between 1 and 10, 0 to exit: ");
		scan("%d", &reply);
	switch(reply)
	{
		case 0:
		exit(0);
		case 1:
		case 2:
		case 3:
		case 4:
		case 5:
		puts("You entered 5 or below.\n");
		break;
		}
	case 6:
```
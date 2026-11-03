# following code to see how the do/while code will work.

```
```c
#include <stdio.h>

Int main()
{
Char ch:
Ch = 'A';
Do
{
Putchar(ch);
Ch++;
}
While (ch != 'z');
Putchar('
');
Return(0);
}
```
```

You will notice that the do/while loop is going to start with line 9 with the statement “do. this one doesn’t have a condition because the statements are going to be executed one right after the other. Then you can see that the while condition is going to appear at your 14th line. The loop is going to rely on the ch variable as the condition and it is first initialized at line 7 before being manipulated at line 12. Take a moment to build and then run this code in your compiler.

In this one, the 'z' won’t be printed because it is considered an exit condition. If you would like to see the 'z' in your code, you will need to save the exit condition to 'z+1' at the end of your code. Now with this one, you are basically creating an endless loop because it has the plus one. If you built and tried to run this one, you would end up in an endless loop and would need to press Ctrl + C in order to get out of the program.
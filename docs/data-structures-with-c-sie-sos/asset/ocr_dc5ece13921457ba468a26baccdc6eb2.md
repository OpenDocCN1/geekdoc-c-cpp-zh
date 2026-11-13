There is no way to know the content of the cell unless the data type of X is known.
(a) Suppose X is declared to be of character type and EBCDIC is used. Then the four characters %GO% are stored in X.
(b) Suppose X is declared to be of some other type, such as integer or real. Then an integer or real number is stored in X.

The following C program demonstrates how the same value is interpreted differently based on different associated data types:

# Program 2.6

```
#include <stdio.h>
#include <conio.h>

void main()
{
char c1='1';
int c2=1;
clrscr();

printf("c1 (char) = %c \\nc1's ASCII value = %d\\nc2 (int) = %d",c1,c1,c2);
getch();
}
```

Output:
c1 (char) = 1
c1's ASCII value = 49
c2 (int) = 1

In the above program, variable c1 treats 1 as a character while variable c2 treats 1 as an integer.

# Local and Global Variables

The organization of a computer program into a main program and various subprograms has led to the notion of local and global variables. Normally, each program module contains its own list of variables, called local variables, which can be accessed only by the given program module. Also, subprogram modules may contain parameters, variables which transfer data between a subprogram and its calling program.

# Example 2.12

Consider the procedure SWITCH(AAA, BBB) in Example 2.10. The variables AAA and BBB are parameters; they are used to transfer data between the procedure and a calling algorithm. On the other hand, the variable TEMP in the procedure is a local variable. It “lives” only in the procedure; i.e., its value can be accessed and changed only during the execution of the procedure. In fact, the name TEMP may be used for a variable in any other module and the use of the name will not interfere with the execution of the procedure SWITCH.
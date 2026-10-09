# # File Level Storage

To understand how file-level storage works, we have to consider how a program is compiled and run. The compiler reads the C code and for each C instruction it outputs a number of lower-level machine code instructions. These instructions are simply bit patterns and only differ from data in that they are examples of machine code instructions and the processor can read and obey them.

That is, a program is just data you can execute.

The output of the compiler is a binary file and to run the program the loader simply loads the file into the correct location in memory and then makes the processor jump to the address of the first instruction.

The fact that the program file is just a binary file that is loaded into memory means that it is possible to include data within it for the program to work with. That is, memory locations within the program can be used to store data. Usually the compiler arranges to store all of the data together in one area of the file and so we have the idea of a data block and a code block. Depending on the system and the compiler there can be multiples of both types of block in a single binary file.

File-level variables are stored in the binary file that the compiler generates and are stored within the program. Thus they are neither automatic variables stored on the stack nor are they heap variables. A file-level variable is defined by being declared outside of a block, i.e. outside of a function. This means that the declaration is at the top of the file of code and hence a “file-level variable”. For example:

```
```
#include <stdio.h>
#include <stdlib.h>

int a = 42;

int main(int argc, char **argv)
{
	int b = 314159;
	printf("%d,%d", a, b);
	return 0;
}
```
```

The variable **a** is declared at the file level and variable **b** is an automatic local variable. Recall that in C the main “program” is just another function and variables declared within it are automatic and stored on the stack. Variable **a** is compiled into the data area of the program and isn’t allocated space on the stack or the heap – it is part of the program file. It is also initialized when the program file is loaded. As it is part of the program, **a** has the maximum lifetime – it lives until the program terminates and the

106
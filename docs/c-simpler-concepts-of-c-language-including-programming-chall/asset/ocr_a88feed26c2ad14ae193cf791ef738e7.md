# 96 C-SIMPLER

```
{
register int upper;
}
```

should only be used for variables that require faster access. However, the register specify only can give a suggestion to the compiler. A variable specified by the register keyword is not guaranteed to be stored in a register. The compiler can ignore the suggestion if there is no register available, or if some other restrictions have to apply.

# 6.1.4. extern

extern qualifier defines a global variable that is visible to all object modules (all .o files). When ‘extern’ keyword is used, the variable cannot be initialized (No declaration initialization is permitted; it can be initialized after declaration!) during declaration.

To prove this conceptually, couple of code snippets required Program 6.5 has both the snippets covered.

+   - Two files 1.c and 2.c are created.
- 1.c has a global variable ‘count’ is called from 2.c, where ‘extern int count’ is used. It says that the variable count has been declared in some external file, in this case it is ‘1.c’.
- When the function write () is called, it will fetch the value for count from file 1.c is 5.

To execute and check, following steps need to be executed! (gcc is the best weapon to handle the situation which involves extern keyword.)
Note: If the user has installed Dev-Cpp, the gcc class is defined by default and hence, he/she can execute the following commands from Windows – Command prompt itself. (To do so, go to Start->Run->cmd. Then using ‘gcc’, go to the path where the gcc has been installed. Finally, execute the following commands.) If the user doesn’t have Dev-Cpp software, they can execute the commands in Linux OS.

+   - Compile 1.c, 1.o will be generated. (gcc -c 1.c)
- Compile 2.c, 2.o will be generated. (gcc -c 2.c)
- Link 1.o and 2.o, generate executable file. (gcc -o output 1.o 2.o), where output is executable file name.
- Run the executable file with ./output. (In Dev-Cpp-Windows pair, just typing ‘ou put’ will fetch the answer!)

The execution on completion, will the output printed as “the count is 10”. This is how extern can be used.
```
str=0x0) at bugged.c:29
#1 0x00000000004005e3 in main () at bugged.c:20
(gdb) backtrace
#0 0x000000000040063b in get_input (prompt=0x400704 "Enter a string: ", str=0x0) at bugged.c:29
#1 0x00000000004005e3 in main () at bugged.c:20
(gdb)
```

The output of the command shows that the program was at location (memory address) 0x000000000040063b at line 30 in the get_input() function when it received the SIGSEGV signal. The stack frame shows that the call sequence is main() => get_input() and the program was executing the *str=getchar() statement at line 29 when it crashed (see the program listing in the previous section). Note that the code on this line has two assignment statements and one comparison statement. In all of these statements, we dereference the string pointer str. Two statements use the C library function getchar(). This library function is well tested and has been in use for many years. Thus, the problem must be with the pointer variable str. We pursue this issue in a later section.

# 14.7.1.6 Setting Breakpoints

Viewing execution of all or part of your code statement by statement is called program/code tracing. In order to trace code, you need to set breakpoints in your program. You can trace a program up to a particular statement or function by using the break command, as described in Table 14.1. It allows you to run a program without interruption until the control reaches the line or function that you want to study more closely. The process of stopping a program in this way is known as setting breakpoints. As shown in the previous section, the main function starts at line 14 but its first executable statement is at line 18. We set the breakpoint at the first executable statement in main() and run the program. The program stops execution at line 18, the only breakpoint we have set, having statement null_function1();

```
(gdb) break main
Breakpoint 1 at 0x4005be: file bugged.c, line 18.
(gdb) run
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /home/sarwar/linux2e/ch14/bugged

Breakpoint 1, main () at bugged.c:18
18            null_function1();
(gdb)
```

# 14.7.1.7 Single-Stepping through Your Program

Always set breakpoints in your program to be able to view execution of all or part of your code statement by statement. The process of tracing program execution statement by statement is known as single-stepping through your program. Single-stepping, combined with tracing of variables, allows you to study program execution closely. Single-stepping can be done with the step command, which executes the next program statement, stepping into a function if the statement is a function call. You can use the next command to single-step through your code, but it executes a function into its entirety. If you are tracing a variable, it shows you the value of the variable when a statement within the scope of the variable executes. Run the help scope command to get more information about the scoping rules.

After setting the breakpoint at main and running the program in the previous session, we then run each statement of the program one by one using the next command. After the third next statement, the control reaches the call to the get_input (PROMPT, temp); function at line 20 in the main() function. We then use the step command to step into and execute each statement in the get_input() function. The first step command takes control to the first executable statement in the get_input() function, the for loop. The second step statement prompts you for keyboard input. As soon as you hit <Enter> after typing Hello World!, the system displays the error message Program received signal SIGSEGV, Segmentation fault along with
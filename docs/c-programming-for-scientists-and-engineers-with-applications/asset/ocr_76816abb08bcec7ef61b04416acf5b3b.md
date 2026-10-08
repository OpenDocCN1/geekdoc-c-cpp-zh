# 368 Storage Classes

File B:
extern int a;
/* a is made visible */

```
void func2(void)
{
    a = a + 10;
    printf("In func2 %d\n", a);

    return;
}
```

The output is as follows:

In func1 a = 15
In main a = 20
In func2 a = 30
In main a = 55

Note that in C multiple files can be compiled and linked using the command line of the computer. The program execution always begins in the file where the main function is located. Also, if you are using a windows-driven compiler (such as DEV-C++ 4.9.9.2), each of the C source files must be included in a Project file in order for the extern variables to cross file boundaries. Once a Project is assembled, the program can be executed by compiling and running the Project. Note that the extern variable a is defined in File A before the func definition. It is global to func1; therefore, it is visible inside func1, assigned a value of 15, and it is printed inside func1. The variable, a, is not visible in main so it is declared extern inside main to make it accessible. It is changed in main and printed. The variable defined in File A is declared in File B as an extern variable. It must be declared extern to avoid allocating storage for it in File B. Func2 in File B can access the variable defined in File A. The output of a inside func2 shows that it is accessible in File B.

File A:
#include <stdio.h>

```
void func1(void);
void func2(void);
```

```
int main()
{
```

```
    extern int a;
    extern int b;
    func1();
```
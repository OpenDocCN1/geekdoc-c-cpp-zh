Suppose our program consists of many files and in file first.c, we have defined many variables that may be needed by other files also. We can put an extern declaration for each variable in every file that needs it. Another better and practical approach is to collect all extern declarations in a header file and include that header file in the files, which require access to those variables.

# 14.2.3 Static

There are two types of static variables-

+   (1) Local static variables
+   (2) Global static variables

# 14.2.3.1 Local Static Variables

The scope of a local static variable is same as that of an automatic variable i.e. it can be used only inside the function or block in which it is defined. The lifetime of a static variable is more than that of an automatic variable. A static variable is created at the compilation time and it remains alive till the end of a program. It is not created and destroyed each time the control enters a function/block. Hence a static variable is created only once and its value is retained between function calls. If it has been initialized, then the initialization value is placed in it only once at the time of creation. It is not initialized each time the function is called.

A static variable can be initialized only by constants or constant expressions. Unlike automatic variables, we can’t use the values of previously initialized variables to initialize static variables. If a static variable is not explicitly initialized then by default it takes initial value zero.

```
```c
int x = 8;
int y = x; /*Valid*/
static int z = x; /*Invalid, initializer should be constant*/
```
```

Let us take a program to understand the use of local static variables. This program is similar to P14.2 but here x and y are declared as static variables.

```
```c
/*P14.5 Program to understand the use of local static variables*/
#include<stdio.h>
main()
{
func();
func();
func();
}
func()
{
static int x=2,y=5;
printf("x=%d,y=%d\n",x,y);
x++; y++;
}
```
```

**Output:**
x = 2, y = 5
x = 3, y = 6
x = 4, y = 7

Note that the effect of initialization is seen only in the first call. In subsequent calls initialization is no
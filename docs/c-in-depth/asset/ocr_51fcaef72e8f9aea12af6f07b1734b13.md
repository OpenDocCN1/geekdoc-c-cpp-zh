# 14.3 Storage Classes in Functions

The storage class specifiers extern and static can be used with function definitions. The definition of a function without any storage specifier is equivalent to its definition with the keyword extern i.e. by default the definition of a function is considered external. If a function is external then it can be used by all the files of the program and if it is static then it can be used only in the file where it is defined.

If an external function is to be used in another file, then that file should contain function declaration and it is a good practice to specify extern in that declaration.

```
```c
first.c
main()
{
    ........
}
float func1(int)
{
    ..........
}
```
```

```
```c
second.c
extern float func1(int);
func2()
{
    ..........
}
static int func3(int)
{
    ..........
}
```
```

```
```c
third.c
void func4()
{
    ..........
}
void func5()
{
    ..........
}
```
```

Here the function func1() is defined in file first.c. Its declaration is put in file second.c, so it can be used in this file also. The function func3() in file second.c is defined as static so it can't be used by any other file. Generally declarations of all functions are collected in a header file and that header file is included in other files.

# 14.4 Linkage

There are three types of linkages in C-

+   (a) External linkage
+   (b) Internal linkage
+   (c) No linkage

Local variables have no linkage, so their scope is only within the block where they are declared. Global variables and functions have external linkage, so they can be used in any file of the program. Static global variables and static functions have internal linkage, so their scope is only in the file where they are declared.

# 14.5 Memory During Program Execution

The register variables are stored in CPU registers and rest of the variables are stored in memory. Now let us see how memory is organized when a C program is run.

Code Area: This area is used to store executable code of the program. The size of this area does not change during run time.

Data Area: This area stores static and global variables. It is further subdivided into two areas viz. initialized data area and uninitialized data area. The initialized data area stores all the initialized static and global
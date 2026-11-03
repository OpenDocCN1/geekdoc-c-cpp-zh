
## 14.3 Storage Classes in Functions

The storage class specifiers extern and static can be used with function definitions. The definition of a function without any storage specifier is equivalent to its definition with the keyword extern i.e. by default the definition of a function is considered external. If a function is external then it can be used by all the files of the program and if it is static then it can be used only in the file where it is defined.

If an external function is to be used in another file, then that file should contain function declaration and it is a good practice to specify extern in that declaration.

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

Here the function func1() is defined in file first.c. Its declaration is put in file second.c, so it can be used in this file also. The function func3() in file second.c is defined as static so it can't be used by any other file. Generally declarations of all functions are collected in a header file and that header file is included in other files.

## 14.4 Linkage

There are three types of linkages in C-

- (a) External linkage
- (b) Internal linkage
- (c) No linkage

Local variables have no linkage, so their scope is only within the block where they are declared. Global variables and functions have external linkage, so they can be used in any file of the program. Static global variables and static functions have internal linkage, so their scope is only in the file where they are declared.

## 14.5 Memory During Program Execution

The register variables are stored in CPU registers and rest of the variables are stored in memory. Now let us see how memory is organized when a C program is run.

Code Area: This area is used to store executable code of the program. The size of this area does not change during run time.

Data Area: This area stores static and global variables. It is further subdivided into two areas viz. initialized data area and uninitialized data area. The initialized data area stores all the initialized static and global variables while the uninitialized data area stores all the uninitialized static and global variables. The reason for division of this area is that all uninitialized variables can be collectively assigned value zero. The size of data area is also fixed and does not change during run time.

| Code | Code of the program |
|---|---|
| Initialized Data | Initialized static variables<br>Initialized global variables |
| Uninitialized Data | Uninitialized static variables<br>Uninitialized global variables |
| Heap | Dynamically allocated memory |
|  |  |
| Stack | Initialized and uninitialized automatic variables |

### Memory during execution of the program

Heap: This area is used for dynamically allocated memory. It is the responsibility of the program to allocate memory from the heap. The size of this area is dynamic i.e. it may change during run time

Stack: Automatic variables are stored in this area. The size of this area keeps on changing during time.

The following table summarizes all the features of storage classes-

| Keyword | Place of declaration | Lifetime | Scope | Initial Value | Place of storage | Linkage | Initializable |
|---|---|---|---|---|---|---|---|
| auto (or none) | Inside Function /Block | Function /Block | Function /Block | Garbage | Memory (stack) | None | Constant Variable |
| register | Inside Function /Block | Function /Block | Function /Block | Garbage | Registers | None | Constant Variable |
| static (local) | Inside Function /Block | Program | Function / Block | Zero | Memory (data area) | None | Const |
| (none) | Outside function (Definition of external variable) | Program | Definition to end of file (can be shared in other files using extern declaration) | Zero | Memory (data area) | External | Const |
| extern | Outside or inside function (Declaration of external variable) | Program | Declaration to end of file / Function | - | Memory (data area) | External | Can't be initialized |
| static (global) | Outside function | Program | Definition to end of file (can't be shared in other files using extern declaration) | Zero | Memory (data area) | Internal | Constant |

## 14.6 const

If any variable is declared with const qualifier, then the value of that variable can't be changed by the program. The const qualifier can occur in the declaration before or after the data type. For example-

```
const int x = 9;
int const x = 9;
```

Both these declarations are equivalent and declare x as a const variable. Any attempt to change the value of this variable in the program will result in an error. For example these statements are invalid-

```
x = 10;    /*Invalid*/
x = func(); /*Invalid*/
x++;      /*Invalid*/
```

The const qualifier informs the compiler that the variable can be stored in read only memory. A const variable can be given a value only through initialization or by some hardware devices. Note that the value of a const variable can't be modified by the program, but any external event outside the program can change its value.

If an array, structure or union is declared as const then each member in it becomes constant. For example-

```c
const int arr[5] = { 10, 11, 12, 13, 14 };
const struct { char x; int y; float z; } var = { 'A', 12, 29.5 };
arr[2] = 22;          /*Invalid*/
var.x = 'B';          /*Invalid*/
```

The const variables are not true compile time constants in C. So we can't use const variables where constant expressions are required e.g. in array dimensions or case labels.

For example the following code is invalid in C.

```c
const int size=10;
int arr[size];
```

The const qualifier can be useful while passing array arguments to functions. We know that when an array is passed as an argument, the function gets access to the original array and can modify it. If we don't want the function to make any changes in the array then we can declare the array as const in the formal parameter list.

```
func( const char arr[] )
{
    ........
}
```

Now we'll see how to use const in pointer declarations. We can declare three types of pointers using the qualifier const.

- (i) Pointer to const data
- (ii) const pointer
- (iii) const pointer to const data

Consider these declarations-

```
const int a = 2, b = 6;
const int *p1 = &a;    /* or int const *p1 = &a; */
```

Here p1 is declared as a pointer to const integer. We can change the pointer p1 but we can't change the variable pointed to by p1.

```
*p1 = 9;          /*Invalid*/
p1 = &b;          /*Valid since p1 is not a constant itself*/
```

Now consider these declarations-

```
int a = 2, b = 6;
int *const p2 = &a;
```

Here p2 is declared as a const pointer. We can't change the pointer variable p2, but we can change the variable pointed to by p2.

```
*p2 = 9;          /*Valid*/
p2 = &b;          /*Invalid since p2 is a constant*/
```

Now consider these declarations-

```
const int a=2, b=6;
const int const *p3=&a;
```

Here p3 is declared as a const pointer to const integer. We can neither change the pointer variable p3 nor the variable pointed to by it.

```
*p3 = 9;          /*Invalid*/
p3 = &b;          /*Invalid*/
```

So the three different types of declarations of pointers using const are-

```
int const *ptr;  or  const int *ptr;          /* pointer to const integer */
int *const ptr;                              /* const pointer to an integer */
const int *const ptr;                        /* const pointer to a const integer */
```

The following example will further clarify this concept.

```c
char str1[] = "wealthy";
char str2[]="strong";
const char *pc=str1;    /*pointer to const*/
char *const cp=str1;   /*const pointer*/
const char *const cpc=str1;  /*const pointer to const*/
```

```
pc=str2;    /*Valid*/
cp=str2    /*Invalid*/
cpc=str2;  /*Invalid*/
```

```
*pc='h';  /*Invalid*/
*cp='h';   /*Valid*/
*cpc='h';  /*Invalid*/
```

If we want to assign the address of a const variable to a non const pointer, then we'll have to use cast operator. For example-

```
const int a = 10;
int *ptr;
ptr = (int *)&a;
```

Now if we try to change the value of variable a indirectly through ptr then the result is undefined and there can be a run time error.

```
*ptr = 12;    /* undefined*/
```

## 14.7 volatile

Whenever a variable is encountered in the program, compiler reads the value of that variable from the memory. But sometimes for optimization purposes the compiler stores the value of the currently used variable in any unused register. Now when that variable is encountered next time in the program and the compiler sees that the program has not changed value of the variable, it reads the value from the register instead of the memory. This process saves time since accessing a register is faster than accessing memory.

This sort of automatic optimization by the compiler may sometimes lead to incorrect results. This generally happens when the value of a variable can be modified by some external process outside the program. These types of situations arise when we have memory mapped I/O, variables shared among multiple processes or variables that can be modified by interrupt routines.

For example suppose we have a variable time that represents current system time and its value is controlled by the system clock. Now consider this loop- while( time != T ) /* Do nothing till value of variable time equals T*/

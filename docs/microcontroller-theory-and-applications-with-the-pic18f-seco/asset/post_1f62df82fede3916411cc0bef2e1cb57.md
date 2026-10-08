
![](img/5e76fd429fabd2b62e16a7bfd8cf546f_97_0.png)

**FIGURE 4.6** Flowchart for the for loop

### 4.5.8 The do-while construct

The C language provides another loop structure called the do-while. The syntax for the do-while construct is provided below:

```
do {
    statements
} while (condition);
```

Figure 4.7 shows the flowchart for the do-while construct.

The do-while loop is a post-checked loop (condition is checked afterwards) in the sense that the exit condition is evaluated after executing all statements. If the condition evaluates to False, the loop terminates. Otherwise, the process continues until the condition becomes false. Whatever is accomplished by a do-while construct can be achieved by a for loop construct. Hence, this loop structure is not as popular as while or for loop structures.

### 4.5.9 Structures, and Unions

In addition to built-in data types such as char and int, C supports user-defined data types. A structure permits the programmer to access a group of different data types using a common user-defined name. The structure can be declared using the keyword `struct` followed by a user-defined name. An example of the structure declaration is provided below:

```
struct struct_name {
    int a;
    char b;
} my_struct;
```

Note that in the above, the name is optional. However, if it is present, it defines the tag or user-defined name of the structure, and the tag can be used later. The variable name `my_struct` is of type `struct_name`. Also, Size of the structure = Sum of the sizes of its components. Hence, Size of the above structure = Size(int) + Size(char) = 2 bytes + 1 byte = 3 bytes.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_98_0.png)

Union is a space saving structure. The memory referenced by the keyword `union` can store different types of data with the restriction that at any one time, the memory holds a single type of data. Note that different data types of the union share the same memory space. The data in a union must be referenced by a member of the proper data type. As an example, a union can be declared as follows:

```
union num {
    char x;
    int a;
};
```

Note that Size of a union = Size of the largest data type held by the union. In the above, Size of the union "num" = Max {size of (int), size of (char)} = Max {2, 1} = 2 bytes. In the above code, any variable of type `union num` can hold a char or an int. The names 'x' and 'a' specify which type of data is referenced. To specify a variable `y` of type `union num`, the following statement can be used:

```
union num y;
```

Now, a character B can be assigned to x using the following:

```
y.x = 'B';
```

Next, an integer 2756 can be assigned to a using the following:

```
y.a = 2756;
```

Since at any one time y holds data of a single type, the assignment of 2756 to y cancels the assignment of 'B' to y.

As mentioned before, Union offers a space saving structure. For union variable, memory space is allocated to hold the largest number. This memory can then be used to hold the smaller numbers. As an example, consider the following:

```
union {
    int a;
    char c[2];
} myu;
```

In the above union, 16 bits of memory space are allocated to integer 'a'; the same storage space is shared by 8-bit characters c[0] and c[1] as shown in Figure 4.8.

### 4.5.10 Functions in C

A function in C is similar to subroutine in assembly. Hence, a function is a block of C codes that performs a particular task. There are two types of functions in C. They are Standard library functions and User defined functions. The Standard library functions are contained in the C compilers. They handle tasks such as mathematical computations and I/O processing. These functions are defined in the compiler's header file. For example, the "printf()" is defined as a standard library function in the C compiler's "stdio.h" header file. The “printf()” outputs formatted data on the screen.

User-defined functions are defined by the programmers. An example of a user-defined function “minus()” is provided in the following:

```c
#include <stdio.h>
int minus (int m, int n); // function prototype
main ( ) {
    int a = 5;
    int b = 3;
    int result;
    result = minus (a, b); //function call
    printf (“result = %d”, result);
    return 0;
}
int minus (int m, int n)
{
    int subtract;
    subtract = m - n;
    return subtract; // return statement
}
```

In the above, “int minus (int m, int n)” is called the function prototype which specifies in the above, the return type of the function as “int”, function name as “minus ( )” and two arguments (m, n) of type “int” are passed to the function. The function prototype is not required if the user-defined function is defined before the “main ( )” function.

In the above example, the function is called using `minus(a, b)` which is a statement inside the `main()`. After the function call, program control is transferred to the user-defined function.

The arguments mean the variables are passed to the function. In the above example, two variables ‘a’ and ‘b’ are passed during function call. The parameters ‘m’ and ‘n’ accept the passed arguments in the function definition since they are of the same type (int).

The return statement ends the execution of a function and returns the value to the calling function. The program control is transferred to the calling function after the return statement. In the above example, the value of the variable “subtract” is returned to the variable “result” in the `main()` function.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_99_0.png)

**FIGURE 4.8** Example of space saving with union

### 4.5.11 Arrays

An array contains a number of the same type of data elements stored under a common name in consecutive memory locations. The same type of data elements means that data elements can be, for example, character (char) elements or integer (int) elements. The size of each element in the array can be 8-, 16- or 32-bit. Arrays can be one-dimensional (table) or two-dimensional (matrices). One-dimensional arrays will be considered in this discussion.

An array is specified by an array type, array name, and array elements. If the array stores integer data, then the array type is “int”. On the other hand, if the array stores characters, then the array type is “char”.

An array is assigned with a name comprised of a string of characters. The elements of an array are stored within curly brackets. The first element of the array is identified as element 0, the second element as element 1, the third element as element 2, and so on.

An example of creating an array containing 10 BCD numbers is provided below:

```
unsigned char table [10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
```

In the above, the array name is “table” with element 0 as 0, element 1 as 1, and so on.

### 4.5.12 Macros

Macros can make programming in C easier by reducing the amount of code the programmer has to actually write. This is accomplished by letting the compiler produce those redundant pieces of program that are used routinely in various places in the program. Basically a macro is a set of codes used repeatedly throughout the program. When the macro is written, it is assigned a name. Rather than writing the same sequence of codes each time they are needed, the name of the macro is inserted in their place. During compiling whenever the name of the macro is encountered, the compiler will insert the sequence of codes that this name represents.

The macro is in some way similar to a function, in that the usage is repeated. As an example, consider the following macro:

```
#define MPY10(X) (X << 3) + (X<< 1)
```

This macro multiplies X by 10 using two left shift operations discussed earlier. A typical macro call is `Z = MPY10(Y);`

Note that there is no transfer of control in macro. In contrast, a function call is performed via transfer of control in the program. The C compiler expands the macro in the program. For example,

```
Z = MPY10 (A) + MPY10 (B) is expanded as
Z = (A<<3) + (A<< 1) + (B<<3) + (B<<1);
```

Macros are faster than functions or subroutines since there is no overhead in macro associated with transfer of control.

## 4.6 Choosing a programming language

Compilers used to provide inefficient machine codes for microprocessors because of the general guidelines that must be followed for designing them. However, modern C compilers with microcontrollers generate very tight and efficient codes. Some of the other advantages


void main()
{
 printf("The size of the union is %d\n", sizeof(u1));
 printf("The size of the structure is %d", sizeof(s1));
}

The program displays the following output
The size of the union is 15
The size of the structure is 23

### 2.10.1 Initializing a Union

There is a major difference between union and structures in terms of storage. In structures, each member has its own storage location whereas all the members of a union occupy the same memory location (i.e., The union stores all the values of its members in a single location). This states that, although a union may contain many members of different data types, it can handle only one member at a time. Hence, you can initialize only one member in a union. If you try to initialize more than one member, the last initialized value will be assigned to all of its members.

### Program 2.13

```
/* Program to demonstrate initialization of a union. */
/* initial.c */
union exam
{
 int roll_no, mark1, mark2, mark3;
}u1;
void main()
{
 u1.roll_no = 252;
 u1.mark1 = 89;
 printf("Roll No : %d\n", u1.roll_no);
 printf("Mark 1 : %d\n", u1.mark1);
 printf("Mark 2 : %d\n", u1.mark2);
 printf("Mark 3 : %d\n", u1.mark3);
}
```

The program displays the following output
Roll No : 89
Mark 1 : 89
Mark 2 : 89
Mark 3 : 89

Note that in the program even the uninitialized members (i.e., mark2 & mark3) take the same value as its other members.

## 2.11 Storage Classes

In C, all classes have data types and storage classes. Data type refers to the type of information represented by a variable (i.e., int, char, etc.). Storage classes determine the storage of the variable, initial value of the variable if not initialized, life of the variable (i.e., how long the variable would be active in the program) and the scope of variables within the program. Scope of a variable is defined as the region over which the variable is visible or valid. Scope is usually established by a set of curly braces. Any variable declared in C have only one of the four storage classes. They are,

- Automatic storage class
- Register storage class
- Static storage class
- External storage class

### 2.11.1 Automatic Storage Class

Variables defined inside a block and are local to the block in which they are declared, are referred as automatic variables or local variables. Automatic variables can only be accessed by the block in which they are declared. Any another block cannot access its value.

When declaring a local variable inside a block, it is more precise in C to use the keyword auto before the declaration of the variable. The following statement is an example for local variable declaration:

```
auto int number;
```

These variables are created as new variables each time the block is executed, and they are destroyed when the block encounters a return statement or the closing brace of the block. The life of the variable will be inside the block in which it is declared. The C compiler treats any variable declared inside a block as an automatic variable by default. So the keyword auto is not necessary along with the variable declaration. Automatic variables are stored in memory. When an automatic variable is not initialized, it takes an unpredictable value referred as garbage value. Program 2.14, illustrates the scope and life of automatic variables.

### Program 2.14

```
/* auto.c */
#include<stdio.h>
void main()
{
    auto int x = 5;
    {
        auto int x = 4;
        {
            auto int x = 3;
            printf("%d \t",x);
        }
        printf("%d \t",x);
    }
    printf("%d \t",x);
}
```

The program displays the following output

3 4 5

Since all printf() functions occur within the block in which it is defined, x is local to the block. Note that the default storage class of a variable defined inside a function is auto. Also note that values passed to the function as arguments are also considered as local variables.

### 2.11.2 Register Storage Class

The register storage class is similar to the auto storage class since the variables defined inside a block are local to the block in which it is specified. Register variables can only be accessed by the block in which it is declared. Its value cannot be accessed by any other function. When declaring a register variable inside a block, it is more precise in C to use the keyword register before the definition of the variable.

The following statement is an example for register variable definition,

```
register int number;
```

Register variables are stored in CPU registers, and hence they can be accessed faster than the automatic variables, which are stored in memory. Hence, if a variable is used in many places in a program it is better to declare its storage class as register. The initial value by default in case of register variables is also a garbage value.

Program 2.15, illustrates the scope and life of register variables.

### Program 2.15

```
/* register.c */
#include<stdio.h>
void main()
{
register int x;
for(x = 1; x <= 10; x++)
printf("%d",x);
}
```

The program displays the following output

1 2 3 4 5 6 7 8 9 10

We cannot use register storage class for all types of variables. For example, register double x; register float y; register long z;

The above declarations are wrong because the CPU registers in the micro computers are usually 16 bit registers and therefore it cannot hold a float or a double value, which require 32 and 64 bytes respectively for storing a value. If the above declarations are used you won't get error messages, but the compiler would treat these variables as automatic variables.

### 2.11.3 Static Storage Class

The word static in general refers to anything that is inert to change. In a program if static variables are declared within individual blocks they are local to the block in which they are declared. The static variables retain their values throughout the life of the program. Hence, if a block is exited and then re-entered at a later time, the static variables declared in that block will retain their values (i.e., the static variable is not destroyed on exit from the block, instead its value is preserved, and becomes available again when the block is executed next time. Hence, the static variables are initialized only once, when the program begins its execution). When declaring a static variable inside a block, it is more precise in C to use the keyword static before the definition of the variable. The following statement is an example for static variable declaration, static int number;

Static variables are stored in the memory. When a static variable is not initialized, it takes a value of zero. The value of the variable persists between different function calls in the program. Program 2.16, illustrates the scope and life of the static variables.

### Program 2.16

```
/* static.c */
#include<stdio.h>
void sum();
/* Function prototype */
void main()
{
    sum();
    sum();
    sum();
    sum();
}
/* Function call */
void sum()
{
    static int x = 1;
    printf("%d ", x);
    x = x + 1;
}
```

The program displays the following output
1 2 3 4

We get the output as above because the value of the variable persists (does not change) between different function calls. If the variable is not defined as static then the output of the program will be

1 1 1 1

### 2.11.4 External Storage Class

Variables that are both alive and active throughout the entire program are called as external variables also referred as global variables. Global variables can be accessed by any function in the program. Global variables do not belong to any particular function (i.e., they are global in nature) and is usually declared outside all functions, usually at the beginning of the program, but after all preprocessor directives. Global variables can be referred by any function that follows the variable declaration in the program. Any function in the program can access the value of the global variable and can change the value of the variable if desired. When declaring an external variable or a global variable in a program, it is more precise in C to use the keyword extern before the declaration of the variable. The following statement is an example for external variable declaration.

```
extern int number;
```

Global variables are also stored in the memory. When an external variable is not initialized it takes a value of zero. The value of the variable persists between different function calls as long as the program execution ends.

Note that initialization of an extern variable takes place only once. (i.e., when the program starts up, before the control enters to the main() function). Program 2.17, illustrates the scope and life of the global variables.

### Program 2.17

```
/* extern.c */
#include<stdio.h>
void test1();
void test2();
void test3();
void main()
{
extern int value;
value = 100;
test1();
test2();
test3();
printf("%d ", value);
}
void test1()
{
extern int value;
value += 100;
printf("%d ", value);
}
void test2()
{
extern int value;
value = 1000;
printf("%d ", value);
}

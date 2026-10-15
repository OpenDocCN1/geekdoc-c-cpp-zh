# 25.- Variables and Pointers

In this class we will see, perhaps, the most advanced functionality of the C language, the pointers.

In C we can define variables of a particular type that store values that we can access in our program

Eg..
int number = 2;

In our program we can access the variable "number" through its name.

The variables is a representation of a memory space that has a physical address.

Eg.
When we define the variable number, the compiler assigns it in memory address 12000.

In our program instead of accessing the variable by the memory address, we access through its name and the compiler itself is in charge of mapping the name of the variable with its physical memory address.

A pointer is a special type of variable that allows you to store the physical address of another variable, so that we can access it through an indirection.

```
pej
int number = 2;
int *number;

number = &number;
*number = 3;
```

In this example number is a pointer that will point to an integer variable.
With the number assignment = &number, we are indicating that the pointer points to the variable number.
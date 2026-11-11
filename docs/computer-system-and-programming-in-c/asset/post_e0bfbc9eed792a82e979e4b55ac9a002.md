
- (c) Both a and b
- (d) None of the above

- 6. Pointer to structures holds
    - (a) Memory address to structure variable
    - (b) Memory address to structure
    - (c) Both a and b
    - (d) None of the above

- 7. In the function declaration you need to specify
    - (a) Type, names and arguments
    - (b) Type, address, argument,
    - (c) Both a and b
    - (d) None of the above

- 8. We can access a member of second structure
    - (a) struct_var1.struct_var2.data_member
    - (b) struct_var2.struct_var1.data_member
    - (c) Both a and b
    - (d) Cannot be done

- 9. Structures can be used for
    - (a) Hold the locations of points in multidimensional space
    - (b) Members of other structures
    - (c) Used to create link list
    - (d) All of the above

- 10. In unions
    - (a) One block of memory is used by each member
    - (b) Allocates memory equals to maximum memory of member
    - (c) Both a and b
    - (d) None of the above

### State True/False

- 1. A structure is a collection of variables of different types.
- 2. Variables in a structure can only be accessed by their address.
- 3. Size of struct is the sum of size of variables it holds.
- 4. sizeof() function returns the size smaller than actually it is.
- 5. The pointer to structure stores its memory address.
- 6. We cannot declare structures within a structure.
- 7. In union you can store one information at a time.
- 8. A structure cannot hold a field which is pointer to it.
- 9. In case of union fields share a same memory space.
- 10. We can have an inline declaration of union in a structure.

### Section B

*Short Answer Type Questions*

- 1. Define the concept of structure with proper explanation.
- 2. Define the concept of union with proper explanation.
- 3. Differentiate between structure and union with proper explanation.
- 4. Write a program in C to read and display the bio-data using structure.
- 5. Write a program in C to find area of circle using structure.
- 6. Write a program in C to find the biggest of three numbers using structure.
- 7. Write a program in C to find the smallest of three numbers using structure.
- 8. Write a program in C to read and display the bio-data using structure.
- 9. Write a program in C to read and display the bio-data with date of birth using structure.
- 10. Write a program in C to read and display the bio-data of 10 students using structure.

### Section C

*Long Answer Type Questions*

- 1. Write a program in C to read and display the numbers using typedef.
- 2. Write a program in C to read and display the bio-data using typedef.
- 3. Write a program in C to read and display the bio-data using typedef.
- 4. Write a program in C to read and display the complete bio-data using typedef.
- 5. Write a program in C to read and display the complex number.
- 6. Write a program in C to read and display the two complex number.
- 7. Write a program in C to read and display the sum of two complex numbers.
- 8. Write a program in C to read and display the difference of two complex numbers.
- 9. Differentiate between structure and union with suitable example.
- 10. Define the term union and why we use the concept of union explain in detail.

## 14 Pointer

If you want to be proficient in the writing of code in the C programming language, you must have a thorough working knowledge of how to use pointers. One of those things beginners in C find difficult is the concept of pointers. The purpose of this chapter is to provide an introduction to pointers and their efficient use in the C programming. Actually, the main difficulty lies with the C’s pointer terminology than the actual concept.

C uses pointers in three main ways. First, they are used to create *dynamic data structures*, data structures built up from blocks of memory allocated from the heap at run-time. Second, C uses pointers to handle *variable parameters* passed to functions. And third, pointers in C provide an alternative means of accessing information stored in arrays, which is especially valuable when you work with strings.

A normal variable is a location in memory that can hold a value. For example, when you declare a variable *i* as an integer, four bytes of memory is set aside for it. In your program, you refer to that location in memory by the name *i*. At the machine level, that location has a memory address, at which the four bytes can hold one integer value. A pointer is a variable that points to another variable. This means that it holds the memory address of another variable. Put another way, the pointer does not hold a value in the traditional sense; instead, it holds the address of another variable. It points to that other variable by holding its address. Because a pointer holds an address rather than a value, it has two parts. The pointer itself holds the address.

That address points to a value. There is the pointer and the value pointed to. As long as you are careful to ensure that the pointers in your programs always point to valid memory locations, pointers can be useful, powerful, and relatively trouble-free tools.

### CONCEPT BEHIND POINTER

Computer’s memory is made up of a sequential collection of storage cells called bytes. Each byte has a number called an address associated with it. When we declare a variable in our program, the compiler immediately assigns a specific block of memory to hold the value of that variable. Since every cell has a unique address, this block of memory will have a unique starting address. The size of this block depends on the range over which the variable is allowed to vary. For example, on 32 bit PC’s the size of an integer variable is 4 bytes. On older 16 bit PC’s integers were 2 bytes. In C the size of a variable type such as an integer need not be the same on all types of Machines. If you want to know the size of the various data types on your system, running the following code given in the example will give you the information.

### Example

Write a program to know the size of the various data types on your system.

### Solution

```c
#include <stdio.h>
#include<conio.h>
void main()
{
clrscr();
printf ("\n size of an int = %d bytes", sizeof (int));
printf ("\n size of a float = %d bytes", sizeof (float));
printf ("\n size of a char = %d bytes", sizeof (char));
getch();
}
```

The output of the above code segment is as follows

```
Size of int = 2 bytes
Size of float = 4 bytes
Size of char = 1 byte
```

### CHARACTERISTIC FEATURES OF POINTERS

The following are the features of pointers

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_245_0.png)

- With the use of pointers in programming, the program execution time will be faster as the data is manipulated with the help of addresses directly.
- With the use of pointers in programming, will save the memory space.
- With the use of pointers in programming, the memory access will be very efficient.
- With the use of pointers in programming, dynamic memory is allocated.

An ordinary variable is a location in memory that can hold a value. For example, when you declare a variable `num` as an integer, the compiler sets aside 2 bytes of memory (depends on the PC) to hold the value of the integer. In your program, you refer to that location in memory by the name `num`. At the machine level that location has a memory address.

`int num = 100;`

We can access the value 100 either by the name `num` or by its memory address. Since, addresses are simply digits, they can be stored in any other variable.

Such variables that hold addresses of other variables are called Pointers.

The general syntax of defining a pointer is as follows:

`<datatype> * <pointername>;`

In other words, a pointer is simply a variable that contains an address, which is a location of another variable in memory. A pointer variable “points to” another variable by holding its address. Since a pointer holds an address rather than a value, it has two parts. The pointer itself holds the address. That address points to a value. There is a pointer and the value pointed to. This fact can be a little confusing until you get comfortable with it, but once you get familiar with it, then it is extremely easy and very powerful.

One good way to visualize this concept is to examine in the following figure.

### THE ADDRESS AND INDIRECTION OPERATORS

Now we will consider how to determine the address of a variable. The operator that is available in C for this purpose is “&” (address of) operator. The operator & and the immediately preceding variable returns the address of the variable associated with it. C’s other unary pointer operator is the “*”, also called as value at address or indirection operator. It returns a value stored at that address.

This can be illustrated with the help of following examples.

### Example

Write a program to print the address associated with a variable and value stored at that address.

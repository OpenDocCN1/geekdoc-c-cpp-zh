
## C Pointers
### Objectives

In this chapter, you'll:

- Use pointers and pointer operators.
- Pass arguments to functions by reference using pointers.
- Understand the various placements of the const qualifier and how they affect what you can do with a variable.
- Use the sizeof operator with variables and types.
- Use pointer arithmetic to process the elements in arrays.
- Understand the close relationships among pointers, arrays and strings.
- Define and use arrays of strings.
- Use pointers to functions.
- Learn about secure C programming issues with regard to pointers.

- 7.1 Introduction
- 7.2 Pointer Variable Definitions and Initialization
- 7.3 Pointer Operators
- 7.4 Passing Arguments to Functions by Reference
- 7.5 Using the const Qualifier with Pointers
- 7.5.1 Converting a String to Uppercase Using a Non-Constant Pointer to Non-Constant Data
- 7.5.2 Printing a String One Character at a Time Using a Non-Constant Pointer to Constant Data
- 7.5.3 Attempting to Modify a Constant Pointer to Non-Constant Data
- 7.5.4 Attempting to Modify a Constant Pointer to Constant Data
- 7.6 Bubble Sort Using Pass-by-Reference
- 7.7 sizeof Operator
- 7.8 Pointer Expressions and Pointer Arithmetic
- 7.8.1 Allowed Operators for Pointer Arithmetic
- 7.8.2 Aiming a Pointer at an Array
- 7.8.3 Adding an Integer to a Pointer
- 7.8.4 Subtracting an Integer from a Pointer
- 7.8.5 Incrementing and Decrementing a Pointer
- 7.8.6 Subtracting One Pointer from Another
- 7.8.7 Assigning Pointers to One Another
- 7.8.8 Pointer to void
- 7.8.9 Comparing Pointers
- 7.9 Relationship between Pointers and Arrays
- 7.9.1 Pointer/Offset Notation
- 7.9.2 Pointer/Index Notation
- 7.9.3 Cannot Modify an Array Name with Pointer Arithmetic
- 7.9.4 Demonstrating Pointer Indexing and Offsets
- 7.9.5 String Copying with Arrays and Pointers
- 7.10 Arrays of Pointers
- 7.11 Case Study: Card Shuffling and Dealing Simulation
- 7.12 Pointers to Functions
- 7.12.1 Sorting in Ascending or Descending Order
- 7.12.2 Using Function Pointers to Create a Menu-Driven System
- 7.13 Secure C Programming
- Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises
- Special Section: Building Your Own Computer | Array of Function Pointer Exercises | Making a Difference

## 7.1 Introduction

In this chapter, we discuss one of the most powerful features of the C programming language, the pointer.¹ Pointers are among C's most difficult capabilities to master. Pointers enable programs to accomplish pass-by-reference, to pass functions between functions, and to create and manipulate dynamic data structures—ones that can grow and shrink at execution time, such as linked lists, queues, stacks and trees. This chapter explains basic pointer concepts. In Section 7.13, we discuss various pointer-related security issues. Chapter 10 examines the use of pointers with structures. Chapter 12 introduces dynamic memory management techniques and presents examples of creating and using dynamic data structures.

1. Pointers and pointer-based entities such as arrays and strings, when misused intentionally or accidentally, can lead to errors and security breaches. See our Secure C Programming Resource Center (www.deitel.com/SecureC/) for articles, books, white papers and forums on this important topic.

## 7.2 Pointer Variable Definitions and Initialization

Pointers are variables whose values are memory addresses. Normally, a variable directly contains a specific value. A pointer, however, contains an address of a variable that contains a specific value. In this sense, a variable name directly references a value, and a pointer indirectly references a value (Fig. 7.1). Referencing a value through a pointer is called indirection.

![](img/bf54db922e6fa8319cba11069e785521_302_0.png)

Fig. 7.1 | Directly and indirectly referencing a variable.

### Declaring Pointers

Pointers, like all variables, must be defined before they can be used. The definition

```
int *countPtr, count;
```

specifies that variable countPtr is of type int * (i.e., a pointer to an integer) and is read (right to left), "countPtr is a pointer to int" or "countPtr points to an object of type int." Also, the variable count is defined to be an int, not a pointer to an int. The * applies only to countPtr in the definition. When * is used in this manner in a definition, it indicates that the variable being defined is a pointer. Pointers can be defined to point to objects of any type. To prevent the ambiguity of declaring pointer and non-pointer variables in the same declaration as shown above, you should always declare only one variable per declaration.

Common Programming Error 7.1
The asterisk (*) notation used to declare pointer variables does not distribute to all variable names in a declaration. Each pointer must be declared with the * prefixed to the name; e.g., if you wish to declare xPtr and yPtr as int pointers, use int *xPtr, *yPtr;

Good Programming Practice 7.1
We prefer to include the letters Ptr in pointer variable names to make it clear that these variables are pointers and need to be handled appropriately.

### Initializing and Assigning Values to Pointers

Pointers should be initialized when they're defined, or they can be assigned a value. A pointer may be initialized to NULL, 0 or an address. A pointer with the value NULL points to nothing. NULL is a symbolic constant defined in the <stddef.h> header (and several other headers, such as <stdio.h>). Initializing a pointer to 0 is equivalent to initializing a pointer to NULL, but NULL is preferred, because it highlights the fact that the variable is of a pointer type. When 0 is assigned, it's first converted to a pointer of the appropriate type. The value 0 is the only integer value that can be assigned directly to a pointer variable. Assigning a variable's address to a pointer is discussed in Section 7.3.

2. In C, an "object" is a region of memory that can hold a value. So objects in C include primitive types such as ints, floats, chars and doubles, as well as aggregate types such as arrays and structs (which we discuss in Chapter 10).

### Error-Prevention Tip 7.1

Initialize pointers to prevent unexpected results.

## 7.3 Pointer Operators

In this section, we present the address (&) and indirection (*) operators, and the relationship between them.

### The Address (&) Operator

The &, or address operator, is a unary operator that returns the address of its operand. For example, assuming the definitions

```
int y = 5;
int *yPtr;
```

the statement

```
yPtr = &y;
```

assigns the address of the variable y to pointer variable yPtr. Variable yPtr is then said to "point to" y. Figure 7.2 shows a schematic representation of memory after the preceding assignment is executed.

![](img/bf54db922e6fa8319cba11069e785521_303_0.png)

### Pointer Representation in Memory

Figure 7.3 shows the representation of the preceding pointer in memory, assuming that integer variable y is stored at location 600000, and pointer variable yPtr is stored at location 500000. The operand of the address operator must be a variable; the address operator cannot be applied to constants or expressions.

![](img/bf54db922e6fa8319cba11069e785521_303_1.png)

### The Indirection (*) Operator

The unary * operator, commonly referred to as the indirection operator or dereferencing operator, returns the value of the object to which its operand (i.e., a pointer) points. For example, the statement

printf( "%d", *yPtr );

prints the value of variable y (5). Using * in this manner is called dereferencing a pointer.

Common Programming Error 7.2

Dereferencing a pointer that has not been properly initialized or that has not been assigned to point to a specific location in memory is an error. This could cause a fatal execution-time error, or it could accidentally modify important data and allow the program to run to completion with incorrect results.

### Demonstrating the & and * Operators

Figure 7.4 demonstrates the pointer operators & and *. The printf conversion specifier %p outputs the memory location as a hexadecimal integer on most platforms. (See Appendix C for more information on hexadecimal integers.) In the program's output, notice that the address of a and the value of aPtr are identical in the output, thus confirming that the address of a is indeed assigned to the pointer variable aPtr (line 8). The & and * operators are complements of one another—when they're both applied consecutively to aPtr in either order (line 18), the same result is printed. The addresses shown in the output will vary across systems. Figure 7.5 lists the precedence and associativity of the operators introduced to this point.

```
1 // Fig. 7.4: fig07_04.c
2 // Using the & and * pointer operators.
3 #include <stdio.h>
4
5 int main(void)
6 {
7    int a = 7;
8    int *aPtr = &a; // set aPtr to the address of a
9
10   printf("The address of a is %p\n"
11          "The value of aPtr is %p\n", &a, aPtr);
12
13   printf("\nThe value of a is %d\n"
14          "The value of *aPtr is %d\n", a, *aPtr);
15
16   printf("\n\nShowing that & and * are complements of "
17          "each other\n*aPtr = %p\n"
18          "\n&*aPtr = %p\n", *&aPtr, &*aPtr);
19 }
```

```
The address of a is 0028FEC0
The value of aPtr is 0028FEC0

The value of a is 7
The value of *aPtr is 7

Showing that & and * are complements of each other
&*aPtr = 0028FEC0
*&aPtr = 0028FEC0
```

Fig. 7.4 | Using the & and * pointer operators.

# 12 Pointers Revisited

# OBJECTIVES

+   - Understanding Pointer Variables
- Describe Chain of Pointers
- Describe Pointer Expressions
- Describe Operations on Pointers
- Describe Pointers and Arrays
- Implement Pointers and Functions
- Implement Pointers and Structures

So far, we have discussed about programs that use identifiers to access memory locations. In other words, we have assigned identifiers to data that we like to store in the memory. The identifiers are used to access or manipulate the contents stored at different memory locations. For example, to store a value 40, an identifier named i_num of integer data type can be declared. This identifier thus gets associated with three entities, that is, a name, a value, and an address, in the memory. To access the value stored in the memory, the name i_num will be used. The variable i_num can identify the location of the memory address and fetch value from there. C language provides the facility to access the address of memory location directly, thereby saving time to map identifier name with its address in memory. C language provides a feature called pointers that allow a programmer to store address of identifiers used in the program. We have discussed about basics of pointers in Chapter 3. There are many usages of pointers in C. In Chapter 8, we have learned that the pointers can be used in functions when using pass-by-address mechanism of parameter passing. Further, in Chapter 9 and 10, we have learned that pointers provide efficient mechanism for manipulating data in arrays. In this chapter, we will revise the concept of pointers and discuss about operations, such as addition, subtraction, comparison, that can be performed on pointers. We will also discuss how to use pointers with arrays, functions, and structures.

# 12.1 Understanding Pointer Variables

We know that a pointer is a variable that can store address of an identifier. Similar to primitive data type variables, such as integer, float, and others, pointer is also associated with a name, a value, and an address in memory. The difference between a variable of primitive data type and a pointer variable is the value stored in them. The value stored in variables of primitive data types can be an integer, float, double, or character, but the value stored in the pointer variable will always be of type unsigned integer that refers to a memory address of other variable.. Pointers are frequently used in C language. Thus, it
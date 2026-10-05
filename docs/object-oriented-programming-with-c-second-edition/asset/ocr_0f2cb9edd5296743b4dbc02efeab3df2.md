# # Dynamic Memory Management

This chapter explains the tools that are available in C++ for dynamic memory management. It begins with a brief explanation of static memory management and its limitation. This is followed by an elucidation of the mechanism of dynamic memory management.
The middle part of the chapter details with the use and usage of the new operator and delete operator. Methods for allocating and deallocating memory for single objects and array of objects are explained.
The chapter also explains how the size of a dynamically allocated memory block is.
The last part of the chapter explains the use of the set_new_handler() function for specifying our new handler.

# 3.1 Introduction

Let us have an overview of static memory management. Memory for program variables allocated and deallocated during run time only. For example, we write

```
int x;
```

in function in the source code. When the source code containing this statement (apart the other statements) is compiled and linked, an executable file is generated. Besides containing equivalent instructions for the other statements, the executable file also contains the equivalent instructions for this statement. When the executable file is executed, all the instructions contained inside it, including the ones to allocate memory for 'x', are executed. Thus, memory gets allocated for 'x' during run time. This is known as static memory allocation (although memory gets allocated during run time only).

The compiler writes instructions in the executable to deallocate the memory previously allocated for 'x' when it encounters the end of the function, in which 'x' was declared, in the source code. When the executable file is executed, all instructions contained inside it including the ones to deallocate memory for 'x' are executed. Thus, for 'x' gets deallocated during run time. This is known as static memory deallocation (although memory gets deallocated during run time only).

Static allocation and deallocation of memory has a limitation. It is rigid. The programmers are forced to predict the total amount of data program will utilize. They write statements to declare pre-calculated amounts of memory. During run time, if more memory is required, static memory allocation cannot fulfill the need. A certain memory block is no longer of
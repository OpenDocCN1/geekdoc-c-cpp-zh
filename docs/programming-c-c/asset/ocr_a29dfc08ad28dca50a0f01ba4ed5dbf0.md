Well, it is a well-established fact that pointers are one of the strongest features of the C programming language. But, pointers can prove to be quite risky. Using as wild pointers (uninitialized pointers) may cause your program to behave badly, or worse, crash. There are a couple of programming languages like Python and Java which do not involve the use of pointers.

# Here are some of the reasons why we use pointers in C and C++:

+   1. We can easily access the memory location of any variable directly and manipulate it according to our convenience.
2. It facilitates the use of dynamic memory allocation, making it a much faster access compared to programming languages that do not support the use of pointers like Python and Java.
3. We prefer pointers in certain situations to improve the efficiency of certain procedures.

# Features of Pointers

+   1. Pointers save memory space.
2. Execution time with pointers is faster because data are manipulated with the address, i.e., direct access to memory location.
3. Memory is accessed efficiently with the pointers. The pointer assigns and releases the memory as well. Hence, it can be said the memory of pointers is dynamically allocated.
4. Pointers are used to create complex data structures. They are useful for representing two-dimensional and multi-dimensional arrays.
5. An array of any type can be accessed with the help of pointers, without considering its subscript range.
6. Pointers are used for file handling.
7. Pointers are used to allocate memory dynamically. Without pointers, dynamic memory allocations are impossible.
8. In C++, a pointer declared to a base class could access the object of a derived class. However, a pointer to a derived class cannot access the object of a base class.

# Disadvantage of Pointers

+   1. Pointers are unsafe because it is easy for a pointer to get you wrong.
2. Uninitialized pointers will cause segmentation fault.
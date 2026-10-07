# Team LiB

# Summary

A pointer is a variable or constant whose value is the address of another variable or constant. Other C++ tasks are performed more easily with pointers, while other C++ tasks, such as dynamic memory allocation, cannot be performed without pointers.

Like any variable or constant, you must declare a pointer before you can work with it. The only difference between declaring a pointer and a variable or constant which stores a value instead of an address is that the pointer declaration includes an asterisk as the data type and name. However, the data type in the declaration of a pointer is not the data type of its value, as is the case with a variable or constant which stores a value instead of an address. The actual data type of all pointers, whether integer, float, character, or otherwise, is the same: a hexadecimal value represents a memory address. The data type in the declaration of a pointer refers to the data type of another variable (or constant) whose address is the value of the pointer. In other words, the value of an integer pointer must be the address of an integer variable or constant, the value of a float pointer must be the address of a float variable or constant, and so forth.

You should explicitly assign a pointer value before you use it; otherwise, you risk a runtime error or worse. When you are ready to assign a pointer to the address of another variable or constant, it is too early in your code to know which address to assign to the pointer, unless you first assign pointer NULL, which is a constant defined in standard libraries, including iostream. The value of NULL, the memory address 0, signals that the pointer is not intended to point to an accessible memory location.

The indirection operator is used on a pointer to obtain the value of the variable or constant to which the pointer points. This operation is said to dereference the pointer.

A pointer may be a variable or a constant. The name of an array is a constant pointer, pointing to the base address of the array. A pointer variable, being a variable, may point to different variables or constants at different times in the program.

A pointer variable may be incremented. Incrementing a pointer is common when looping through consecutive indices of an array. Incrementing a pointer variable does not necessarily increase its value by 1. Instead, incrementing a pointer increases its value by the number of bytes of its data type.

Pointers may be passed by reference arguments. This is commonly used to note that an argument is a pointer. The difference in syntax between passing by reference and passing by address is that, in the function prototype, you use an ampersand (&) for passing by reference, but an asterisk (*) for passing by reference. Additionally, if the pointer argument is the name of a single variable passed to an array, there are two further differences in syntax between passing by reference and passing by address. When you call the function, you don't need to use the address operator (&) for passing by reference, but you do for passing by address. In the body of the called function, you don't need to dereference the argument when you pass it by reference, but when you pass it by address.

You can use a size declared for an array if you use dynamic memory allocation because memory is allocated at runtime from a different place—the heap—where memory is allocated for variables declared at time on the stack. You need to use a pointer with the new operator to dynamically allocate memory, and
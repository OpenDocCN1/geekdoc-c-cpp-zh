The important differences between the memory models are in the size of the data and code pointers, number of data and code segments, and the number and types of heaps available.

In all the 16-bit memory models, the compiler puts all static and global variables into a single data segment (called DGROUP) that can contain only 64KB. With far data, a particular data structure can be put into a data segment of its own. However, that data structure cannot be larger than 64KB. The major determinant of memory availability is the size of the pointers used to access memory locations.

If the pointer is declared globally, the value of its address will be 0000 in the case of a near pointer and 0000:0000 in the case of a far pointer. If the pointer is declared inside a function definition as an auto variable (default), then it is created on the stack and will have a default address of whatever value happened to be at that location on the stack when it was created. In either case, these default memory addresses are invalid. This is referred to as an uninitialized pointer and should never be dereferenced.

There are three types of pointers. They are near, far, and huge.

In Turbo C; almost all pointers are declared as near (16 bits per pointer by default) or far (32 bits per pointer). While near pointers simplify memory access in the segmented memory of Intel processors by allowing direct arithmetic on pointers, they limit accessible memory to 64 kilobytes (2^16). Far pointers can be used to access multiple code segments, each 64K, up to 1 megabyte (2^20), by using segment and offset addressing. The disadvantage is that the programmer cannot use the simple pointer arithmetic that is possible with near pointers.

The default model is small, which is effective for the majority of applications. The tiny model is specifically designed for the production of TSR (Terminate and Stay Resident) programs, which must fit into one code segment and be compiled as .com rather than .exe files. The remaining models are selectable in the compilation process through the IDE or in the make file.

GNU C does not have memory models because in this compiler all addresses are 32 bits wide. This is advantageous for the user, since it does not have the 64K limit. For DOS or Win16 compilers, a memory model must be selected.

+   **Note**
+   - The mechanism of using variable-length arguments with functions is error-prone because it defeats type checking.
+   - There are six types of memory models: tiny, small, medium, compact, large, and huge.
+   - The important differences between the memory models are in the size of the data and code pointers, number of data and code segments, and the number and types of heaps available.
+   - There are three types of pointers: near, far, and huge, which use different memory models and functions for memory allocation.

# # SUMMARY

There are several features in C that can be classified as advanced features. Among these are the bitwise operators. There are six bitwise operators, namely AND (&), OR (|), complement (~), XOR (^), left-shift (<<), and right-shift (>>). These operators act on the contents of bits individually when applied on bytes or words.

The function main() can be defined with formal parameters so that the program may accept command-line arguments. This means that arguments are specified to main() when the program is executed.

The C preprocessor is a program that processes any source program in C before compilation. Since it allows the user to define macros, the C preprocessor is also called a macro processor. The preprocessor provides its own instructions, called directives. There are several directives that are used to invoke it. A directive usually occupies a single line. The preprocessor also furnishes a small set of predefined identifiers that denote useful information.

There are two or three data type qualifiers—const, volatile, and/or restrict—that have been introduced in C. The concepts of const and volatile are completely independent. A common misconception is to imagine that const is the opposite of volatile and vice versa.

The C89 standards committee added two type qualifiers to C, const and volatile and the C99 committee added a third type qualifier with restrict.

const means something that is not modifiable. The const type qualifier is used to qualify an object whose value cannot be changed. Objects qualified by the const keyword cannot be modified. On the other hand, a volatile value is one that might change unexpectedly. This situation generally occurs while accessing special hardware registers, usually when writing device drivers. The compiler should not assume that a volatile-qualified variable contains the last value that was written to it, or that reading it again would yield the same result that reading it the previous time did. An object qualified by the volatile keyword can be modified or accessed by other processes or hardware, and is especially vulnerable to side effects.

The restrict qualifier is an invention of the C99 committee. The object accessed through the restrict-qualified pointer has a special relation with that pointer. Only pointer types can be restrict-qualified. A restrict-qualified pointer that is a function parameter is the sole means of access to an object.
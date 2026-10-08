# List of Common Header Files and Their Library Functions

| Header File | Library Function | Return Type | Description |
| --- | --- | --- | --- |
| stdio.h | scanf(...) | int | Reads data items from the standard input device. |
| stdlib.h | abs(int) | int | Returns the absolute value of int. |
| stdlib.h | atof(str) | double | Converts the string str to a double precision quantity. |
| stdlib.h | atoi(str) | int | Converts the string str to an integer equivalent. |
| stdlib.h | atol(str) | long | Converts the string str to a long integer equivalent. |
| stdlib.h | calloc(uint 1, uint 2) | void* | Allocates memory for an array having uint 1 elements, each of length uint2 bytes. It returns a pointer to the beginning of the allocated space. |
| stdlib.h | exit(uint) | void | Closes all files and buffers, and terminates the program (value of uint is assigned by the function to indicate termination status). |
| stdlib.h | free(ptr) | void | Frees an allocated memory block whose beginning is indicated by the pointer ptr. |
| stdlib.h | malloc(uint) | void* | Allocates uint bytes of memory. It returns a pointer to the beginning of the allocated space. |
| stdlib.h | rand(void) | int | Returns a random positive integer. |
| stdlib.h | realloc(ptr, uint) | void* | Reallocates uint bytes of memory to the pointer variable ptr. It returns a pointer to the beginning of the memory space. |
| stdlib.h | srand(uint) | void | Initializes the random number generator. |
| stdlib.h | system(str) | int | Passes command string str to the operating system. O if the command is successfully executed; otherwise, returns a nonzero value. |
| string.h | strcmp(str1, str2) | int | Compares two strings lexicographically. It returns O if str1 and str2 are identical; a negative value if str1 < str2 and a positive value if str1 > str2. |
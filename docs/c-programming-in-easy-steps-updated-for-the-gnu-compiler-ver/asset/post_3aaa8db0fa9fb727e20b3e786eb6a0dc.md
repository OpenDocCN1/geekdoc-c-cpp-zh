
## Allocating memory

The standard C stdlib.h library header file provides memory management functions, with which a program can explicitly request memory be made available as the program executes. The malloc() function requires a single integer argument to specify how many bytes of memory to allocate, whereas the calloc() function requires two integer arguments that get multiplied together to specify how many bytes of memory to allocate. Both of these functions return a pointer to the beginning of the memory block when successful, or a NULL value upon failure.

Memory previously allocated with malloc() or calloc() can be increased with the realloc() function. This requires the pointer to the allocated memory block as its first argument, and an integer specifying the new block size as its second argument. It returns a pointer to the beginning of the enlarged memory block when successful, or a NULL value upon failure.

All memory allocated with these functions should be released when no longer required by specifying the memory block pointer as the argument to the free() function.

There is no standard C function to determine the size of a dynamically allocated memory block but this can be discovered with platform-specific functions. On Windows there is _msize() and on Linux there is malloc_usable_size(). Both these functions require the memory block pointer as their argument.

![](img/d1dfb0563339ba187decb78799155b7f_137_0.png)

The calloc() function clears all allocated memory space to zero, but malloc() leaves whatever values are already there.

![](img/d1dfb0563339ba187decb78799155b7f_137_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_137_2.png)

On Linux systems, replace the _msize prototype declaration and function calls with the alternative malloc_usable_size.

- 1. Begin a new program with preprocessor instructions to include the standard library input/output functions and memory management functions
- 2. Declare a Windows-specific function prototype
- 3. Add a main function that declares an integer variable and an integer pointer variable

```
#include <stdio.h>
#include <stdlib.h>
```

```
int _msize( int *bytes );
```

```
int main()
{
    int size, *mem;
}
```

- 4. Request memory to accommodate 100 integers
mem = malloc( 100 * sizeof( int ) );

![](img/d1dfb0563339ba187decb78799155b7f_138_0.png)

Even though an int typically occupies 4 bytes it is good practice to use the sizeof() operator to specify the size in case of variation.

- 5. Next, output details of the allocated memory block or an advisory message if the request fails
if( mem != NULL )
{
size = _msize( mem );
printf( "\nSize of block for 100 ints: %d bytes\n", size );
printf( "Beginning at %p\n", mem );
}
else { printf( "!!! Insufficient memory\n"); return 1; }

![](img/d1dfb0563339ba187decb78799155b7f_138_1.png)

The implementation of the realloc() function can vary on different platforms.

- 6. Now, attempt to enlarge the allocated memory block and output its details or an advisory message if the request fails
mem = realloc( mem , size + ( 100 * sizeof( int ) ) );
if( mem != NULL )
{
size = _msize( mem );
printf( "\nSize of block for 200 ints: %d bytes\n", size );
printf( "Beginning at %p\n", mem );
}
else { printf( "!!! Insufficient memory\n"); return 1; }

- 7. At the end of the main function block, remember to release the allocated memory, then return the required zero integer value
free( mem );
return 0 ;

- 8. Save the program file, then compile and execute the program to see the allocated memory blocks when the requests are successful

![](img/d1dfb0563339ba187decb78799155b7f_138_2.png)

![](img/d1dfb0563339ba187decb78799155b7f_138_3.png)

The memory request statement could alternatively have used calloc( 100 , sizeof(int) ).

## Summary

- A struct can contain one or more variables of any data type, which are known as struct members.
- Each struct member can be referenced by appending its name to a tag name with the `.` dot operator.
- Further instances of a struct will inherit the member properties of the original from which they are derived.
- The struct keyword may be preceded by the typedef keyword to declare the struct to be a data type.
- It is helpful to capitalize tag names to readily identify structure-defined data types.
- Variable declarations may optionally initialize each struct member by assigning a comma-separated list of values.
- A pointer to a struct holds the memory address of the beginning of the region of memory used to store member data.
- In a struct pointer, the `.` dot operator can be replaced by the `->` arrow operator.
- The members in an array of structures may, optionally, be initialized in the declaration – but each list of member values must be enclosed within a pair of braces.
- A struct may be passed as an argument to a function, just like any other variable.
- Passing a struct variable to a function means it will operate on a copy of the struct members, but passing a struct pointer variable means the function operates on the original members.
- A union is like a struct in which different pieces of data are stored at the same memory location as the program proceeds.
- The standard C library `stdlib.h` header file provides the `malloc()`, `calloc()` and `realloc()` functions, which can allocate memory, and the `free()` function to release allocated memory.

## 10 Producing Results

This chapter demonstrates how C programs can utilize files, system time, random numbers, and a simple Windows dialog box.

- 140 Creating a file
- 142 Reading & writing characters
- 144 Reading & writing lines
- 146 Reading & writing entire files
- 148 Scanning filestreams
- 150 Reporting errors
- 152 Getting the date and time
- 154 Running a timer
- 156 Generating random numbers
- 158 Displaying a dialog box
- 160 Summary

### Creating a file

A special data type for handling files is defined in the stdio.h header file. It is called a "file pointer" and has the syntax FILE *fp. File pointers are used to open, read, write, and close files. In a C program, a file pointer called "file_ptr" can be created with the declaration FILE *file_ptr ;

A file pointer points to a structure defined in the stdio.h header file that contains information about the file. This includes details about the current character and if the file is being read or written.

Before a file can be read or written it firstly must always be opened with the fopen() function. This takes two arguments to specify the name and location of the file, and a "mode" in which to open the file. The fopen() function returns a file pointer if successful, or a NULL value upon failure.

Once a file has been successfully opened it can be read or added to, or new text can be written in the file, depending on the mode specified in the call to the fopen() function. Following this, the open file must then always be closed by calling the fclose() function and specifying the file pointer as its single argument.

The table below lists all the possible file modes that can be specified as the second argument to the fopen() function:

All the standard functions for file input/output are contained in the stdio.h header file.

For convenience, all the text files in the examples in this chapter are located in the MyPrograms folder that also contains the C source code files. On Windows the directory is C:\MyPrograms, and on Linux systems it's at /home/MyPrograms.

| File mode | Operation |
|---|---|
| r | Open an existing file to read |
| w | Open an existing file to write. Creates a new file if none exists, or opens an existing file and discards all its previous contents |
| a | Appends text. Opens or creates a text file for writing at the end of the file |
| r+ | Opens a text file to read from or write to |
| w+ | Opens a text file to write to or read from |
| a+ | Opens or creates a text file to read from or write to at the end of the file |

Note: Where the mode includes a b after any of the file modes listed above, the operation relates to a binary file rather than a text file – for example, rb or w+b

![](img/d1dfb0563339ba187decb78799155b7f_141_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_141_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_141_2.png)

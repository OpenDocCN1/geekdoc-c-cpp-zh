
```c
struct Distinct sdata = { 10, 'C', "Program" };
```

5. Now, in the main function block, declare a variable of the union data type `Unified`:

   ```c
   union Unified udata;
   ```

   ![](img/db19f3858a1e321646bf2590afd29547_194_0.png)

   It is the programmer's responsibility to understand which type of data is being stored in a union at any point in the execution of a program.

6. After the variable declarations, output the value and memory address of each struct member:

   ```c
   printf("\nStructure:\nNumber: %d", sdata.num );
   printf("\tStored at: %p\n", &sdata.num );
   printf("Letter: %c", sdata.ltr );
   printf("\tStored at: %p\n", &sdata.ltr );
   printf("String: %s", sdata.str );
   printf("\tStored at: %p\n", &sdata.str );
   ```

7. Now, assign a value to the first union member then output its value and memory address:

   ```c
   udata.num = 16 ;
   printf("\nUnion:\nNumber: %d", udata.num );
   printf("\tStored at: %p\n", &udata.num );
   ```

8. Next, assign a value to the second union member then output its value and memory address:

   ```c
   udata.ltr = 'A' ;
   printf("Letter: %c", udata.ltr );
   printf("\tStored at: %p\n", &udata.ltr );
   ```

9. Finally, assign a value to the third union member then output its value and memory address:

   ```c
   udata.str = "Union" ;
   printf("String: %s", udata.str );
   printf("\tStored at: %p\n", &udata.str );
   ```

10. At the end of the main function block, return a zero integer value, as required by the function declaration:

    ```c
    return 0 ;
    ```

11. Save the program file, then compile and execute the program to see the values stored in the structure and union members and the addresses where they are stored:

    ```
    C:\MyPrograms>gcc union.c -o union.exe
    C:\MyPrograms>union.exe

    Structure:
    Number: 10 Stored at: 0061FF24
    Letter: C Stored at: 0061FF28
    String: Program Stored at: 0061FF2C

    Union:
    Number: 16 Stored at: 0061FF20
    Letter: A Stored at: 0061FF20
    String: Union Stored at: 0061FF20
    ```

**Hot tip:** Unions are mostly useful when memory is very limited.

## Allocating memory

The standard C `stdlib.h` library header file provides memory management functions, with which a program can explicitly request memory be made available as the program executes. The `malloc()` function requires a single integer argument to specify how many bytes of memory to allocate, whereas the `calloc()` function requires two integer arguments that get multiplied together to specify how many bytes of memory to allocate. Both of these functions return a pointer to the beginning of the memory block when successful, or a `NULL` value upon failure.

![](img/db19f3858a1e321646bf2590afd29547_196_0.png)

The `calloc()` function clears all allocated memory space to zero, but `malloc()` leaves whatever values are already there.

Memory previously allocated with `malloc()` or `calloc()` can be increased with the `realloc()` function. This requires the pointer to the allocated memory block as its first argument, and an integer specifying the new block size as its second argument. It returns a pointer to the beginning of the enlarged memory block when successful, or a `NULL` value upon failure.

All memory allocated with these functions should be released when no longer required by specifying the memory block pointer as the argument to the `free()` function.

There is no standard C function to determine the size of a dynamically allocated memory block but this can be discovered with platform-specific functions. On Windows there is `_msize()` and on Linux there is `malloc_usable_size()`. Both these functions require the memory block pointer as their argument.

1. Begin a new program with preprocessor instructions to include the standard library input/output functions and memory management functions.

## memory.c

![](img/db19f3858a1e321646bf2590afd29547_197_0.png)

### Declare a Windows-specific function prototype

```c
int _msize(int *bytes );
```

### Add a main function that declares an integer variable and an integer pointer variable

```c
int main()
{
	int size ,*mem ;
}
```

![](img/db19f3858a1e321646bf2590afd29547_197_1.png)

On Linux systems, replace the `_msize` prototype declaration and function calls with the alternative `malloc_usable_size`.

### Request memory to accommodate 100 integers

```c
mem = malloc(100 * sizeof(int) );
```

### Next, output details of the allocated memory block or an advisory message if the request fails

```c
if (mem != NULL)
{
	size = _msize( mem );
	printf("Size of block for 100 ints: %d bytes\n", size );
	printf("Beginning at %p\n", mem );
}
else { printf("!!! Insufficient memory\n"); return 1; }
```

### Now, attempt to enlarge the allocated memory block and output its details or an advisory message if the request fails

```c
if (mem = realloc( mem , size + (100 * sizeof(int) )))
{
	// output details or advisory message
	size = _msize( mem );
	printf( "\nSize of block for 200 ints: %d bytes\n", size );
	printf( "Beginning at %p\n", mem );
}
else { printf( "!!! Insufficient memory\n" ); return 1; }
```

7. At the end of the main function block, remember to release the allocated memory, then return the required zero integer value:

   ```c
   free( mem );
   return 0 ;
   ```

8. Save the program file, then compile and execute the program to see the allocated memory blocks when the requests are successful.

![](img/db19f3858a1e321646bf2590afd29547_198_0.png)

![](img/db19f3858a1e321646bf2590afd29547_198_1.png)

Even though an int typically occupies 4 bytes it is good practice to use the `sizeof()` operator to specify the size in case of variation.

![](img/db19f3858a1e321646bf2590afd29547_198_2.png)

The implementation of the `realloc()` function can vary on different platforms.

![](img/db19f3858a1e321646bf2590afd29547_199_0.png)

The memory request statement could alternatively have used `calloc(100, sizeof(int))`.

## Summary

- A **struct** can contain one or more variables of any data type, which are known as **struct** members.
- Each **struct** member can be referenced by appending its name to a tag name with the . dot operator.
- Further instances of a **struct** will inherit the member properties of the original from which they are derived.
- The **struct** keyword may be preceded by the **typedef** keyword to declare the struct to be a data type.
- It is helpful to capitalize tag names to readily identify structure-defined data types.
- Variable declarations may optionally initialize each **struct** member by assigning a comma-separated list of values.
- A pointer to a **struct** holds the memory address of the beginning of the region of memory used to store member data.
- In a struct pointer, the . dot operator can be replaced by the -> arrow operator.
- The members in an array of structures may, optionally, be initialized in the declaration – but each list of member values must be enclosed within a pair of braces.
- A **struct** may be passed as an argument to a function, just like any other variable.
- Passing a **struct** variable to a function means it will operate on a copy of the **struct** members, but passing a **struct** pointer variable means the function operates on the original members.
- A **union** is like a **struct** in which different pieces of data are stored at the same memory location as the program proceeds.
- The standard C library **stdlib.h** header file provides the **malloc()**, **calloc()** and **realloc()** functions, which can allocate memory, and the **free()** function to release allocated memory.

## 10 Producing Results

*This chapter demonstrates how C programs can utilize files, system time, random numbers, and a simple Windows dialog box.*

- Creating a file
- Reading & writing characters
- Reading & writing lines
- Reading & writing entire files
- Scanning filestreams
- Reporting errors
- Getting the date and time
- Running a timer
- Generating random numbers
- Displaying a dialog box
- Summary

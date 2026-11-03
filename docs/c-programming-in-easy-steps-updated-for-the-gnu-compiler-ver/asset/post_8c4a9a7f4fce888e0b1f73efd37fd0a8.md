
- 6. After the main function block, define the two custom functions declared by the prototypes that each receive an integer pointer as an argument when called

```c
void twice( int *number )
{
  *number = ( *number * 2 );
}

void thrice( int *number )
{
  *number = ( *number * 3 );
}
```

> > **Don't forget!**
> >
> > The * character in the definition parentheses denotes that the argument is a pointer, whereas in the statement it dereferences the argument when it appears before the argument name, and represents the multiplication operator in the arithmetic statement.

- 7. Back in the main function block, add calls to each custom function, passing the address of the regular variable as a reference, and output the modified original value of the regular variable

```c
twice( ptr );
printf( "The num value is now %d\n", num );
thrice( ptr );
printf( "And now the num value is %d\n", num );
```

- 8. At the end of the main function block, return a zero integer value, as required by the function declaration

```c
return 0 ;
```

- 9. Save the program file, then compile and execute the program to see the values output after passing a reference

```text
C:\MyPrograms>gcc passtr.c -o passtr.exe
C:\MyPrograms>passtr
ptr stores address: 0061FF28
*ptr dereferences value: 5
The num value is 5
The num value is now 10
And now the num value is 30
C:\MyPrograms>
```

## Creating arrays of pointers

A C program can contain arrays of pointers in which each element of an array stores the address of other variables.

This ability is especially useful for handling strings of characters. A character array that ends with the \0 null character has string status, so can be assigned to a pointer variable. The name of a string char array acts like a pointer to its first element so the & addressof operator is not needed when assigning a string to a pointer variable.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
`#include <stdio.h>`

- 2. Add a main function that declares an integer variable, then declares and initializes an integer array variable
```c
int main()
{
    int i;
    int nums[5] = { 1, 2, 3, 4, 5 };
}
```

- 3. Next, in the main function block, declare and initialize integer pointer variables with the address of each element
```c
int *ptr0 = &nums[0];
int *ptr1 = &nums[1];
int *ptr2 = &nums[2];
int *ptr3 = &nums[3];
int *ptr4 = &nums[4];
```

- 4. Now, declare and initialize an integer pointer array, with each element containing one of the integer pointers
```c
int *ptrs[5] = { ptr0 , ptr1 , ptr2 , ptr3 , ptr4 };
```

- 5. Next, declare and initialize a character array; a pointer to that array; and a character pointer array with a string in each element
```c
char str[9] = { 'C', ',', 'i', 's', ',', 'F', 'u', 'n', '\0' };
char *string = str;
char *strings[3] = { "Alpha", "Bravo", "Charlie" };
```

![](img/d1dfb0563339ba187decb78799155b7f_105_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_105_1.png)

Notice how the value of the counter i is substituted for the element index number on each iteration of the loop.

- 6. Add a loop to output the address of each integer pointer array element and their dereferenced values

~~~c
for(i = 0; i < 5; i++ )
{
    printf( "The value at %p is: %d\n" , ptrs[i], *ptrs[i] );
}
~~~

![](img/d1dfb0563339ba187decb78799155b7f_106_0.png)

> > **Don't forget**
> > The entire string in a char array is referenced by the pointer name alone – without the * dereference operator.

- 7. Add a statement to output the value stored in the character array

~~~c
printf( "\nString is: %s\n\n" , string );
~~~

- 8. Add a loop to output the string stored in each character pointer array element

~~~c
for( i = 0 ; i < 3 ; i++ )
{
    printf( "String %d is: %s\n" , i , strings[i] );
}
~~~

- 9. At the end of the main function block, return a zero integer value, as required by the function declaration

~~~c
return 0 ;
~~~

- 10. Save the program file, then compile and execute the program to see the values output from the pointer array elements

~~~
Command Prompt

C:\MyPrograms>gcc arprtr.c -o arprtr.exe

C:\MyPrograms>arprtr
The value at 0061FF00 is: 1
The value at 0061FF04 is: 2
The value at 0061FF08 is: 3
The value at 0061FF0C is: 4
The value at 0061FF10 is: 5

String is: C is Fun

String 0 is: Alpha
String 1 is: Bravo
String 2 is: Charlie

C:\MyPrograms>
~~~

![](img/d1dfb0563339ba187decb78799155b7f_106_1.png)

> > **Beware**
> > To include a space in a string there must actually be a space between the single quotes, like this ' ' – two single quotes together, such as '' is seen as an empty element and causes a compiler error.

## Pointing to functions

Pointers can be created that point to functions, although this ability is used less than pointers that point to data values.

A pointer to a function is like a pointer to data but must always be enclosed within parentheses when using the * dereference operator to avoid a compiler error. These will also be followed by further parentheses containing any arguments to be passed to the function to which the pointer points.

The function pointer contains the address in memory at which the function to which it points begins. When the function pointer is dereferenced, the function to which it points gets called, and any arguments specified to the function pointer get passed to the called function.

A function pointer can even be passed as an argument to another function – so the receiving function may then call the function to which the function pointer points.

![](img/d1dfb0563339ba187decb78799155b7f_107_0.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
`#include <stdio.h>`

- 2. Declare a custom function prototype that has an integer argument, and another that has both a function pointer argument and an integer argument
`int bounce(int a);`
`int caller(int (*function)(int), int b);`

- 3. Add a main function that declares an integer variable, then declares and initializes a function pointer variable
`int main()`
`{`
`  int num;`
`  int (*fptr)(int) = bounce;`
`}`

- 4. After the main function block, define the first custom function to output a received value and return an integer
`int bounce(int a)`
`{`
`  printf("\nReceived Value: %d\n", a);`
`  return ((3 * a) + 3);`
`}`

...cont'd

- 5. Next, define the second custom function to call a regular function from a received function pointer, and pass it a received integer value

```c
int caller( int (*function)(int), int b )
{
    (*function)(b);
}
```

![](img/d1dfb0563339ba187decb78799155b7f_108_0.png)

The first argument to the caller() function in this example may be a pointer to any function that receives one integer argument and returns an integer value - as specified in the prototype declaration.

- 6. Back in the main function block, assign a value to the integer variable by calling the regular function via the function pointer, and output the value it returns

```c
num = (*fptr)(10);
printf( "Returned Value: %d\n", num );
```

- 7. Now, assign a new value to the integer variable by passing the function pointer and an integer to another function, which in turn calls the regular function, then output the value it returns

```c
num = caller( fptr, 5 );
printf( "Returned Value: %d\n", num );
```

- 8. At the end of the main function block, return a zero integer value, as required by the function declaration

```c
return 0 ;
```

- 9. Save the program file, then compile and execute the program to see the values output via function pointers

![](img/d1dfb0563339ba187decb78799155b7f_108_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_108_2.png)

Like other pointers in C programming, a function pointer simply stores a memory address. When a function pointer is dereferenced with * the function at that address to which the pointer points gets called.

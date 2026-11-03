
## Pointing to structures

Pointers to struct data types can be created in just the same way as pointers to regular data types. In this case, the pointer holds the address of the beginning of the region of memory used to store the member data.

The use of pointers to structures is so common in C programs that there is even a special operator to describe it. In a struct pointer the "." dot operator can be replaced by "->", which is a hyphen followed by the greater-than operator. This combination is known as the arrow operator. For example, a pointer to a struct member ptr->member is the equivalent of (*ptr).member.

![](img/d1dfb0563339ba187decb78799155b7f_131_0.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```c
#include <stdio.h>
```

- 2. Next, declare an un-named structure defining a data type with two character pointer members and one tag name

```c
typedef struct {
  char *name; char *popn ;
} City ;
```

- 3. Now, add a main function that declares three regular variables and a pointer variable, all of the struct data type

```c
int main()
{
  City ny , la , ch , *ptr ;
}
```

- 4. Within the main function block, assign values to members of the first variable then display the stored values, using the dot operator to both store and retrieve the values

```c
ny.name = "New York City" ;
ny.popn = "8,274,527" ;
printf( "\n%s , Population: %s\n", ny.name , ny.popn ) ;
```

- 5. Assign the address of the second variable to the pointer variable

```c
ptr = &la ;
```

![](img/d1dfb0563339ba187decb78799155b7f_131_1.png)

The arrow operator is useful in C programming to differentiate between structure pointers and other pointers.

- 6. Now, assign values to members of the second variable, then display the stored values, using the arrow operator to store the values and the dot operator to retrieve the values

```c
ptr->name = "Los Angeles";
ptr->popn = "3,834,340";
printf( "\n%s, Population: %s\n" , la.name, la.popn );
```

- 7. Next, assign the address of the third variable to the pointer variable

```c
ptr = &ch ;
```

- 8. Now, assign values to members of the third variable, then display the stored values, using the arrow operator to both store and retrieve the values

```c
ptr->name = "Chicago";
ptr->popn = "2,836,658";
printf( "\n%s, Population: %s\n" , ptr->name, ptr->popn );
```

- 9. At the end of the main function block, return a zero integer value, as required by the function declaration

```c
return 0;
```

- 10. Save the program file, then compile and execute the program to see the values stored in the structure members

The population values in this example are assigned as strings to preserve the comma separations.

![](img/d1dfb0563339ba187decb78799155b7f_132_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_132_1.png)

## Passing structures to functions

Structure member values can be stored in an array, just like the values of any other data type. The array is declared as usual, but the method used to assign the values to its elements is slightly different. Each comma-separated list of member values must be enclosed within a pair of braces.

Similarly, a struct can be passed as an argument to a function, just like any other variable. The structure's data type must be specified in both the function prototype declaration and its definition, along with a variable name by which the function can address its member values.

But remember that passing by value, simply using a regular variable, means that the function will operate on a copy of the struct – its original member values will remain unchanged. Passing the struct by reference, on the other hand, using a pointer variable, means that the function will operate on the original struct members – so the original member values will get changed.

![](img/d1dfb0563339ba187decb78799155b7f_133_0.png)

> Simply assigning all the values as a comma-separated list will not work – each set of values must be enclosed by its own pair of braces.

![](img/d1dfb0563339ba187decb78799155b7f_133_1.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```c
#include <stdio.h>
```

- 2. Next, declare an un-named structure defining a data type with two members and one tag name

```c
typedef struct
{
  char *name ;
  int quantity ;
} Item ;
```

- 3. Now, declare an array of the structure's data type, initializing each member of three structures

```c
Item fruits[3] =
{ { "Apple", 10 }, { "Orange", 20 }, { "Pear", 30 } };
```

- 4. Add a function prototype that will pass a structure variable and a pointer variable to a structure as arguments

```c
void display( Item val , Item *ref );
```

## Grouping in a union

In C programming, a “union” allows different pieces of data, of any data type, to be stored at the same memory location as the program proceeds – assigning a value to the union will overwrite that previously stored there. This allows efficient use of memory.

A union is like a struct but is declared with the union keyword and, because of its nature, its members can only be assigned values individually as the program proceeds.

An array of unions can be created in the same way as an array of structs was created in the previous example, but union members can only be initialized in the declaration if they are all of the same data type. A pointer to a union can be created in exactly the same manner in which a pointer to a struct is created and a union can be passed to a function just like any other variable.

![](img/d1dfb0563339ba187decb78799155b7f_135_0.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```c
#include <stdio.h>
```

- 2. Next, declare an un-named structure defining a data type with three members and one tag name

```c
typedef struct { int num ; char ltr , *str } Distinct ;
```

- 3. Now, declare an un-named union defining a data type with three members and one tag name

```c
typedef union { int num ; char ltr , *str ; } Unified ;
```

- 4. Add a main function that declares a variable of the struct's data type and initializes each of its members

```c
int main()
{
Distinct sdata = { 10 , 'C' , "Program" } ;
}
```

- 5. Now, in the main function block, declare a variable of the union data type

```c
Unified udata ;
```

![](img/d1dfb0563339ba187decb78799155b7f_135_1.png)

> It is the programmer's responsibility to understand which type of data is being stored in a union at any point in the execution of a program.

- 6. After the variable declarations, output the value and memory address of each struct member

```c
printf("\nStructure:\nNumber: %d", sdata.num );
printf("\tStored at: %p\n", &sdata.num );
printf("Letter: %c", sdata.ltr );
printf("\tStored at: %p\n", &sdata.ltr );
printf("String: %s", sdata.str );
printf("\tStored at: %p\n", &sdata.str );
```

![](img/d1dfb0563339ba187decb78799155b7f_136_0.png)

- 7. Now, assign a value to the first union member then output its value and memory address

```c
udata.num = 16 ;
printf( "\nUnion:\nNumber: %d" , udata.num );
printf( "\tStored at: %p\n" , &udata.num );
```

- 8. Next, assign a value to the second union member then output its value and memory address

```c
udata.ltr = 'A' ;
printf( "Letter: %c" , udata.ltr );
printf( "\tStored at: %p\n" , &udata.ltr );
```

- 9. Finally, assign a value to the third union member then output its value and memory address

```c
udata.str = "Union" ;
printf( "String: %s" , udata.str );
printf( "\tStored at: %p\n" , &udata.str );
```

- 10. At the end of the main function block, return a zero integer value, as required by the function declaration

```c
return 0 ;
```

- 11. Save the program file, then compile and execute the program to see the values stored in the structure, and union members and the addresses where they are stored

```text
C:\MyPrograms>gcc union.c -o union.exe
C:\MyPrograms>union
Structure:
Number: 10    Stored at: 0061FF24
Letter: C     Stored at: 0061FF28
String: Program Stored at: 0061FF2C

Union:
Number: 16    Stored at: 0061FF20
Letter: A     Stored at: 0061FF20
String: Union Stored at: 0061FF20
```

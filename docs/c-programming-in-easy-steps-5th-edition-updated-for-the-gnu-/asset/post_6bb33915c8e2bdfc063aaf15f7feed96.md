
```
return 0 ;
```

Save the program file, then compile and execute the program to see the values stored in the structure members

![](img/db19f3858a1e321646bf2590afd29547_186_0.png)

![](img/db19f3858a1e321646bf2590afd29547_186_1.png)

Notice that the members of different structures can be named alike without conflict.

![](img/db19f3858a1e321646bf2590afd29547_186_2.png)

The elements of a char array can only be initialized using a comma-separated list in its declaration.

## Pointing to structures

Pointers to struct data types can be created in just the same way as pointers to regular data types. In this case, the pointer holds the address of the beginning of the region of memory used to store the member data.

The use of pointers to structures is so common in C programs that there is even a special operator to describe it. In a struct pointer the “.” dot operator can be replaced by “->”, which is a hyphen followed by the greater-than operator. This combination is known as the arrow operator. For example, a pointer to a struct member ptr->member is the equivalent of (*ptr).member.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_187_0.png)

structptr.c

- 2. Next, declare an un-named structure defining a data type with two character pointer members and one tag name

```
typedef struct
{
    char *name; char *popn ;
} City ;
```

- 3. Now, add a main function that declares three regular variables and a pointer variable, all of the struct data type

```
int main()
{
    City ny , la , ch , *ptr ;
}
```

- 4. Within the main function block, assign values to members of the first variable then display the stored values, using the dot operator to both store and retrieve the values

```
ny.name = "New York City" ;
ny.popn = "8,274,527" ;
printf( "\n%s , Population: %s\n", ny.name , ny.popn ) ;
```

- 5. Assign the address of the second variable to the pointer variable
ptr = &la ;

![](img/db19f3858a1e321646bf2590afd29547_188_0.png)

The arrow operator is useful in C programming to differentiate between structure pointers and other pointers.

- 6. Now, assign values to members of the second variable, then display the stored values, using the arrow operator to store the values and the dot operator to retrieve the values

```
ptr->name = "Los Angeles" ;
ptr->popn = "3,834,340" ;
printf( "\n%s, Population: %s\n", la.name, la.popn ) ;
```

- 7. Next, assign the address of the third variable to the pointer variable
ptr = &ch ;

- 8. Now, assign values to members of the third variable, then display the stored values, using the arrow operator to both store and retrieve the values

```
ptr->name = "Chicago" ;
ptr->popn = "2,836,658" ;
printf( "\n%s, Population: %s\n", ptr->name, ptr->popn ) ;
```

- 9. At the end of the main function block, return a zero integer value, as required by the function declaration
return 0 ;

- 10. Save the program file, then compile and execute the program to see the values stored in the structure members

```
C:\MyPrograms>gcc structptr.c -o structptr.exe

New York City, Population: 8,274,527
Los Angeles, Population: 3,834,340
Chicago, Population: 2,836,658

C:\MyPrograms>
```

The population values in this example are assigned as strings to preserve the comma separations.

## Passing structures to functions

Structure member values can be stored in an array, just like the values of any other data type. The array is declared as usual, but the method used to assign the values to its elements is slightly different. Each comma-separated list of member values must be enclosed within a pair of braces.

![](img/db19f3858a1e321646bf2590afd29547_190_0.png)

Simply assigning all the values as a comma-separated list will not work – each set of values must be enclosed by its own pair of braces.

Similarly, a **struct** can be passed as an argument to a function, just like any other variable. The structure’s data type must be specified in both the function prototype declaration and its definition, along with a variable name by which the function can address its member values.

But remember that passing by value, simply using a regular variable, means that the function will operate on a copy of the struct – its original member values will remain unchanged. Passing the struct by reference, on the other hand, using a pointer variable, means that the function will operate on the original struct members – so the original member values will get changed.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```c
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_190_1.png)

passtruct.c

- 2. Next, declare an un-named structure defining a data type with two members and one tag name

```
typedef struct
{
 char *name ;
 int quantity ;
} Item ;

```

Now, declare an array of the structure’s data type, initializing each member of three structures

```
Item fruits[3] = {{ "Apple" , 10 },{ "Orange" , 20 },{ "Pear" , 30 }} ;
```

Add a function prototype that will pass a structure variable and a pointer variable to a structure as arguments

```
void display( Item val, Item *ref );
```

Now, define the function declared in the prototype that begins by revealing the value of the passed arguments

```
void display( Item val, Item *ref )
{
 printf("%s: %d\n", val.name, val.quantity );
 }
```

Next, in the function block, change the values of the struct member copies passed then output the new values

```
val.name = "Banana" ; val.quantity = 40 ;
printf("%s: %d\n", val.name, val.quantity );
```

Confirm that the original values are unchanged

```
printf("%s: %d\n", fruits[0].name, fruits[0].quantity );
```

Then, change the original member values and output the new values

```
ref->name = "Peach" ;
ref->quantity = 50 ;
printf("%s: %d\n", fruits[0].name, fruits[0].quantity );
```

Just before the function block, insert a main function that calls the other function, passing a struct and a pointer as arguments

```
int main()
{
 display( fruits[0], &fruits[0] );
 }
```

At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0 ;
```

Save the program file, then compile and execute the program to see the values stored in the structure members

```
C:\MyPrograms>gcc passstruct.c -o passstruct.exe
C:\MyPrograms>passstruct
Apple: 10
Banana: 40
Apple: 10
Peach: 50
C:\MyPrograms>_
```

![](img/db19f3858a1e321646bf2590afd29547_192_0.png)

Passing large structs by value is inefficient as it creates a copy of the entire struct in memory, whereas passing by reference only requires the size of a pointer.

## Grouping in a union

In C programming, a “union” allows different pieces of data, of any data type, to be stored at the same memory location as the program proceeds – assigning a value to the union will overwrite that previously stored there. This allows efficient use of memory.

A union is like a struct but is declared with the union keyword and, because of its nature, its members can only be assigned values individually as the program proceeds.

An array of unions can be created in the same way as an array of structs was created in the previous example, but union members can only be initialized in the declaration if they are all of the same data type. A pointer to a union can be created in exactly the same manner in which a pointer to a struct is created and a union can be passed to a function just like any other variable.

![](img/db19f3858a1e321646bf2590afd29547_193_0.png)

union.c

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
`#include <stdio.h>`

- 2. Next, declare an un-named structure defining a data type with three members and one tag name
`typedef struct { int num ; char ltr , *str ; } Distinct ;`

- 3. Now, declare an un-named union defining a data type with three members and one tag name
`typedef union { int num ; char ltr , *str ; } Unified ;`

- 4. Add a main function that declares a variable of the struct’s data type and initializes each of its members
`int main()`

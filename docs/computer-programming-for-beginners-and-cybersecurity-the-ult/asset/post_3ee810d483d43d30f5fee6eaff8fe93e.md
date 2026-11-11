
To create a pointer, we use the dereferencing operator (*), this will create a pointer variable that is designed to hold a memory location's address. Below is a program that creates a pointer and uses the reference operator (&) to store another regular variable's address in the newly created pointer. The dereferencing operator (*) is also used to access or change the actual data in that memory location.

- Dereferencing operator (*) is used to create a pointer, it is also used when changing the actual value
- Referencing operator (&) is used when obtaining the memory location of a pointer

Must be in increased indent.

```c
//Regular variable

int var = 10;

//Pointer
int* pointer;

//Storing of var memory location
pointer = &var;

//Pointer is now effectively 'var' so
//things like this can happen
*pointer = 20;

printf("Var's value is now: %d", var);
```

Output:

> Var's value is now: 20

## NULL pointers

When you create a pointer, it is initially not given anything to point at, this is dangerous because the pointer when created it references random memory, and changing this data in the memory location can crash the program. To prevent this, when we create a pointer we assign it to NULL like so:

```c
int* pointer = NULL;
```

This means the pointer has an address of '0', this is a reserved memory location to identify a null pointer. A null pointer can be checked by an if statement:

```c
if (pointer){}
```

## Using pointers

Now some real-world uses of pointers are passing them as parameters and effectively passing them by reference. The example below will show the effect:

```c
void Change_Value(int* reference)
{
    //Changes the value in the memory location
    *reference = 20;
}

int main()
{
    //Creates pointer to variable
    int var = 10;
    int* pointer = &var;
    printf("The value before call: %d\n", var);
    //Method call
    Change_Value(pointer);

    //Prints new value
    printf("The value after call: %d\n", var);
    return 0;
}
```

Output:

> The value before call: 10
> The value after call: 20

This passes the memory location, not the value of the variable, meaning you have the location where you can make changes.

Note the parameter is int* this is the pointer type, so for example, a pointer to a char would be char*.

## Pointer Arithmetic

There are times when moving a pointer along to another memory location might be useful; this is where pointer arithmetic comes into use. If we were to execute say ptr++ and the ptr was an integer pointer it would now move 4bytes (Size of an int) along, and we were to run it again, another 4bytes etc. This can mean a pointer (if pointing to valid array structures) can act much like an array can. An example is below:

```c
int arrayInt[] = { 10, 20, 30 };

size_t arrayInt_Size = 3;

//Will point to the first array index
int* ptr = &arrayInt;
for (int i = 0; i < arrayInt_Size; i++)
{
    //Remember, *ptr gets the value in the memory location
    printf("Value of arrayInt[%d] = %d\n", i, *ptr);

    ptr++;
}
```

Output:

> Value of arrayInt[0] = 10
> Value of arrayInt[1] = 20
> Value of arrayInt[2] = 30

This shows that a pointer to the first address of the array can be incremented along the addresses of the array (Remember each value of an array is stored in neighbouring memory locations)

You can do the opposite and decrement a pointer i.e. make the pointer's value decrease.

There is also a way to compare pointers using relational operators such as ==, < and >. The most common use for this is checking if two pointers point to the same location:

```c
int value;

//Assigns ptr1 and ptr2 the same value
int* ptr1 = &value;
int* ptr2 = &value;

//ptr3 is assigned another value
int* ptr3 = NULL;

if (ptr1 == ptr2)
{
    printf("ptr1 and ptr2 are equal!\n");
}

if (ptr1 != ptr3)
{
    printf("ptr1 is not equal to ptr3\n");
}
```

This checks if the various pointers are equal. The same can be done with > and <.

## Function pointers

Much like you can do with variables, you can also do the same with functions; below is a snippet of code that shows a function pointer being defined. Key sections will be highlighted:

```c
void printAddition(int value1, int value2)
{
    int result = value1 + value2;
    printf("The result is: %d", result);
}

int main()
{
    //Function pointer definition
    //<returnType>(*<Name>)(<Parameters>)
    void(*functionPtr)(int, int);
    functionPtr = &printAddition;
    //Invoking call to pointer function
    (*functionPtr)(100, 200);
    return 0;
}
```

The basic structure for defining a function pointer is like so

`<Return_Type> (*<Name>) (<Parameters>)`

Where in this case:

`<Return_Type> = void`

`<Name> = functionPtr`

`<Parameters> = int, int`

This function pointer can now be passed as a parameter and used in situations where you would want to change the behaviour of code but with almost the same code.

An example could be dynamically choosing what operation a calculator should perform (Note: this is complex code and should be used as a rough example, so don’t worry if you don’t fully understand)

```c
void calculator(int value1, int value2, int(*opp)(int,int))
{
    int result = (*opp)(value1, value2);
    printf("The result from the operation: %d\n", result);
}

//Adds two values
int add(int num1, int num2)
{
    return num1 + num2;
}

//Subtracts two values
int sub(int num1, int num2)
{
    return num1 - num2;
}

int main()
{
    calculator(10, 20, &add);
    calculator(10, 20, &sub);
    return 0;
}
```

Here what is happening we are passing the function ‘add’ and ‘sub’ as parameters for the function calculator, as you see from the highlight the function parameter is defined like it is above with the return type, name and parameters being defined, all that is passed into calculator is &add and &sub for the function pointers. The calculator function then goes on to invoke the pointer and passes in the values and returns the result.

## Storage Classifications

In C each variable can be given a storage class that can define certain characteristics.

The classes are:

- Automatic variables
- Static variables
- Register variables
- External variables

### Automatic variables

Every variable we have defined so far has been an automatic variable; they are created when a function is called and automatically destroyed when a function exits. These variables are also known as local variables.

```c
auto int value;
```

Is the same as

```c
int value;
```

### Static variables

Static is used when you want to keep the variable from being destroyed when it goes out of scope; this variable will persist until the program is complete. The static variable is created only once throughout the lifetime of the program. Below is an example of a static variable in use:

```c
void tick()
{
    //This will run once
    static int count = 0;
    count++;
    printf("The count is now: %d\n", count);
}

int main()
{
    tick();
    tick();
    tick();
}
```

Output:

> The count is now: 1
> The count is now: 2
> The count is now: 3

The highlighted section is the static definition and will only run once.

### Register variables

The register is used to define a variable that is to be stored in register memory as opposed to regular memory, the benefits register memory has is it is much much quicker to access; however, there is only space for a few variables.

Defining a register variable is done like so:

```c
register int value;
```

### External variable

We touched on this before, but a global variable is a variable not defined in a scope and, therefore, can be used anywhere. An external variable is a variable defined in a separate location like another file, and the extern keyword is used to signify that the variable is in another file. You would include another file as a reference by placing this at the top of your file:

```c
#include "FileName.c"
```

This is to tell the program to reference this file as well. Note the files need to be in the same location.

Program 1 [File_2.c]

```c
#include <stdio.h>

#include "C_TUT.c"

int main()

{
```

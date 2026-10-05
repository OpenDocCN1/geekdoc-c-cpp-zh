
An integral literal without a prefix indicates a decimal number (base 10).

| Type | Representation |
| --- | --- |
| unsigned int | U or u |
| unsigned long int | UL or ul |
| long long | LL or ll |
| unsigned long long | ULL or ull |

## Variable Scope In C And C++

Variable scope refers to the region of a program where a variable exists and can be accessed.

In C there are three places where a variable can be declared:

- inside a brace delimited block { ... } (local variables)
- in the parameter list of a function
- outside all functions (global variables)

Pair of braces {} defines a block and variables declared inside a block have their scope restricted to the block. In C, the scope of a variable begins at the point of it's declaration.

C and C++ implement **lexical scope**. This means the scope of any variable can be determined at compile-time by examining the source code.

**Lexical scope** can be explained as follows. Suppose the compiler encounters a variable name in a block of code and wants to know whether the name exists and it's value. The compiler first examines the current block for the declaration of the name and if not found; it examines any outer enclosing block(s) and finally the global scope for the variable name.

The following C++ program shows C/C++ lexical scoping:

```cpp
#include <iostream>
int value = 999;

void f()
{
    int value = 1;
    std::cout << "value in f - " << value << std::endl;
}
```

```cpp
{
  std::cout << "value in f - " << value << std::endl;
}

int main() {
{
  int value = 2;
  f();
  std::cout << "value in main - " << value << std::endl;
  return 0;
}

// output
value in f - 1
value in f - 999
value in main - 2
```

## C Language: Function Prototypes

### Forward Declarations

The following program will not compile:

```cpp
#include <stdio.h>

int main() {
    printMe(5);
}

// printMe declared and defined here
void printMe(int x) {
    printf("%d", x);
}
```

The problem is when the compiler encounters the printMe statement in main, it does not know what printMe is, since printMe has not been declared. This problem can be solved by including the definition of printMe before main or by including the declaration of printMe before it is used.

```cpp
#include <stdio.h>

// forward declaration
void printMe(int);

int main() {
    printMe(5);
}

// definition of printMe
void printMe(int x) {
    printf("%d", x);
}
```

This forward declaration of printMe is also called a function prototype.

## The void Type

The data type void represents no value. Functions should always be declared as void if they do not take any parameters.

Consider the following two prototypes:

```cpp
void foo(void);
void foo();
```

The C compiler interprets the first prototype as not taking any parameters and not returning any value. The second declaration is interpreted by the C compiler as not knowing whether foo takes any parameters and returning no value (the C++ compiler behaves differently).

## C Language: C Style Casts

A variable value is stored as a sequence of bits. The data type of a variable tells the compiler how to translate these bits into meaningful values. Different data types may represent the "same" number differently. For example, the integer value 3 and the float value 3.0 are stored as completely different bit patterns.

In C we can convert a variable or a literal from one type to another by preceding the variable or literal with the target type in round brackets:

```c
float y = (float) 6/4;
```

This is an example of type conversion. The compiler will convert the integer number 6 to a float and then divide it by 4 to get 1.25. Note that if the float type conversion is not present on the right hand side, then the right hand side will evaluate to 1 and 1.0 will be assigned to y. Since y is a float type the compiler performs an implicit type conversion of the integer 1 to a float type.

## Function-Style Casts

C also implements function-style casts:

```c
T(expression)
```

where T is some type.

```c
int x = int(3.14)          // 3.14 is cast to an int type.
```

## Implicit Type Conversion

The type conversions that we have shown in the examples above are explicit type conversions. However the compiler will automatically attempt an implicit type conversion when the target type is a type different from the subject type. An implicit type conversion or automatic type conversion will occur in three cases:

### During Initialization:

```c
float y = 5; // int type 5 converted to float
```

### When Setting Function Parameters:

```c
int myFunc(float p); // myFunc is called with an int argument. For example, myFunc(3)
```

### Function Return Values:

A function's return value is changed to a different type.

```c
float y = myFunc(5); // myFunc returns an integer type
```

Automatic type conversion occurs whenever a value from one fundamental data type is converted to another. (Note: The original text contained significant corruption/garbled characters here, which has been cleaned based on context).

## C Language: Pointers

A pointer is a variable that stores the address of another variable. The syntax for a pointer declaration is:

```c
int *ptr;
```

This states that *ptr* is a pointer and its value is the address of a variable of *int* type. Note that this is a declaration only and *ptr* has not been initialized. Suppose that we have:

```c
int x = 5;
```

Then the address of *x* (the memory address where *x* is stored) is:

```c
&x
```

The **address operator &** gets the address of the variable *x*. We can initialize *ptr* (point *ptr* to *x*) as follows:

```c
ptr = &x;
```

Now *ptr* contains the address of *x*. We can obtain the value at the address pointed by *ptr* as follows:

```c
int value = *ptr;
```

This is referred to dereferencing the pointer. * is the **dereferencing operator** gets the value at the location *ptr* points to.

## Pointer Arithmetic

Pointer variables can be incremented and decremented. An increment sets the value of pointer variable to a location that is size of (the data type pointed to) bytes ahead of the current value of the pointer.

In our example, pointer is pointing to an int type which is 4 bytes long, so ++ptr points to the location four bytes ahead of the current location. Similarly with the decrement operator. Ordinary addition and subtraction work similarly.

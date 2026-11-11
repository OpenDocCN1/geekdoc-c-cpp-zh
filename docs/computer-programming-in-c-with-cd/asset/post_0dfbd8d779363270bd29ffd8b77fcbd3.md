
- Initialization of variables
- Reference variables
- Scope of variables

## Variable Declaration

In C++, variables can be declared anywhere in the program, unlike C where all the variables need to be declared at the beginning of the program. The syntax to declare a variable in C++ is the same as in C:

```
datatype var_name;
```

In the preceding syntax,

- **datatype**: Refers to any valid C++ data type, such as int, float, or char
- **var_name**: Refers to the name of the variable to be declared

The following code snippet shows the declaration of variables:

```
int x;
char c;
```

In the preceding code snippet, the x variable is declared as integer type, which will hold the integer values. The c variable of the char data type is also declared, which will hold the character type data. You can declare multiple variables of the same data type in a single line by separating them with commas, as shown in the following code snippet:

```
int x, y, z;
```

The preceding code snippet for declaring variables is exactly the same in comparison to the one shown in the following code snippet:

```
int x;
int y;
int z;
```

In the preceding code snippet, the x, y, and z variables of the int type are declared. After declaring a variable, you must initialize it to access it in a program. Let’s now discuss how to initialize variables.

## Variable Initialization

Variables are initialized to store some values in it. The syntax to initialize variables in C++ is:

```
var_name = value;
```

The preceding syntax is common in both C and C++. In this syntax, the `var_name` variable is initialized with the `value` value.

The following code snippet shows the initialization of variables:

```
x = 10; // common in both C and C++
```

In the preceding code snippet, the x variable is initialized with the value 10 by using both the already discussed syntaxes to initialize a variable. The syntax to initialize and declare a variable is:

```
datatype var_name = value;
```

The following code snippet shows the valid initialization and declaration of variables:

```
int x=10; // common in both C and C++
```

In the preceding code snippet, the x variable is declared as well as initialized.

Apart from initializing variables with integer values, you can also declare variables that can store decimal values, as shown in the following code snippet:

```
float num1, num2; //declaring float variables
num1 = 5.25; //initializing float variables
num2 = num1 * 3.24;
```

In the preceding code snippet, the real variables num1 and num2 are declared and initialized.

Next, let’s discuss reference variables in C++.

## Reference Variables

A reference variable is a variable that provides a second name (alias) for an already existing variable. It may not sound appealing at first and you may question the need for creating an alias for an already existing variable. A reference variable helps you to pass values to a function by reference. Reference variables allow you to access and modify the content stored in the original variable. The syntax to create a reference variable is:

```
datatype &ref_var = var_name;
```

In the preceding syntax,

- datatype: Refers to the type of data the variable will hold
- `&ref_var`: Refers to the name of the reference variable to be declared
- `var_name`: Refers to the variable name whose reference variable is created

A reference variable is created by using the & symbol with the name of the reference variable. The following code snippet shows the declaration and initialization of reference variables:

```
int x=10; // x is original variable
int &a = x; // a is alias of x

int y[10]; // y is original variable representing array
int &b=y[6]; // b is alias for the value stored at 6th index in array y.
```

The & symbol in the reference variable points to the memory address where the original variable is stored; therefore, both the original variable and its alias represents the same memory location.

## Scope of Variables

The scope of variables depends on the location they are declared in a program. Variables can either have a local scope or a global scope. A variable is considered to have local scope when it is declared inside a function or block within curly braces ({}). However, when a variable is declared outside a function, it becomes a global variable. The following code snippet clarifies the concept of variable scope:

```
#include <iostream.h>
int x; // global variable
int main ()
{
    int y; // local variable
    .
    .
}
```

In the preceding code snippet, int x is a global variable, whereas int y is a local variable. A global variable can be accessed anywhere in the program, whereas a local variable is accessible only in the function or block where it is declared.

You are now familiar with variables and how they are used in C++. In the next section, let’s discuss C++ data types.

## Data Types

Data types are a very important part of a language, as you cannot even declare variables without them. The term data type is used to specify the type of a variable, which means we have to specify that what kind of data a variable will store. The data type used with a variable name also specifies how much memory a variable can utilize to store data in it. For example, the long data type in C++ has the size of 4 bytes, that is, a variable of type long can utilize 4 bytes of memory. Table 2 lists the simple data types available in standard C++:

**Table 2: Data Types in C++**

| Type | Description |
|---|---|
| bool | Holds true (non-zero) or false (zero) values |
| char | Contains characters, such as a and b |
| signed char | Represents a char type with numeric sign, such as − and + |
| unsigned char | Represents a char type with no numeric sign |
| short | Represents an integer that is larger than or equal to the char type, and shorter than or equal to the int type |
| short int | Same as short type but only represents an integer value |
| signed short | Same as the short type, except for the range, which is -32768 to 32767 |
| unsigned short | Same as the short type, except for the range, which is 0 to 65535 |
| int | Represents a basic integer type |
| signed int | Same as the int type, except for the range, which is -2147483648 to 2147483647 |
| unsigned int | Same as the int type, except for the range, which is 0 to 4294967295 |
| long | Represents a long integer |
| signed long | Same as the long type, except for the range, which is -2147483648 to 2147483647 |
| unsigned long | Same as the long type, except for the range, which is -2147483648 to 2147483647 |
| float | Represents a floating point number |
| double | Represents a double precision floating point number; it usually has more precision than the float type |
| long double | Represents a floating point number with even more precision than the double type |
| void | Represents a void type |

Data types in C++ can be divided into the following three broad categories:

- Built-in
- User-defined
- Derived

Let’s discuss these data types one by one.

### Built-in Data Types

The C++ compiler supports all built-in data types, which are also known as basic or fundamental data types. Except for the void data type, all built-in data types may have several modifiers, such as signed, unsigned, long, and short applied to the character and integer data types. The built-in data types in C++ are as follows:

- Integer type
- Character type
- Floating point type
- Boolean type
- Void

Let’s discuss each of these in detail.

### Integer Types

C++ provides three integer types: short, int, and long. It also supports signed integers as well as unsigned integers. Signed integers have −ve and +ve values, while unsigned integers have only positive values. Among all the integer types, short is the smallest integer type and long is the largest integer type. Table 3 shows the width and range of the int, long, and short data types:

**Table 3: Range of Integer Type Data Types in C++**

| Data Type | Representation | Width (bytes) | Range |
|---|---|---|---|
| short | Short integer | 2 | Signed: -32768 to 32767<br>Unsigned: 0 to 65535 |
| int | Integer | 2 (16 bit compiler)<br>4 (32 bit compiler) | Signed: -32768 to 32767<br>Unsigned: 0 to 65535<br>Signed: -2147483648 to 2147483647<br>Unsigned: 0 to 4294967295 |
| long | Long integer | 4 | Signed: -2147483648 to 2147483647<br>Unsigned: 0 to 4294967295 |

The following code snippet shows the declaration of the variables of the int type:

```cpp
//declaring int type variables
int x;
int sum;
int age;
```

In the preceding code snippet, the x, sum, and age variables are of the int type, which will hold integer values. Apart from the int data type, you can also declare shorter integer type variables, which occupy less memory space and thereby speed up program execution. The following code snippet shows the declaration of short integer type variables:

```cpp
//declaring short int type variables
short int x;
short int sum;
short int age;
```

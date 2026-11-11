
In the preceding code snippet, you can see that no value is assigned to the name of days (enumerations), except the enumeration Tuesday. The value assigned to the enumeration Tuesday is 5. The compiler starts assigning values to the enumerations in increasing order, starting with 0 for Sunday. The value assigned to the sequence of numbers changes from Tuesday, which means that the compiler assigns values to the enumerations after Tuesday based on the value of the enumeration Tuesday. This is the reason the compiler assigns 0 to Sunday, 1 to Monday, 5 to Tuesday, 6 to Wednesday, 7 to Thursday, 8 to Friday, and 9 to Saturday.

## TEST YOUR KNOWLEDGE

Q4. Write a program to implement the concept of enumeration.

Ans.

```cpp
#include <iostream.h>
int main()
{
enum month {
    Jan,
    Feb,
    Mar,
    Apr,
    May,
    Jun,
    Jul,
    Aug,
    Sep,
    Oct,
    Nov,
    Dec
};

enum month summer = Jun;
if (summer == May || summer == Jun || summer == Jul)
{
cout << "It is summer " << endl;
}
return 0;

}
```

Output:

```text
It is summer
```

![](img/8a6886c00caa6a1651a6c0e62bff341f_49_0.png)

Write a short note on Enumerated Data type (Mumbai University, May 2009)

## Derived Data Types

Data types that are created from existing data types are known as derived data types. The following are the derived data types available in C++:

- Arrays
- Pointers

### Arrays

An array is a collection of data storage locations, each of which holds the same type of data. Now the question arises, why do we need this kind of complex structure? There can be a situation where you need to store similar type of values for a large number of data items. Primitive data types are fine as long as they are used for storing single data, but what if the data to be stored is more complex? For example, suppose that you want to store the names of 50 students. You can do this by declaring 50 variables, each storing a name. However, this is not the correct approach. Imagine writing 50 statements just to store the names of the students. The solution to this problem lies in using arrays. With arrays, you can declare a single variable that is capable of storing all these 50 names. The advantage of using arrays is that they simplify programming by replacing several statements with just one or two statements. The syntax to declare an array in C++ is:

```cpp
datatype array_name [array_size];
```

In the preceding syntax,

- `datatype`: Refers to a legal C++ data type
- `array_name`: Refers to any identifier used to identify an array
- `array_size`: Refers to an integer value, which represents the total number of elements an array can store

The code snippet to declare an array is:

```cpp
int  item [10];
```

In the preceding code snippet, the item array of the int type is declared. This array can store a maximum of 10 elements.

![](img/8a6886c00caa6a1651a6c0e62bff341f_50_0.png)

Arrays are discussed in more detail in Chapter 3, *Working with Arrays and Functions.*

### Pointer

A pointer in C++ is defined as a variable that stores the memory address of another variable. A pointer is similar to other variables in C++ and needs to be declared before it can be used. Pointers are declared in the same way as other variables. A pointer stores the address of specific data types, such as int, char, and float. The syntax to declare a pointer is:

```cpp
datatype *point_name;
```

In the preceding syntax,

- **datatype:** Refers to any legal primary C++ data type or user-defined data type.
- **point_name:** Refers to any variable name. The * informs the compiler that the variable point_name is a pointer variable.

![](img/8a6886c00caa6a1651a6c0e62bff341f_51_0.png)

> Pointers are discussed in more detail in Chapter 4, Pointers.

After discussing built-in, user-defined, and derived data types, let’s learn how to convert a variable of one data type to another.

## Type Conversion and Type Casting in C++

In C++ the concept of converting an integer type variable into a float type is known as type conversion. Listing 10 shows how the integer type variable is automatically converted to a float type (you can find the IntTypeEx.cpp file on the CD in the code/chapter1 folder:

### Listing 10: Converting an Integer Type Variable to a Float Type

```cpp
#include <iostream.h>
int main()
{
    int a = 10;
    float b = 22.7;
    b = b + a;
    cout << "The value of the b variable is:" <<b;
    return 0;
}
```

**Output:**

```text
The value of the b variable is:32.700001
```

In Listing 10, the int type variable, a, is assigned a value of 10, which is automatically converted to 10.0 during the addition of the values of variables a and b. In Listing 10, you notice the automatic conversion of type from int to float. However, if you want to convert the double type variable to an int type, then you need to explicitly provide code for it. The concept of explicitly converting one data type variable to another is known as type casting. Listing 11 shows how to type cast the double type variable to an int type (you can find the DoubleTypeEx.cpp file on the CD in the code/chapter1 folder):

### Listing 11: Type Casting the Double Type Variable to an Int Type

```cpp
#include <iostream.h>
int main()
{
double a = 2134.56;
int b;
b = int(a);
cout << "The value of the b variable is:" <<b;
return 0;
}
```

Output:

The value of the b variable is:2134

In Listing 11, a double type variable is type cast to the int type variable, b. After discussing the concept of type casting and type conversion, let's now learn about preprocessor directives that help you to include files in a C++ program and define macros.

## Preprocessor Directives

Preprocessor directives are handled before the code is passed to the C++ compiler. The compiler includes a preprocessor that handles preprocessor directives before the starting of the C++ compilation process. Preprocessor directives helps you to perform operations, such as including header files in a C++ program so that you can utilize the functions stored in header files, and defining constants. The preprocessing directives in C++ are as follows:

- `#define`: Defines a macro/token
- `#elif`: Represents the else-if directive, which works similar to the else-if statement
- `#else`: Represents the else directive, which works similar to the else statement
- `#error`: Produces compile time error messages
- `#if`: Represents the if directive, which works similar to the if statement
- `#ifdef`: Represents the if-defined directive used to test the existence of a macro
- `#ifndef`: Represents the if-not-defined directive
- `#include`: Includes a file in the C++ program
- `#line`: Represents the current line directive
- `#pragma`: Represents a special function that runs before the code
- `#undef`: Undefines a defined macro

You can use these preprocessor directives with predefined tokens, such as _cplusplus that is defined if the current program is in C++, and undefined otherwise. You can check if a token is defined with an `ifdef` directive, which starts with `#ifdef` keyword and ends with `#endif` keyword. The following code snippet checks whether or not a program is created in C++:

```cpp
#ifdef _cplusplus
cout << "This is a C++ program." << endl;
#endif
```

Some of the predefined tokens you can use in your code are as follows:

- `_cplusplus`: Defined if the current program is in C++
- `_STDC_`: Defined if the current program is in standard C
- `__LINE__`: Holds the current line number
- `__FILE__`: Holds the current file name
- `__DATE__`: Holds the date of compilation of a program
- `__TIME__`: Holds the time of compilation of a program

Preprocessor directives also support *macros*, which are sections of predefined code. These macros are replaced by the preprocessor along with the values stored in the macros. All preprocessor directives are discussed in detail under following sections:

- The #define directive
- The #undef directive
- The #include directive
- Directives used in conditional compilation

### The #define Directive

The #define directive is a preprocessor directive used to give a meaningful name to a constant in a C++ program and the constant is then used as a macro in the program. The #define directive is used in the following two ways:

- To define a variable holding a constant value
- To define a function constant

The two syntaxes to use the # define directive are:

```cpp
#define <macro/constant name> < value> // defining constant variable/macro
#define < func_name () > < func_val> // function constant/macro
```

In the first syntax, macro/constant name can be any logical variable name to be used as a constant or macro, and value can be any logical value assigned to the variable. An example of this can be #define PI 3.14. In this case, all occurrences of PI in the program are replaced with the value 3.14.

In the second syntax, func_name() is the function name whose macro has to be created, and func_val is the value to be assigned to the parameters passed in the function. For example, in #define radius (a) (PI *a*a), a will be replaced with the parameter passed in the function radius from a C++ program. Now, consider the following code snippet to understand the concept of function macro better:

```cpp
result = radius (a);
```

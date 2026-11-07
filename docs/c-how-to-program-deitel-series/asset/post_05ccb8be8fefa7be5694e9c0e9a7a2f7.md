
called *indirection*. Diagrams typically represent a pointer as an arrow from the variable that contains an address to the variable located at that address in memory.

![](img/b42ba5cd262b1358d16610173f975e4d_371_0.png)

**Fig. 8.1** | Directly and indirectly referencing a variable.

### Declaring Pointers

Pointers, like any other variables, must be declared before they can be used. For example, for the pointer countPtr in Fig. 8.1, the declaration

```cpp
int *countPtr, count;
```

declares the variable countPtr to be of type int * (i.e., a pointer to an int value) and is read (right to left), “countPtr is a pointer to an int.” Also, variable count in the preceding declaration is declared to be an int, not a pointer to an int. The `*` in the declaration applies only to countPtr. Each variable being declared as a pointer must be preceded by an asterisk (`*`). For example, the declaration

```cpp
double *xPtr, *yPtr;
```

indicates that both xPtr and yPtr are pointers to double values. When `*` appears in a declaration, it’s not an operator; rather, it indicates that the variable being declared is a pointer. Pointers can be declared to point to objects of *any* data type.

> **Common Programming Error 8.1**
>
> Assuming that the `*` used to declare a pointer distributes to all names in a declaration’s comma-separated list of variables can lead to errors. Each pointer must be declared with the `*` prefixed to the name (with or without spaces in between). Declaring only one variable per declaration helps avoid these types of errors and improves program reliability.

> **Good Programming Practice 8.1**
>
> Although it’s not a requirement, including the letters Ptr in a pointer variable name makes it clear that the variable is a pointer and that it must be handled accordingly.

### Initializing Pointers

Pointers should be initialized to `nullptr` (new in C++11) or an address of the corresponding type either when they’re declared or in an assignment. A pointer with the value `nullptr` “points to nothing” and is known as a null pointer. From this point forward, when we refer to a “null pointer” we mean a pointer with the value `nullptr`.

> **Error-Prevention Tip 8.1**
>
> Initialize all pointer variables pointing to unknown or uninitialized areas of memory.

### Null Pointers Prior to C++11

In earlier versions of C++, the value specified for a null pointer was 0 or NULL. NULL is defined in several standard library headers to represent the value 0. Initializing a pointer to NULL is equivalent to initializing a pointer to 0, but prior to C++11, 0 was used by convention. The value 0 is the only integer value that can be assigned directly to a pointer variable without first casting the integer to a pointer type.

## 8.3 Pointer Operators

### Address (&) Operator

The address operator (&) is a unary operator that obtains the memory address of its operand. For example, assuming the declarations

```cpp
int y = 5; // declare variable y
int *yPtr = nullptr; // declare pointer variable yPtr
```

the statement

```cpp
yPtr = &y; // assign address of y to yPtr
```

assigns the address of the variable y to pointer variable yPtr. Then variable yPtr is said to “point to” y. Now, yPtr indirectly references variable y’s value. The use of the & in the preceding statement is not the same as the use of the & in a reference variable declaration, which is always preceded by a data-type name. When declaring a reference, the & is part of the type. In an expression like &y, the & is the address operator.

Figure 8.2 shows a representation of memory after the preceding assignment. The “pointing relationship” is indicated by drawing an arrow from the box that represents the pointer yPtr in memory to the box that represents the variable y in memory.

Figure 8.3 shows another pointer representation in memory with integer variable y stored at memory location 600000 and pointer variable yPtr stored at location 500000. The operand of the address operator must be an lvalue—the address operator cannot be applied to constants or to expressions that result in temporary values (like the results of calculations).

![](img/b42ba5cd262b1358d16610173f975e4d_372_0.png)

**Fig. 8.2** | Graphical representation of a pointer pointing to a variable in memory.

![](img/b42ba5cd262b1358d16610173f975e4d_372_1.png)

**Fig. 8.3** | Representation of y and yPtr in memory.

### Indirection (\*) Operator

The unary `*` operator—commonly referred to as the indirection operator or dereferencing operator—returns an lvalue representing the object to which its pointer operand points. For example (referring again to Fig. 8.2), the statement

```text
The address of a is 002DFD80
The value of aPtr is 002DFD80

The value of a is 7
The value of *aPtr is 7
```

**Fig. 8.4** | Pointer operators & and *. (Part 2 of 2.)

### Precedence and Associativity of the Operators Discussed So Far

Figure 8.5 lists the precedence and associativity of the operators introduced to this point. The address operator (&) and the dereferencing operator (`*`) are *unary operators* on the fourth level.

| Operators | Associativity | Type |
|---|---|---|
| `::` `()` | left to right | primary |
| `[]` `()` `++` `--` `.` `->` `static_cast<type>(operand)` | left to right | postfix |
| `++` `--` `+` `-` `!` `&` `*` `(type)` `sizeof` | right to left | unary (prefix) |
| `*` `/` `%` | left to right | multiplicative |
| `+` `-` | left to right | additive |
| `<<` `>>` | left to right | insertion/extraction |
| `<` `<=` `>` `>=` | left to right | relational |
| `==` `!=` | left to right | equality |
| `&&` | left to right | logical AND |
| `||` | left to right | logical OR |
| `?:` | right to left | conditional |
| `=` `+=` `-=` `*=` `/=` `%=` | right to left | assignment |
| `,` | left to right | comma |

*See caution in Fig. 2.10 regarding grouping parentheses.*

**Fig. 8.5** | Operator precedence and associativity of the operators discussed so far.

## 8.4 Pass-by-Reference with Pointers

There are three ways in C++ to pass arguments to a function—pass-by-value, pass-by-reference with reference arguments and pass-by-reference with pointer arguments. Chapter 6 compared and contrasted pass-by-reference with reference arguments and pass-by-value. Here, we explain pass-by-reference with pointer arguments.

Chapter 6 showed that the return statement can return *one value* from a called function or simply return *control*. You also learned that arguments can be passed to a function using reference parameters, which enable the called function to *modify the original values of the arguments in the caller*. Reference parameters also enable programs to pass *large data objects* to a function and avoid the overhead of passing the objects by value (which, of course, copies the object). Pointers, like references, also can be used to modify one or more variables in the caller or to pass pointers to large data objects to avoid the overhead of passing the objects by value.

You can use pointers and the indirection operator (`*`) to accomplish pass-by-reference (exactly as pass-by-reference is done in C programs—C does not have references). When calling a function with an argument that should be modified, the address of the argument is passed. This is normally accomplished by applying the address operator (&) to the name of the variable whose value will be modified.

### An Example of Pass-By-Value

Figure 8.6 and Fig. 8.7 present two versions of a function that cubes an integer. Figure 8.6 passes variable number by value (line 14) to function cubeByValue (lines 19–22), which cubes its argument and passes the new value back to main using a return statement (line 21). The new value is assigned to number (line 14) in main. The calling function has the opportunity to examine the function call’s result before modifying variable number’s value. For example, we could have stored the result of cubeByValue in another variable, examined its value and assigned the result to number only after determining that the returned value was reasonable.

```cpp
// Fig. 8.6: fig08_06.cpp
// Pass-by-value used to cube a variable’s value.
#include <iostream>
using namespace std;

int cubeByValue( int ); // prototype

int main()
{
   int number = 5;

   cout << "The original value of number is " << number;

   number = cubeByValue( number ); // pass number by value to cubeByValue
   cout << "\nThe new value of number is " << number << endl;
} // end main

// calculate and return cube of integer argument
int cubeByValue( int n )
{
   return n * n * n; // cube local variable n and return result
} // end function cubeByValue
```

```text
The original value of number is 5
The new value of number is 125
```

**Fig. 8.6** | Pass-by-value used to cube a variable’s value.

### An Example of Pass-By-Reference with Pointers

Figure 8.7 passes the variable number to function cubeByReference using pass-by-reference with a pointer argument (line 15)—the address of number is passed to the function. Function cubeByReference (lines 21–24) specifies parameter nPtr (a pointer to int) to receive its argument. The function uses the dereferenced pointer to cube the value to which nPtr points (line 23). This directly changes the value of number in main (line 11). Line 23 is equivalent to

```cpp
*nPtr = (*nPtr) * (*nPtr) * (*nPtr); // cube *nPtr
```


## Table 4.6 Default values of variables

| TYPE | DEFAULT VALUE |
|---|---|
| All integer types | 0 |
| char type | '\x0000' |
| float type | 0.0f |
| double type | 0.0d |
| decimal type | 0.0m |
| bool type | false |
| enum type | 0 |
| All reference types | null |

## 4.10 CONSTANT VARIABLES

The variables whose values do not change during the execution of a program are known as constants. For example, the variables representing the maximum number of rows and columns of a matrix or number of students in a class in a program may not change during execution of the program. Such variables can be made unmodifiable by using the const keyword while initializing them.

Example:

```
const int ROWS = 10;
const int COLS = 20;
const int NUM = 90;
```

Remember, constants must be declared and initialized simultaneously as shown above. For instance,

```
const int m;
m = 100;
```

is illegal. By definition, a constant cannot have its value changed later.

A constant variable can be initialized using an expression.

Example:

```
const int m = 10;
const int n = m * 5;
```

Remember, we cannot use non-const values in expressions. For instance,

```
int m = 10;        // non-constant value
const int n = m * 5;   // error
```

will result in an error.

In C and C++, such constants are known as symbolic constants and are defined using the #define statement. They are not declared for types.

Advantages of using constants are:

- They make our programs easier to read and understand.
- They make our programs easier to modify.
- They minimize accidental errors, like attempting to assign values to some variables which are expected to be constants.

Note:

- 1. The names of constant take the same form as variable names.
- 2. After declaration of constants, they should not be assigned any other value.

## SCOPE OF VARIABLES

The scope of a variable is the region of code within which the variable can be accessed. This depends on the type of the variable and place of its declaration. C# defines several categories of variables. They include:

- Static variables
- Instance variables
- Array elements
- Value parameters
- Reference parameters
- Output parameters
- Local variables

```
class ABC
{
	static int m;
	int n;
	void fun(int x, ref int y, out int z, int [] a)
	{
		int j = 10;
		....
		....
	}
}
```

- m as a static variable
- n as an instance variable
- x as a value parameter
- y as a reference parameter
- z as an output parameter
- a[0] as an array element
- j as a local variable

Static and instance variables are declared at the class level and are known as field or field variables. The scope of these variables begins at the place of their declaration and ends when the Main method terminates.

The variables x, y and z are parameters of the method fun(). The value parameter x will exist till the end of the method. The reference and output parameters (y and z) do not have their own storage locations. Instead, they represent the same storage locations as the variables that are passed as arguments. The scope of these variables is always the same as the underlying variables.

The elements of an array such as a[0] come into existence when an array instance is created, and cease to exist when there are no references to that array instance. Arrays declared at class level behave like fields.

Variables declared inside methods are called local variables. They are called so because they are not available for use outside the method definition. Local variables can also be declared inside program

This program when executed will produce the following output:

```
100
200
10
20
```

Although we have declared two variables named x and two variables named y, the code will compile and produce the output. In this case, the variables declared inside the Main method hide the class-level variables with the same name. Note that we have used the dot operator with the class name to access the static variable y and with the keyword this to access the instance variable x. More about static and instance variables will be considered later while discussing classes.

Let us consider another example code as shown below:

```
using System;
class Scope
{
    public static void Main()
    {
        int m=100;
        for (int i=0; i<=4; i++)
        {
            int m=200; // Error
            Console.WriteLine (m*i); //ok m = 100
        }
    }
}
```

This code will not compile because the compiler cannot understand the statement.

```
int m=200;
```

placed inside the for loop. The variable m defined before the for loop statement is still in scope inside the for loop and goes out of scope only when the Main has finished executing. If we delete the statement

```
int m = 100;
```

then the program will compile and produce the following output:

```
0
100
200
300
400
```

## 4.12 BOXING AND UNBOXING

In object-oriented programming, methods are invoked using objects. Since value types such as int and long are not objects, we cannot use them to call methods. C# enables us to achieve this through a technique known as boxing. Boxing means the conversion of a value type on the stack to an object type on the heap. Conversely, the conversion from an object type back to a value type is known as unboxing.

### 4.12.1 Boxing

Any type, value or reference can be assigned to an object without an explicit conversion. When the compiler finds a value type where it needs a reference type, it creates an object ‘box’ into which it places the value of the value type. The following code illustrates this:

```
int m = 100;
object om = m; // creates a box to hold m
```

When executed, this code creates a temporary reference_type ‘box’ for the object on heap. We can also use a C-style cast for boxing.

```
int m = 100;
object om = (object)m; //C-style casting
```

Note that the boxing operation creates a copy of the value of the m integer to the object om. Now both the variables m and om exist but the value of om resides on the heap. This means that the values are independent of each other. Consider the following code:

```
int m = 10;
object om = m;
m = 20;
Console.WriteLine(m); // m = 20
Console.WriteLine(om); //om = 10
```

When a code changes the value of m, the value of om is not affected.

### 4.12.2 Unboxing

Unboxing is the process of converting the object type back to the value type. Remember that we can only unbox a variable that has previously been boxed. In contrast to boxing, unboxing is an explicit operation using C-style casting.

```
int m = 10;
object om = m; //box m
int n = (int)om; //unbox om back to an int
```

When performing unboxing, C# checks that the value type we request is actually stored in the object under conversion. Only if it is, the value is unboxed.

When unboxing a value, we have to ensure that the value type is large enough to hold the value of the object. Otherwise, the operation may result in a runtime error. For example, the code

```
int m = 500;
object om = m;
byte n = (byte)om;
```

will produce a runtime error.

Notice that when unboxing, we need to use explicit cast. This is because in the case of unboxing, an object could be cast to any type. Therefore, the cast is necessary for the compiler to verify that it is valid as per the specified value type.

## Case Study

### Problem Statement

ForEx Enterprises is a medium sized organisation that is involved in the money exchange business. This means that the main function of ForEx is to convert the money of one currency to the money of another currency for its customers. ForEx Enterprises was started in 2000 and since then it has been manually calculating the value of foreign currency into domestic currency and vice versa. Manual calculation of money value in a specific currency is recently leading to the occurrence of a large number of errors. In addition, the staff of ForEx Enterprises is spending a lot of its time in the process of converting the currency value of a certain amount of money into another currency value. How can the management of ForEx Enterprises automate the task of converting the money value of a specific currency into the money value of another currency?

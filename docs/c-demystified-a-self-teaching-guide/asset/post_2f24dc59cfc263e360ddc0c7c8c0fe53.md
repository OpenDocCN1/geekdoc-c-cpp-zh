
For example, the following code outputs 0012FED4 on my computer. However, the particular memory address for testScore on your computer may be different than 0012FED4. Even, if I run this program again some later time, the particular memory address for testScore on my computer may be different from 0012FED4.

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int testScore;
    cout << &testScore;
    return 0;
}
```

The address 0012FED4 is a hexadecimal (Base 16) number. As discussed in Chapter 2, memory addresses are expressed as a hexadecimal number.

The operating system, by the programmer, chooses the address to store a variable. The particular address chosen by the operating system depends on the data type of the variable, how much memory has been reserved, and other factors.

You do not need to be concerned about how the operating system chooses since your code will refer to variable by its name, not its address. However, as you will learn in Chapter 11 when we discuss pointers, the address operator can be quite useful.

## Using the Address and sizeof Operators with Variables

The amount of memory reserved on a variable's data type. As you learned in Chapter 2, different data types have different sizes.

In Chapter 2, you use the sizeof operator to learn the size (on your compiler and operating system) of different types. You can also use the sizeof operator to determine the size (again, on your compiler and operating system) of different variables.

The syntax for using the sizeof operator to determine the size of a variable is almost the same as that for using the sizeof operator to determine the size of a data type. The only difference is that the parentheses following the sizeof refers to a variable name rather than a data type.

The following code outputs the address and size of two variables:

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    float testScore;
    cout << "The address of testScore is " << &testScore << "\n";
    cout << "The size of testScore is " << sizeof(testScore) << "\n";
    cout << "The address of myGPA is " << &myGPA << "\n";
    cout << "The size of myGPA is " << sizeof(myGPA) << "\n";
    return 0;
}
```

The output when I ran this program (yours may be different) is:

The address of testScore is 0012FED4

The size of testScore is 2

The address of myGPA is 0012FEC8

The size of myGPA is 4

Figure 3-1 shows how memory is reserved for the two variables. Due to the different size of the variables, the short variable, testScore, takes up two bytes of memory, and the float variable, myGPA, takes up four bytes of memory.

| float myGPA | short testScore |
|---|---|
| 0012FEC8 0012FEC9 0012FECA 0012FEFB | 0012FED4 0012FED5 |

**Figure 3-1:** Memory reserved for declared variables

As Figure 3-1 depicts, the addresses of the two variables are near each other. The operating system often attempts to do this. However, this is not always possible, depending on factors such as the size of the variables and memory already reserved. There is no guarantee that two variables will even be near each other in memory.

In Figure 3-1, the value for both memory addresses is unknown. That is we have not yet specified the values to be stored in those memory locations. The next section shows you how to do this.

![](img/59a3417a6d5906fae6d8000d4c2cff76_59_0.png)

## Assigning Values to Variables

The purpose of a variable is to store information. Therefore, after you have created a variable, the next logical step is to specify the information that the variable will store. This is called assigning a value to a variable.

A variable can be assigned a value supplied by the programmer in code. A variable also can be assigned a value by the user, usually via the keyboard, when the program is running.

You may use the assignment operator, which is discussed in the next section, to specify the value to be stored in a variable. You use the cin object (discussed in the upcoming section "Using the cin Object") after the assignment operator, to obtain the user's input, usually from the keyboard, and then insert that input in a variable.

## Assignment Operator

You use the assignment operator to assign a value to a variable. The syntax is `[variable name] = [value];`

The assignment operator looks like the equal sign. However, in C++ the sign is not used to test for equality; it is used for assignment. As you learn in Chapter 5 in C++ the equal sign is ==, also called the equality operator.

The variable must be declared either before, or at the same time, you assign it a value, not afterwards. In the following example, the first statement declares the variable, and the second statement assigns a value to that variable:

```cpp
int testScore;
testScore = 95;
```

The next example concerns initialization, which is when you assign a value to a variable as part of the statement that declares that variable:

```cpp
int testScore = 95;
```

However, the variable cannot be declared after you assign it a value. The following code will cause the compiler error "undeclared identifier" at the line testScore = 95:

```cpp
testScore = 95;
testScore;
```

As mentioned earlier in the "Declaring Variables", this error will occur even though the variable is declared in the next line because the compiler reads the code from top to bottom, so when it reaches the line testScore = 95, it has not seen the variable declaration.

The value assigned need not be a literal value, such as 95. The following code assigns to one integer variable the value of another integer:

```cpp
int a, b;
a = 44;
b = a;
```

The assignment takes place in two steps:

- First, the value 44 is assigned to the variable a.
- Second, the value of a, which now is 44, is assigned to the variable b.

You can also assign a value to several variables at once. The following code assigns 0 to three variables:

```cpp
int a, b, c;
a = b = c = 0;
```

[...Rest of text is corrupted/unreadable in source...]

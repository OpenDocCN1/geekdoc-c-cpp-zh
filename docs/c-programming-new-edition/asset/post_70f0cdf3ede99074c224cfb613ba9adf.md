
Well, it doesn’t understand anything unless you tell it, folks! So now how do you tell it? To specify to the computer what type you want to store, you specify the data type (i.e., `int` for integer, `float` for numbers with decimal point, and `char` for character) just before the variable name.

Take a look below:

```c
int e_sal; float da; char e_name;
```

Here `e_sal`, `da`, `e_name` are the different variable names. Though the programmer decides the variable names, it is always preferable to use meaningful variable names. For example, in the above example, `e_sal` means employee salary, `da` means dearness allowance, and `e_name` means employee name.

## 2.4. Type Declaration

One may tend to consider type declarations to be just another drop in the vast ocean of C’s technical jargon and tend to turn a blind eye towards it, but it doesn’t happen to be so. You are aware that C uses variables (a, b, x, y, and so on). These variables can be assigned to any one of the data types, i.e., the variable can be assigned to store an integer number or a floating point number (a number with decimals, in case you forgot) or a character.

This assignment of a data type to the variable is called type declaration. Type declaration has to be done at the beginning of the program right after the opening braces. The process of type declaration makes programming in C very uncomplicated because once the variable is declared at the beginning, the same variable can be used any number of times in the program and each time its data type will be the same as that declared in the beginning.

- **Example 2.2:** Presume that `x` is a variable and it has been assigned the data type `int`. This means that the variable `x` can store only integer numbers throughout the program anywhere it is called. `int sal;` If there is more than one variable to which the same data type has to be assigned, it can be done by making it succeed the data type instead of prefixing the data type name before all the variables.

For example:

```c
int sno, cno, hno; float sal, id; char sname, cname;
```

There are a few rules that have to be observed while exercising the task of type declaration.

### 2.4.1. Rules for Type Declaration

- All data types are keywords and they should always be written in lower case and they cannot be used as a variable name or for any other purpose (refer to the rules).
- The data types should be written as depicted above and not in their full form, i.e., `int` cannot be written as `integer`.
- All declarations should be performed before the first executable statement.
- All declarations must end with a semicolon.

## 2.5. Output Function

The formatted output function used in C is the `printf()`. The purpose of this function is to display the output desired by the user. To do so, the desired characters are written within the inverted quotations.

For example:

```c
printf("Welcome in Dharm's World \n");
```

The above function when inserted in a C program displays the message that is within the quotations. The message within the quotations is displayed as it is and it does not affect the program even a wee bit.

The `\n` makes the cursor skip to the next line. Another function of the print statement is that it can be used to ask the user to enter data for the program, which will be used for computation in the program. Say two numbers have to be added and the two values are to be requested from the user using the keyboard. Then the request for the two values is made in the following fashion, e.g.:

```c
printf("enter the value for x: ");
printf("enter the value for y: ");
```

The entered values are then accepted by the computer in a manner that will be discussed later during the session.

## 2.6. The Input Function and Format Specifiers

In your first encounter with a simple C program you stumbled upon the output function which is the `printf()`. Now you have to make way for the input function, which is called the `scanf()` function. You already know that the `printf()` can be used to request data from the user through the keyboard.

Everything’s fine till now, but who is going to accept the entered characters? The `scanf()` does. How it does is rather an intriguing fact, which will surely keep you spellbound (if not confused). What happens is that the `scanf()` uses something called the format specifiers, which aid it in the input proceedings. The format specifiers are special symbols allotted to the different data types. These format specifiers are mentioned in the parentheses of the `scanf()` based on the data type assigned to the variable in the beginning. Also, in the parentheses is mentioned the variable name preceded by an `&` symbol (Figure 2.2).

| Functions | Description |
|-----------|-------------|
| `scanf()` | This function is used to read one or multiple inputs from the user at the console. |
| `sscanf()` | This function is used to read the characters from a string and stores them in variables. |
| `printf()` | This function is used to display one or multiple values in the output to the user at the console. |
| `sprintf()` | This function is used to read the values stored in different variables and store these values in a character array. |

*Figure 2.2. Basic function in C programming.*

The variable name is preceded by an `&` symbol. It looks something like this:

```c
printf("enter the customer number:");
scanf("%d", &cno);
```

Here `%d` is the format specifier for an integer.

All format specifiers must be enclosed within quotations. `&` is the mandatory symbol and `cno` is the variable name which holds an integer. As soon as the user inserts the values, the `scanf()` identifies to which data type the inserted character belongs and stores it in the memory in that location (i.e., in `int`, `char`, or `float`). Some of the symbols for their corresponding data types are tabulated below:

| Format specifier | Description |
|------------------|-------------|
| `%c` | Character |
| `%d`, `%i` | Signed decimal integers |
| `%f` | Decimal floating point |
| `%s` | String of characters |
| `%u` | Unsigned decimal integers |
| `%x` | Unsigned hexadecimal |
| `%p` | Displays a pointer |
| `%%` | Prints a `%` sign |

## 2.7. Operators in C

Now the time is ripe to learn operators in C. In your earlier endeavors on C you noted that C encompasses a variety of operators. You will concentrate on the basic building blocks of operators and throw some light on the other operators.

While performing the division operation, if the quotient is not a perfect number and has decimal points, the division is performed after terminating the decimal points (truncation). You shall now undertake some tailor-made examples that will help you understand the role of the operators in different data types.

- **Example 2.4:** Assume that `x` and `y` are two integers whose values are 9 and 4 respectively, then the application of the operators on these numbers will result in the following values.

```c
x + y = 13   x - y = 5   x * y = 36   x / y = 2   x % y = 1
```

## 2.8. Unary Operators

If the outlook of the name bewilders you, there’s no cause for panic. This is just another example that goes to prove that things that seem confounding are actually elementary. There are two basic unary operators: the increment operator (denoted as `++`) and the decrement operator (denoted as `--`). You must again be wondering what two addition signs or two subtraction signs do. Well, when the increment operator is prefixed to a variable which holds an integer, it increases the value of the number by one.

Similarly, the decrement operator decreases the value by one. To put it simply:

- **Example 2.5:** If you assign an integer `a` the value 3, then writing `++a` would be equivalent to writing it as `a = a + 1`. Therefore, the modified value of `a` would be 4. Similarly, `--a` would mean `a = a - 1` and its modified value would be 2. Another operator worth mentioning is the `sizeof` operator. As the name suggests, whenever this operator is prefixed to the operand, the size of the operand in bytes is returned.

Assume that `x` is an integer and `y` is a floating point number, then the size of `x` and `y` can be determined as follows:

```c
#include<stdio.h>
void main()
{
    int x;
    float y;
    printf("integer: %d", sizeof x);
    printf("float: %d", sizeof y);
}
```

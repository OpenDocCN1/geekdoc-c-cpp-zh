
```
}
```

Negative three billion is too large for 32-bit integers, however, and the program's output is obviously wrong:

```
1294967296
```

The number printed was not even negative! Most C++ compilers will issue a warning about this statement. Section 4.6 explores errors vs. warnings in more detail. If the compiler finds an error in the source, it will not generate the executable code. A warning indicates a potential problem and does not stop the compiler from producing an executable program. Here we see that the programmer should heed this warning because the program's execution produces meaningless output.

This limited range of values is common among programming languages since each number is stored in a fixed amount of memory. Larger numbers require more storage in memory. In order to model the infinite set of mathematical integers an infinite amount of memory would be needed! As we will see later, C++ supports an integer type with a greater range. Section 4.8.1 provides some details about the implementation of C++ integers.

## 3.2 Variables and Assignment

In algebra, variables are used to represent numbers. The same is true in C++, except C++ variables also can represent values other than numbers. Listing 3.4 (variable.cpp) uses a variable to store an integer value and then prints the value of the variable.

### Listing 3.4: variable.cpp

```
#include <iostream>
int main() {
  int x;
  x = 10;
  std::cout << x << '\n';
}
```

The main function in Listing 3.4 (variable.cpp) contains three statements:

- int x;

This is a declaration statement. All variables in a C++ program must be declared. A declaration specifies the type of a variable. The word int indicates that the variable is an integer. The name of the integer variable is x. We say that variable x has type int. C++ supports types other than integers, and some types require more or less space in the computer's memory. The compiler uses the declaration to reserve the proper amount of memory to store the variable's value. The declaration enables the compiler to verify the programmer is using the variable properly within the program; for example, we will see that integers can be added together just like in mathematics. For some other data types, however, addition is not possible and so is not allowed. The compiler can ensure that a variable involved in an addition operation is compatible with addition. It can report an error if it is not.

The compiler will issue an error if a programmer attempts to use an undeclared variable. The compiler cannot deduce the storage requirements and cannot verify the variable's proper usage if it is not declared. Once declared, a particular variable cannot be redeclared in the same context. A variable may not change its type during its lifetime.

- x = 10;

This is an assignment statement. An assignment statement associates a value with a variable. The key to an assignment statement is symbol = which is known as the assignment operator. Here the value 10 is being assigned to the variable x. This means the value 10 will be stored in the memory location the compiler has reserved for the variable named x. We need not be concerned about where the variable is stored in memory; the compiler takes care of that detail.

After we declare a variable we may assign and reassign it as often as necessary.

- std::cout << x << '\n';

This statement prints the variable x's current value.

> Note that the lack of quotation marks here is very important. If x has the value 10, the statement
> std::cout << x << '\n';
> prints 10, the value of the variable x, but the statement
> std::cout << "x" << '\n';
> prints x, the message containing the single letter x.

The meaning of the assignment operator (=) is different from equality in mathematics. In mathematics, = asserts that the expression on its left is equal to the expression on its right. In C++, = makes the variable on its left take on the value of the expression on its right. It is best to read x = 5 as "x is assigned the value 5," or "x gets the value 5." This distinction is important since in mathematics equality is symmetric: if x = 5, we know 5 = x. In C++, this symmetry does not exist; the statement

```
5 = x;
```

attempts to reassign the value of the literal integer 5, but this cannot be done, because 5 is always 5 and cannot be changed. Such a statement will produce a compiler error:

```
error C2106: '=' : left operand must be l-value
```

Variables can be reassigned different values as needed, as Listing 3.5 (multipleassignment.cpp) shows.

### Listing 3.5: multipleassignment.cpp

```
#include <iostream>

int main() {
    int x;
    x = 10;
    std::cout << x << '\n';
    x = 20;
    std::cout << x << '\n';
    x = 30;
    std::cout << x << '\n';
}
```

Observe that each print statement in Listing 3.5 (multipleassignment.cpp) is identical, but when the program runs the print statements produce different results.

A variable may be given a value at the time of its declaration; for example, Listing 3.6 (variable-init.cpp) is a variation of Listing 3.4 (variable.cpp).

### Listing 3.6: variable-init.cpp

```
#include <iostream>

int main() {
    int x = 10;
    std::cout << x << '\n';
}
```

Notice that in Listing 3.6 (variable-init.cpp) the declaration and assignment of the variable x is performed in one statement instead of two. This combined declaration and immediate assignment is called initialization.

C++ supports another syntax for initializing variables as shown in Listing 3.7 (alt-variable-init.cpp).

### Listing 3.7: alt-variable-init.cpp

```
#include <iostream>

int main() {
    int x{10};
    std::cout << x << '\n';
}
```

This alternate form is not commonly used for simple variables, but it is necessary for initializing more complicated kinds of variables called objects. We introduce objects in Chapter 13 and Chapter 14.

Multiple variables of the same type can be declared and, if desired, initialized in a single statement. The following statements declare three variables in one declaration statement:

```
int x, y, z;
```

The following statement declares three integer variables and initializes two of them:

```
int x = 0, y, z = 5;
```

Here y's value is undefined. The declarations may be split up into multiple declaration statements:

```
int x = 0;
int y;
int z = 5;
```

In the case of multiple declaration statements the type name (here int) must appear in each statement.

The compiler maps a variable to a location in the computer's memory. We can visualize a variable and its corresponding memory location as a box as shown in Figure 3.1.

We name the box with the variable's name. Figure 3.2 shows how the following sequence of C++ code affects memory.

```
int a, b;
a = 2;
```

### Figure 3.1 Representing a variable and its memory location as a box

![](img/e84ad11adb18201d71595b31ce6c9eff_32_0.png)

```
b = 5;
a = b;
b = 4;
```

Importantly, the statement

```
a = b;
```

does not mean a and b refer to the same box (memory location). After this statement a and b still refer to separate boxes (memory locations). It simply means the value stored in b's box (memory location) has been copied to a's box (memory location). a and b remain distinct boxes (memory locations). The original value found in a's box is overwritten when the contents of b's box are copied into a. After the assignment of b to a, the reassignment of b to 4 does not affect a.

## 3.3 Identifiers

While mathematicians are content with giving their variables one-letter names like x, programmers should use longer, more descriptive variable names. Names such as altitude, sum, and user_name are much better than the equally permissible a, s, and u. A variable's name should be related to its purpose within the program. Good variable names make programs more readable by humans. Since programs often contain many variables, well-chosen variable names can render an otherwise obscure collection of symbols more understandable.

C++ has strict rules for variable names. A variable name is one example of an identifier. An identifier is a word used to name things. One of the things an identifier can name is a variable. We will see in later chapters that identifiers name other things such as functions and classes. Identifiers have the following form:

- Identifiers must contain at least one character.

- The first character must be an alphabetic letter (upper or lower case) or the underscore

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz_
```

- The remaining characters (if any) may be alphabetic characters (upper or lower case), the underscore, or a digit

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz_0123456789
```

- No other characters (including spaces) are permitted in identifiers.

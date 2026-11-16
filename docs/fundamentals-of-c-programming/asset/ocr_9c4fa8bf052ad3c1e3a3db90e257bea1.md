```
}
```

Negative three billion is too large for 32-bit integers, however, and the program's output is obviously wrong:

```
1294967296
```

The number printed was not even negative! Most C++ compilers will issue a warning about this statement. Section 4.6 explores errors vs. warnings in more detail. If the compiler finds an error in the source, it will not generate the executable code. A warning indicates a potential problem and does not stop the compiler from producing an executable program. Here we see that the programmer should heed this warning because the program's execution produces meaningless output.

This limited range of values is common among programming languages since each number is stored in a fixed amount of memory. Larger numbers require more storage in memory. In order to model the infinite set of mathematical integers an infinite amount of memory would be needed! As we will see later, C++ supports an integer type with a greater range. Section 4.8.1 provides some details about the implementation of C++ integers.

# 3.2 Variables and Assignment

In algebra, variables are used to represent numbers. The same is true in C++, except C++ variables also can represent values other than numbers. Listing 3.4 (variable.cpp) uses a variable to store an integer value and then prints the value of the variable.

# Listing 3.4: variable.cpp

```
#include <iostream>
int main() {
  int x;
  x = 10;
  std::cout << x << '\n';
}
```

The main function in Listing 3.4 (variable.cpp) contains three statements:

+   * int x;

This is a declaration statement. All variables in a C++ program must be declared. A declaration specifies the type of a variable. The word int indicates that the variable is an integer. The name of the integer variable is x. We say that variable x has type int. C++ supports types other than integers, and some types require more or less space in the computer's memory. The compiler uses the declaration to reserve the proper amount of memory to store the variable's value. The declaration enables the compiler to verify the programmer is using the variable properly within the program; for example, we will see that integers can be added together just like in mathematics. For some other data types, however, addition is not possible and so is not allowed. The compiler can ensure that a variable involved in an addition operation is compatible with addition. It can report an error if it is not.

The compiler will issue an error if a programmer attempts to use an undeclared variable. The compiler cannot deduce the storage requirements and cannot verify the variable's proper usage if it not declared. Once declared, a particular variable cannot be redeclared in the same context. A variable may not change its type during its lifetime.
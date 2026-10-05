# 3.2 Variables and Assignment

In algebra, variables are used to represent numbers. The same is true in C++, except C++ variables also can represent values other than numbers. Listing 3.4 (variable.cpp) uses a variable to store an integer value and then prints the value of the variable.

```
Listing 3.4: variable.cpp
```cpp
#include <iostream>

using namespace std;

int main() {
    int x;
    x = 10;
    cout << x << endl;
}
```
```

The main function in Listing 3.4 (variable.cpp) contains three statements:

+   * int x;

This is a declaration statement. All variables in a C++ program must be declared. A declaration specifies the type of a variable. The word int indicates that the variable is the integer. The name of the integer is x. We variable x has type int. C++ supports types other than integer, and some types require more or less space in the computer's memory. The compiler uses the declaration to reserve the proper amount of memory to store the variable's value. Due to the compiler it can also check if the variable is being used properly; for example, we see that it can be added together like in mathematics. For some other types, however, addition is not possible and so is not allowed. The compiler can ensure that a variable in an addition is compatible with declaration. It can return an error if it is not.

The compiler will issue an error if a programmer attempts to use an undeclared variable. The compiler cannot deduce and verify the variable's usage if it not declared. Once declared, a particular variable cannot be recalculated in the same context. A variable cannot change its type during its lifetime.

+   * x = 10;

This is an assignment statement. An assignment statement associates a variable with a value. The key to the assignment statement is the symbol = which is known as the assignment operator. Here the value 10 is assigned to the variable x. This means the value 10 will be stored in the memory location for the variable named x. We need not be concerned about where the variable is stored in memory; the compiler takes care of that.

After we declare a variable we may assign and reassign it as often as necessary.

+   * cout << x << endl;

This statement prints the variable x's current value.
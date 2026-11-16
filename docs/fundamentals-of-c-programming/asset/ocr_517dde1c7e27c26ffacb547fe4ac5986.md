+   x = 10;

This is an assignment statement. An assignment statement associates a value with a variable. The key to an assignment statement is symbol = which is known as the assignment operator. Here the value 10 is being assigned to the variable x. This means the value 10 will be stored in the memory location the compiler has reserved for the variable named x. We need not be concerned about where the variable is stored in memory; the compiler takes care of that detail.

After we declare a variable we may assign and reassign it as often as necessary.

+   std::cout << x << '\n';

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

# Listing 3.5: multipleassignment.cpp

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
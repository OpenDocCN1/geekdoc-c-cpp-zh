# 88 Introduction to C++

Note: The right parenthesis (")") means that the right number is not included in the indicated set."

```
#include <iostream>
int main() {
    float grd;

    std::cout << "Enter grade: ";
    std::cin >> grd;
    std::cout << ((grd >= 7.5 && grd <= 10) ? "A" : (grd >= 5 && grd < 7.5) ? "b" : (grd >= 0 && grd < 5) ? "Next time" : "Wrong input") << '\n';
    return 0;
}
```

# THE SWITCH STATEMENT

The switch statement can be used as an alternative to an if-else-if series, when we want to test the value of an expression against a series of values and handle each case differently. In the most common case, or at least the one I prefer, the syntax of the switch statement is:

```
switch(expression) {
    case constant_l:
        /* block of statements that will be executed if the value of the expression is equal to constant_l. */
        break;
        ...
    case constant_n:
        /* block of statements that will be executed if the value of the expression is equal to constant_n. */
        break;
    default:
        /* block of statements that will be executed if the expression is other than the previous constants. */
        break;
}
```

As a matter of style, there are several ways to write the switch statement. The most popular is to put the statements under the case label and the break statement with some space(s)inner or aligned with the statements. My preference is to align break with the case label and leave a space between each case and the preceding break. expression must be of an integral type (e.g., an integer variable or expression), or be a class type that provides an unambiguous conversion to integral type and the values of all constant_l, ..., constant_n must be integer constant expressions (e.g., 30 is a constant expression, and 30+40 as well) with different values. That is, you are not allowed to write:

```
double i, j;
const int c = 10;
```
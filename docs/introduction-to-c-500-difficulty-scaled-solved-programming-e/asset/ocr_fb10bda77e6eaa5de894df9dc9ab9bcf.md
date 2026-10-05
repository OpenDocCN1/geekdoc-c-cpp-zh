# Introduction to C++

For example, the following program uses the sizeof operator to display how many bytes allocate memory for the variables of the program:

```
int main() {

    char c;
    int i;
    double d;

    std::cout << sizeof(c) << ' ' << sizeof(i) << ' ' << sizeof(d) << '\\n';

    return 0;
}
```

In my environment, the program displays: 1 4 8. Notice that if we declare another variable, e.g., int j, and write sizeof(i+j), the program will display 4, because the type of the expression is integer. If we write sizeof(i+d), the program will display 8, as we learned in Chapter 2, the type of expression is double.

Note that if the operand is a function (e.g., int) parentheses are required, but if it is a variable it is necessary. If you are not using parentheses the result of an expression such as sizeof*j is not clear. sizeof applies first and then the multiplication or the other round? Because you'll always know to use sizeof in expressions, as is to avoid problems, I won't give you the answer. If you intend to get the answer, consult the precedence in Annex A. Nevertheless, parentheses may give the wrong impression that the sizeof is a function. No, it is not a function, it is an operator.

The sizeof operator is particularly useful in writing portable code. For example, we will see in Chapter 7, in order to find the size of the memory that an array allocates, we write:

```
int arr[100];
int i = sizeof(arr);
```

Thus, we calculate the memory regardless of the system in which the program runs and the size of the int type. In the next chapters, we'll see its usefulness with other data types, such as structures.
The next one is a quite easy example to introduce you in the if-else statement. What does the following program output?

```
int main() {

    if(sizeof(int) > -1)
        std::cout << "Yes\\n";
    else
        std::cout << "No\\n";

    return 0;
}
```
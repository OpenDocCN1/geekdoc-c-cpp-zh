exists for the effective life of the program. This is not true for the variables used in get_int_range: temp, in_value, bad_entry, and the parameters first and last. These variables maintained by get_int_range appear automatically when get_int_range begins executing (the left end of its bar) and their space is released when get_int_range is finished (the right end of its bar). During the printing of a 3 x 3 table the program calls print_row three times, and for each call the function's parameters row and column and local variable col come to life and then disappear when the function returns.

# 9.5 Organizing Functions

The code we have seen so far provides a function definition before its invocation. Listing 9.19 (organization1.cpp) organizes its functions this way:

```
Listing 9.19: organization1.cpp
// Function definition precedes main where the function is called
#include <iostream>

int twice(int n) {
    return 2 * n;
}

int main() {
    std::cout << twice(5) << '\n';
}
```

When the compiler attempts to parse the following statement:

```
std::cout << twice(5) << '\n';
```

it needs to be able to determine if the expression twice(5) is valid in the given context; that is, it must determine if the expression twice(5) evaluates to something that can be sent to the std::cout object using the << operator. The following points are important in the parsing process:

+   • The earlier definition of the twice function declares the identifier twice to the compiler. Consequently the compiler expects a caller to twice to pass a single argument that is compatible with the int type. The compiler also knows that the call to twice will return an integer value.
+   • The parentheses after the name twice in the statement indicate the expression is a function call.
+   • Within the parentheses is the integer literal 5, which clearly is compatible with the int type.
+   • The expression twice(5) thus evaluates to an int, and the << operator can send integer values to the std::cout output stream object.

The compiler can verify that the code within the main function is using the twice function correctly.

If we instead place twice's definition after the main function's definition, the compiler will report an error where twice's call appears within main. This is because the compiler parses C++ source code line by line from top to bottom within the .cpp file. When the compiler sees the identifier twice first at its

[1] Technically, the run-time environment does not allocate the space for a local variable until after its point of declaration. For variables declared within blocks, like temp with the if body, the variable is discarded at the end of the block's execution.
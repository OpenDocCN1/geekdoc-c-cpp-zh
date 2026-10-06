can be accessed from any compilation unit in the program; these have external linkage.
Static linkage is ideal for helper functions and internal variables that should not be used in other compilation units. It reduces the risks of having colliding identifiers (global variables with the same name or global functions with the same signature in different compilation units) and prevents malicious or otherwise ill-used users from accessing the internals of a compilation unit.

Let's now look at the second file, main.cpp, which uses the two global variables declared with external linkage in random.cpp:

```
#include <iostream>

extern int randomNumbers[128];

void populateRandomArray();

int main() {
    populateRandomArray();
    for (int i = 0; i < 128; ++i)
        cout << randomNumbers[i] << std::endl;
    return 0;
}
```

We declare the external variables and functions before we call them. The external variable declaration (which makes an external variable in the current compilation unit) for randomNumbers starts with the extern keyword. Without extern, the compiler would think it has to deal with a variable definition, and the linker would complain because the same variable is defined in two compilation units (random.cpp and main.cpp). Variables can be declared as many times as we want, but be defined only once. The definition is what causes the compiler to reserve space for the variable.

The populateRandomArray() function is declared using a function prototype. The extern keyword is optional for functions.

Typically, we would put the external variable and function declarations in a header file and include it in all the files that need them:

```
#ifndef RANDOM_H
#define RANDOM_H
extern int randomNumbers[128];

void populateRandomArray();
```
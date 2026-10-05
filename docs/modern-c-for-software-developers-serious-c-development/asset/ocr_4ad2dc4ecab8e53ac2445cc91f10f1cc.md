# Misc: How To Call A Function Before main

C and C++ programs start execution at the function main(). The following code will call the function func before main() is executed:

```
#include <iostream>
void func() { std::cout << "inside func" << std::endl; }

class Base {
public:
    Base() { func(); }
};

Base foo;

int main() {
    std::cout << "inside main" << std::endl;
    # output
    inside func
    inside main
```

The global variable foo will be initialized by the compiler before main is called.

We can also use a static global variable to call func before main:

```
#include <iostream>
int func() {
    std::cout << "in func" << std::endl;
    return 0;
}
static int foo = func();

int main() {
    std::cout << "in main" << std::endl;
    return 0;
}

# output
in func
in main
```

The compiler will initialize the global variable foo before calling main().
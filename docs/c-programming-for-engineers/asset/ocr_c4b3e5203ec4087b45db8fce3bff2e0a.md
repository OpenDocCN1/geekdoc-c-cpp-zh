# 32 Chapter 2. Problem Solving

other modules through clearly defined interfaces. The benefits of modularity include the following.

+   ** Reusability:** Modules can be reused in different parts of a program or even in different programs, reducing code duplication and development effort.
** Easier Maintenance:** Modular code is easier to maintain and update, as changes can be made to individual modules without affecting the rest of the system. This facilitates debugging and updating processes.
** Organization and Readability:** Modular code is more organized and easier to understand, as it breaks down complex functionality into smaller logical units.
** Improved Scalability:** Modular design allows for easier scaling of a system by adding or removing modules as needed.
** Team Collaboration:** Modularity facilitates collaboration among multiple programmers, as different team members can work on different modules concurrently.

In C, modularity is achieved by breaking a program into functions. Functions are defined with a return type, a name, optional parameters (also known as arguments), and a body containing the code to be executed. Functions are invoked or called by their name, and they can return a value to the caller if specified.

Let's look at an example of a simple function:

```
#include <stdio.h>

// Function declaration for a simple function
void greet() {
    printf("Hello, World!\n");
}

int main() {
    greet();      // Function call
    return 0;
}
```

Listing 2.5: https://onecompiler.com/c/426sbwcjc7

In this example, greet() prints "Hello, World!". We declare it using void because it doesn't return anything. Then, we call the function from main().nMany functions take inputs, perform calculations, and return results. Let us take a look at a parameterized function:

```
#include <stdio.h>
```

```
// Function declaration for a parameterized function
int add(int a, int b) {
    return a + b;
}

int main() {
```
# 10.3. Variable Scope and Storage Classes

The following code fixes this error:

```
#include <stdio.h>

void display() {
    int age = 19; // This variable is local to the display function
    printf("Age is %d\n", age);
}

int main() {
    display();
    return 0;
}
```

Variables have scope within any block of code, not just within functions. In the following program, the variable i only exists within the loop. Trying to access i outside the loop will cause a compilation error.

```
#include <stdio.h>

int main() {
    int sum = 0;

    for (int i=0; i<5; i++) {
        sum += i;
    }
    printf("i = %d, sum = %d\n", i, sum); // Compilation error

    return 0;
}
```

In summary, local variables can have block or function scope, meaning that they exist and can be used only within the blocks or functions where they are declared. Attempting to access them outside of these blocks would lead to compilation errors.

# Global Variables

Global variables, as the name suggests, can be accessed from any part of the program. They are declared outside of all functions. They are available throughout the program’s execution.

Excessive use of global variables is generally discouraged as it can lead to name conflicts, tight coupling between code sections, and difficulty maintaining and testing the program.

```
// Global variable declaration
int globalVar = 20;
```

```
void myFunction() {
```
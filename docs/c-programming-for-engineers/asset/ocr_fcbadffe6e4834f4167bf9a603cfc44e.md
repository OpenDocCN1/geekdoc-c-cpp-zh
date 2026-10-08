```
printf("%d\n", globalVar);
```

```
}
```

```
int main() {
```

```
{
```

```
  display();
```

```
  globalVar = 23; // changing the value of global variable from main
```

```
  → function
```

```
  display();
```

```
  return 0;
```

```
}
```

In this program, the variable globalVar is declared outside of any function, making it accessible from anywhere in the program.

Local variables promote modularity and information hiding, making code easier to understand and maintain. Global variables should be used sparingly as they can introduce dependencies and make your code less flexible and reusable.

In summary, variable scope and storage classes are separate but closely related concepts in C programming. The variable scope determines a variable's visibility, while the storage classes determine its lifetime and behavior across functions and blocks. Understanding these concepts is essential for writing efficient, maintainable, and portable C code.

# Static Variables

Static variables are a special type of variable that combine aspects of local and global variables. Like local variables, they exist throughout the program's execution, not just within a single function. Unlike global variables, they are declared within a function, limiting their visibility to that function (local scope).

Static variables are defined with the 'static' keyword in a function. Static variables can be used to implement counters, maintain historical data, and store persistent values within a function. Here's a simple C code demonstrating static variables:

```
#include <stdio.h>
```

```
void incrementCounter() {
  static int counter = 0; // Static variable initialization
  counter++;              // Increment count in each function
  printf("Counter: %d\n", counter);
}
```

```
int main() {
  // Calling the function to increment and print the counter
  incrementCounter();
  incrementCounter();
```
```
}
}
```

First, the variable a is declared. Then, inside the inner code block, b is declared. Then the inner code block terminates and b goes out of scope, then a goes out of scope. Therefore, the lifetime of b is entirely contained within the lifetime of a. The idea that you always de-allocate variables in the reverse order of how you allocate them is crucial to the way the stack works.

Note that b is in a different block from code (defined by a different nesting of curly braces). For this reason, it is contained within a different scope. This is termed as block scope or structure scope.

You do not know exactly where in the address space the stack is—you don’t need to know for C# development. A stack pointer (a variable maintained by the operating system) identifies the next free location on the stack. When your program first starts running, the stack pointer will point to just past the end of the block of memory that is reserved for the stack. The stack fills downward, from high memory addresses to low addresses. As data is put on the stack, the stack pointer is adjusted accordingly, so it always points to just past the next free location. This is illustrated in Figure 5.2, which shows a stack pointer with a value of 800000 (0xc3500 (in hex); the next free location is the address 799999.

![](bbox=[0.1, 0.47, 0.9, 0.76])

# Figure 5.2

The following code tells the compiler that you need space in memory to store an integer and a double, and these memory locations are referred to as nRacingCars and engineSize. The line that declares each variable indicates the point at which you start requiring access to this variable. The closing curly brace of the block in which the variables are declared identifies the point at which both variables go out of scope:

```
{
```
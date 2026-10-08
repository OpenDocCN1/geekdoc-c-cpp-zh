# 10.3. Variable Scope Storage Classes

+   - Finally, we define the addNumbers function below the main() function, which takes two integers and returns their sum.

In summary, function prototypes declare a function's signature without defining its implementation. They enable modular compilation, catch errors, and provide documentation for proper usage.

# 10.3 Variable Scope and Storage Classes

Variable scope and storage classes are related concepts in C programming, but serve different purposes.

# Scope

Scope defines the visibility of a variable - where in your program you can access and modify its value. The scope can be

+   - Local: Variables declared within a function or block are accessible only within that specific block or function.
- Global: Variables declared outside functions or with the "extern" keyword are accessible to all functions in the program.

# Storage Class

The storage class determines the lifetime (how long a variable exists in memory) and memory allocation (where in memory the variable is stored) of the variable. Storage classes in C influence scope to some extent, but they are not the same thing. Here are the common storage classes:

+   - auto (default): Local variables declared within functions or blocks. They are automatically created when the block or function is entered and are destroyed when it exits. Memory is allocated in the stack.
- register: Similar to auto, but the compiler tries to store them in CPU registers for faster access (if available). Their size depends on the specific processor's size.
- static: When a static variable is declared, it retains its value between function calls. It can be declared within a function or globally. They retain their value between function calls for local static variables and throughout the program. Memory is allocated in the data segment.
- extern: The "extern" keyword is used to declare a variable defined in another source file. It does not allocate memory, but tells the compiler about the variable's existence elsewhere.

The scope of variables defines where a variable can be used within a program, with the main types being local and global variables.
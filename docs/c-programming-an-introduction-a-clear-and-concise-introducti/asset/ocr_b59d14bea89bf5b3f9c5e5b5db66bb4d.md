programs.

+   - Ability to manage modularity – Code that makes heavy use of global variables is not as modular as code that uses more local variables.

The best advice is to start out making your variables local and then change them to global only when it is absolutely necessary. Later in this book we will discuss situations where using global variables is advantageous.

# Local Scope

We have already discussed how to create variables with *local scope* and will only review the concept here. Variables declared within the body of a function, including the main() function, are considered to have local scope. A variable with local scope has a lifetime that mirrors the lifetime of the function and any code defined in the body of the function that includes the declaration of the function has access to the variable.

# Block Scope

A variable that has *block scope* is accessible only to code found within the block of that variable. This may seem confusing since local variables are usually defined within a block, but there are many instances when there is a block of code within another block of code.

Consider the following simple for loop:
# Difference between Variable and Identifier

An Identifier is a name given to any variable, function, structure, pointer or any other entity in a programming language. A variable is a named memory location to store data which is used in the program.

| Identifier | Variable |
| --- | --- |
| Identifier is the name given to a variable, function, etc. | While, variable is used to name a memory location which stores data. |
| An identifier can be a variable, but not all identifiers are variables. | All variable names are identifiers. |

Example:

```
// a variable
intstudentight;;
or, a function
intstudentight() {
}
```

Example:
// int variable
int a;
// float variable
float a and b, i.e, float b,c;

Another great analogy to understand the difference between Identifier and Variable is:

You can think of an Identifier x to be a variable's name, but it can also be a function's name int() { } and still be an identifier.

Just like vasavi is a name of a person, but also the name of a foundation.

# Scope and Life of Variables in C

Lifetime: Lifetime of any variable is the time for which the particular variable outlives in memory during running of the program.

Scope: The scope of any variable is actually a subset of lifetime. A variable may be in the memory but may not be accessible though, the area of our program where we can actually access our variable is the scope of that variable.

The scope of any variable can be broadly categorized into three categories:

+   - Global scope: When variable is defined outside all functions. It is then available to all the functions of the program and all the blocks program contains.

+   - Local scope: When variable is defined inside a function or a block, then it is locally accessible within the block and hence it is a local variable.
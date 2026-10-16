lifetime of sum extends over the time during which printheader executes. Whatever storage location sum is bound to before the call to printheader, that binding will continue during and after the execution of printheader.

# 5.7 Referencing Environments

The referencing environment of a statement is the collection of all variables that are visible in the statement. The referencing environment of a statement in a static-scoped language is the variables declared in its local scope plus the collection of all variables of its ancestor scopes that are visible. In such a language, the referencing environment of a statement is needed while that statement is being compiled, so code and data structures can be created to allow references to variables from other scopes during run time. Techniques for implementing references to nonlocal variables in both static- and dynamic-scoped languages are discussed in Chapter 10.

In Python, scopes can be created by function definitions. The referencing environment of a statement includes the local variables, plus all of the variables declared in the functions in which the statement is nested (excluding variables in nonlocal scopes that are hidden by declarations in nearer functions). Each function definition creates a new scope and thus a new environment. Consider the following Python skeletal program:

```
g = 3; # A global

def sub1():
    a = 5; # Creates a local
    b = 7; # Creates another local
    ... <--------------------------- 1
def sub2():
global g;  # Global g is now assignable here
    c = 9;  # Creates a new local
    ... <--------------------------- 2
def sub3():
nonlocal c:  # Makes nonlocal c visible here
    g = 11; # Creates a new local
    ... <--------------------------- 3
```

The referencing environments of the indicated program points are as follows:

| Point | Referencing Environment |
| --- | --- |
| 1 | local a and b (of sub1), global g for reference, but not for assignment |
| 2 | local c (of sub2), global g for both reference and for assignment |
| 3 | nonlocal c (of sub2), local g (of sub3) |
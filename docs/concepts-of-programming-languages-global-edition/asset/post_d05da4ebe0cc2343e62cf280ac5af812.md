
lifetime of sum extends over the time during which printheader executes. Whatever storage location sum is bound to before the call to printheader, that binding will continue during and after the execution of printheader.

## 5.7 Referencing Environments

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

Now consider the variable declarations of this skeletal program. First, note that, although the scope of sub1 is at a higher level (it is less deeply nested) than sub3, the scope of sub1 is not a static ancestor of sub3, so sub3 does not have the access to the variables declared in sub1. There is a good reason for this. The variables declared in sub1 are stack dynamic, so they are not bound to storage if sub1 is not in execution. Because sub3 can be in execution when sub1 is not, it cannot be allowed to access variables in sub1, which would not necessarily be bound to storage during the execution of sub3.

A subprogram is active if its execution has begun but has not yet terminated. The referencing environment of a statement in a dynamically scoped language is the locally declared variables, plus the variables of all other subprograms that are currently active. Once again, some variables in active subprograms can be hidden from the referencing environment. Recent subprogram activations can have declarations for variables that hide variables with the same names in previous subprogram activations.

Consider the following example program. Assume that the only function calls are the following: main calls sub2, which calls sub1.

```
void sub1() {
int a, b;
. . . <--------------- 1
} /* end of sub1 */
void sub2() {
int b, c;
. . . <--------------- 2
sub1();
} /* end of sub2 */
void main() {
int c, d;
. . . <--------------- 3
sub2();
} /* end of main */
```

The referencing environments of the indicated program points are as follows:

| Point | Referencing Environment |
|-------|-------------------------|
| 1     | a and b of sub1, c of sub2, d of main, (c of main and b of sub2 are hidden) |
| 2     | b and c of sub2, d of main, (c of main is hidden) |
| 3     | c and d of main |

## 5.8 Named Constants

A named constant is a variable that is bound to a value only once. Named constants are useful as aids to readability and program reliability. Readability can be improved, for example, by using the name pi instead of the constant 3.14159265.

Another important use of named constants is to parameterize a program. For example, consider a program that processes a fixed number of data values, say 100. Such a program usually uses the constant 100 in a number of locations for declaring array subscript ranges and for loop control limits. Consider the following skeletal Java program segment:

```
void example() {
    int[] intList = new int[100];
    String[] strList = new String[100];
    ...
    for (index = 0; index < 100; index++) {
        ...
    }
    ...
    for (index = 0; index < 100; index++) {
        ...
    }
    ...
    average = sum / 100;
    ...
}
```

When this program must be modified to deal with a different number of data values, all occurrences of 100 must be found and changed. On a large program, this can be tedious and error prone. An easier and more reliable method is to use a named constant as a program parameter, as follows:

```
void example() {
    final int len = 100;
    int[] intList = new int[len];
    String[] strList = new String[len];
    ...
    for (index = 0; index < len; index++) {
        ...
    }
    ...
    for (index = 0; index < len; index++) {
        ...
    }
    ...
    average = sum / len;
    ...
}
```

Now, when the length must be changed, only one line must be changed (the variable len), regardless of the number of times it is used in the program. This is another example of the benefits of abstraction. The name len is an abstraction for the number of elements in some arrays and the number of iterations in some loops. This illustrates how named constants can aid modifiability.

C++ allows dynamic binding of values to named constants. This allows expressions containing variables to be assigned to constants in the declarations. For example, the C++ statement

```
const int result = 2 * width + 1;
```

declares result to be an integer type named constant whose value is set to the value of the expression 2 * width + 1, where the value of the variable width must be visible when result is allocated and bound to its value.

Java also allows dynamic binding of values to named constants. In Java, named constants are defined with the final reserved word (as in the earlier example). The initial value can be given in the declaration statement or in a subsequent assignment statement. The assigned value can be specified with any expression.

C# has two kinds of named constants: those defined with const and those defined with readonly. The const named constants, which are implicitly static, are statically bound to values; that is, they are bound to values at compile time, which means those values can be specified only with literals or other const members. The readonly named constants, which are dynamically bound to values, can be assigned in the declaration or with a static constructor.

So, if a program needs a constant-valued object whose value is the same on every use of the program, a const constant is used. However, if a program needs a constant-valued object whose value is determined only when the object is created and can be different for different executions of the program, then a readonly constant is used.

The discussion of binding values to named constants naturally leads to the topic of initialization, because binding a value to a named constant is the same process, except it is permanent.

In many instances, it is convenient for variables to have values before the code of the program or subprogram in which they are declared begins executing. The binding of a variable to a value at the time it is bound to storage is called initialization. If the variable is statically bound to storage, binding and initialization occur before run time. In these cases, the initial value must be specified as a literal or an expression whose only nonliteral operands are named constants that have already been defined. If the storage binding is dynamic, initialization is also dynamic and the initial values can be any expression.

In most languages, initialization is specified on the declaration that creates the variable. For example, in C++, we could have

```
int sum = 0;
int* ptrSum = &sum;
char name[] = "George Washington Carver";
```

```
Sum=30
Subtraction=20
```

In Program 1.9, the method set\_val() declared in the private section, and methods sum() and sub() are declared in the public section. The method sub() is defined outside the class that performs subtraction on a and b. The private method set\_val() is accessed by making a call to it in the public member function sum().

# 1.5 CLASS SCOPE

Identifiers such as variable name, function name, typedef in C++ can be used only in certain areas of a program. This area is called the “scope” of the identifier. Scope determines the lifetime and visibility of an identifier. It also determines whether the identifier clashes with another identifier in any other parts of the program. There are five kinds of scope.

+   a. Local scope: Variables declared within a function or blocks have local scope, i.e. they are accessed only within in that block. If the same variable is used in more than one function then each function, defines a new scope for it. Blocks can also be nested. A name declared in a block is local to that and to all the blocks contained in it. The formal arguments to a function will have local scope and are treated as if they belong to the outermost block.

```
{
 int i;
}
```

Here i has local scope, because it is declared inside a block enclosed by braces and it is never accessible since no code accesses it before closing the braces.

+   b. Function scope: Labels are those that have function scope and they can be accessed only within the function but not outside of that function.

+   c. File scope: When an identifier is not part of a function or class definition, then it is said to have file scope. File scope is the outermost scope in the program and it encloses both local and class scope. Variables defined at the file scope are called global variables.

+   d. Class scope: Every C++ class defines a unique scope for its members called the class scope, i.e. data members and member functions have class scope.

```
class A
{
 int a;
 public:
 void b();
}
```

Here the variable a and function b() must be accessed, so that the compiler determines its class. Accessing a class member is done in three ways:

+   i. Using (.dot) operator:
+   obj.a,
+   obj.b()
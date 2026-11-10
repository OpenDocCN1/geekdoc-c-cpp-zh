# **Declarations and Definitions**

The apparently similar terms "declaration" and "definition" for programming-language concepts are actually quite different. Declarations tell us about the types of things, while definitions tell us about their values. Thus, int i is a declaration of i, while i = 1 is a definition of i.

The difference is more significant when we deal with methods or other procedures. In C++, a method is declared in a class definition, by giving the types of the arguments and result of the method (often called the *signature* for the method). The method is then defined, i.e., the code for executing the method is given, in another place. Similarly, it is common to define a C function in one file and declare it in other files where the function is used.

**Example 1.7:** In the C program of Fig. 1.12, identify a as a macro that stands for expression (x + 1). But what is x? We cannot resolve x statically, that is, in terms of the program text.

```
```c
#define a (x+1)

int x = 2;

void b() { int x = 1; printf("%d\n", a); }

void c() { printf("%d\n", a); }

void main() { b(); c(); }
```
```

Figure 1.12: A macro whose names must be scoped dynamically

In fact, in order to interpret x, we must use the usual dynamic-scope rule. We examine all the function calls that are currently active, and we take the most recently called function that has a declaration of x. It is to this declaration that the use of x refers.

In the example of Fig. 1.12, the function *main* first calls function *b*. As *b* executes, it prints the value of the macro a. Since (x + 1) must be substituted for a, we resolve this use of x to the declaration int x=1 in function *b*. The reason is that *b* has a declaration of x, so the (x + 1) in the *printf* in *b* refers to this x. Thus, the value printed is 2.

After *b* finishes, and *c* is called, we again need to print the value of macro a. However, the only *x* accessible to *c* is the global *x*. The *printf* statement in *c* thus refers to this declaration of *x*, and value 3 is printed. □

Dynamic scope resolution is also essential for polymorphic procedures, those that have two or more definitions for the same name, depending only on the
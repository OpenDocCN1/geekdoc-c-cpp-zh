# # Chapter 8

# # Value Categories

This chapter introduces the formal terminology and rules for move semantics. We formally introduce value categories such as lvalue, rvalue, prvalue, and xvalue and discuss their role when binding references to objects. This allows us to also discuss details of the rule that move semantics is not automatically passed through, as well as a very subtle behavior of decltype when it is called for expressions.

This chapter is the most complicated chapter of the book. You will probably see facts and features that are tricky and for some people hard to believe. Come back to it later, whenever you read about value categories, binding references to objects, and decltype again.

# ## 8.1 Value Categories

To compile an expression or statement it does not only matter whether the involved types fit. For example, you cannot assign an int to an int when on the left-hand side of the assignment an int literal is used:

```
```cpp
int i = 42;
```
```

```
```cpp
i = 77;      // OK
77 = i;      // ERROR
```
```

For this reason, each expression in a C++ program has a *value category*. Besides the type, the value category is essential to decide what you can do with an expression.

However, value categories have changed over time in C++.

# ### 8.1.1 History of Value Categories

Historically (taken from Kernighan&Ritchie C, *K&R C*), we had only the value categories *lvalue* and *rvalue*. The terms came from what was allowed in an assignment:

+   - An *lvalue* could occur on the *left-hand* side of an assignment
+   - An *rvalue* could occur only on the *right-hand* side of an assignment

According to this definition, when you use an int object/variable you use an lvalue, but when you use an int literal you use an rvalue:
# # Chapter 7

# ## By Value or by Reference?

Since the beginning, C++ has provided call-by-value and call-by-reference, and it is not always easy to decide which one to choose. Usually calling by reference is cheaper for nontrivial objects but more complicated: C++11 added move semantics to the mix, which means that now you have different ways to pass by reference:

+   1. `X const&` (constant lvalue reference): The `X` parameter refers to the passed object, without the ability to modify it.
+   2. `X&` (nonconstant lvalue reference): The `X` parameter refers to the passed object, with the ability to modify it.
+   3. `X&&` (rvalue reference): The `X` parameter refers to the passed object, with move semantics, meaning that you can modify or “steal” the value.

Deciding how to declare parameters that know concrete types is complicated enough. In templates, suppose not know, and therefore `X` becomes even harder to decide which passing mechanism is appropriate.

Nevertheless, in Section 1.6.2, on page 20 we did recommend passing parameters in function templates by value unless there are good reasons, such as the following:

+   - Copying is not possible.
+   - Parameters are used to return data.
+   - Templates just forward the parameters to somewhere else by keeping all properties of the original arguments.
+   - There are significant performance improvements.

This chapter discusses the different approaches to declare parameters in template instantiating the overall recommendation to pass by value, and providing arguments for the reasons not to do so. It also discusses the tricky problems you run into when dealing with string literals and other raw arrays.

When reading this chapter, it is helpful to be familiar with the terminology of value categories (lvalue, rvalue, prvalue, xvalue), which is explained in Appendix B.

# ### 7.1 PASSING BY VALUE

When passing arguments by value, each argument must in principle be copied. Thus, each parameter becomes a copy of the passed argument. For classes, the object created as a copy generally is initialized by the copy constructor.

Calling a copy constructor can become expensive. However, there are various ways to avoid expensive copying even when passing parameters by value. In fact, compilers might optimize away copy operations giving objects and become cheap even for complex objects by using move semantics.

For example, let's look at a simple function template implemented so that the argument is passed by value:

Click here to view code image

```
template<typename T>
void printV(T arg) {
    // ...
}
```

When calling this function template for an integer, the resulting code is

Click here to view code image

```
void printV(int arg) {
    // ...
}
```

Parameter `arg` becomes a copy of any passed argument, whether it is an object or a literal as a value returned by a function.
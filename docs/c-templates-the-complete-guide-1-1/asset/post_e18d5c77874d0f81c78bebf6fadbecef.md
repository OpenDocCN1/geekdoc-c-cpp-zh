
## Chapter 7

### By Value or by Reference?

Since the beginning, C++ has provided call-by-value and call-by-reference, and it is not always easy to decide which one to choose. Usually calling by reference is cheaper for nontrivial objects but more complicated: C++11 added move semantics to the mix, which means that now you have different ways to pass by reference:

- 1. `X const&` (constant lvalue reference): The `X` parameter refers to the passed object, without the ability to modify it.
- 2. `X&` (nonconstant lvalue reference): The `X` parameter refers to the passed object, with the ability to modify it.
- 3. `X&&` (rvalue reference): The `X` parameter refers to the passed object, with move semantics, meaning that you can modify or “steal” the value.

Deciding how to declare parameters when you know concrete types is complicated enough. In templates, you do not know the concrete types, and therefore it becomes even harder to decide which passing mechanism is appropriate.

Nevertheless, in Section 1.6.2, on page 20 we did recommend passing parameters in function templates by value unless there are good reasons, such as the following:

- Copying is not possible.
- Parameters are used to return data.
- Templates just forward the parameters to somewhere else by keeping all properties of the original arguments.
- There are significant performance improvements.

This chapter discusses the different approaches to declare parameters in templates, instantiating the overall recommendation to pass by value, and providing arguments for the reasons not to do so. It also discusses the tricky problems you run into when dealing with string literals and other raw arrays.

When reading this chapter, it is helpful to be familiar with the terminology of value categories (lvalue, rvalue, prvalue, xvalue), which is explained in Appendix B.

### 7.1 Passing by Value

When passing arguments by value, each argument must in principle be copied. Thus, each parameter becomes a copy of the passed argument. For classes, the object created as a copy generally is initialized by the copy constructor.

Calling a copy constructor can become expensive. However, there are various ways to avoid expensive copying even when passing parameters by value. In fact, compilers might optimize away copy operations for temporary objects and become cheap even for complex objects by using move semantics.

For example, let's look at a simple function template implemented so that the argument is passed by value:

```cpp
template<typename T>
void printV(T arg) {
    // ...
}
```

When calling this function template for an integer, the resulting code is

```cpp
void printV(int arg) {
    // ...
}
```

Parameter `arg` becomes a copy of any passed argument, whether it is an object or a literal or a value returned by a function.

The template parameter `T` is instantiated as `std::string` so that we get

```cpp
void printV (std::string arg)
{
    ...
}
```

Again, when passing the string, `arg` becomes a copy of `s`. This time the copy is created by the copy constructor of the string class, which is a potentially expensive operation, because in principle this copy operation creates a full or "deep" copy so that the copy internally allocates its own memory to hold the value.

However, the potentially expensive copy constructor is not always called. Consider the following:

```cpp
std::string returnString();
std::string s = "hi";
printV(s);                         // copy constructor
printV(std::string("hi"));        // copying usually optimized
printV(std::move(s));              // move constructor
printV(returnString());            // copying usually optimized
printV(std::move(s));              // move constructor
```

In the first call we pass an lvalue, which means that the copy constructor is used. However, in the second and fourth calls, the temporaries passed directly to the function template are probably optimized away, and calling the function template for a temporary is turned into a call to the move constructor; see Appendix B. Compilers usually optimize passing the argument so that no copying is constructed at all. Since C++17, this optimization is required. Before C++17, a compiler that does not optimize the copying away must at least try to use move semantics, which usually makes copying cheap. In the last call, when passing an lvalue (an existing nonconstant object) with `std::move()`, we force the call to use the move constructor by signaling that we no longer need the value of `s`.

### Passing by Value versus Move

Thus, calling an rvalue or temporary by value we have to mention: When passing arguments to a parameter by value, the type decays. This means that arrays get converted to pointers and that qualifiers such as `const` and `volatile` are removed (just like using the value as initializer for an object declared without `&`).

```cpp
template<typename T>
void printV (T arg)
{
    ...
}
```

```cpp
std::string const c = "hi";
printV(c);                         // const removed so that arg has
                                   // type std::string

printV("hi");                      // decays to pointer so that
                                   // arg has type char const*

int arr[4];
printV(arr);                       // decays to pointer so that
                                   // arg has type int*
```

Thus, when passing the string literal `"hi"`, its type `char const[3]` decays to `char const*` so that this is the deduced type of `T`. Thus, the template is instantiated as follows:

```cpp
void printV (char const* arg)
{
    ...
}
```

This behavior is derived from C and has its benefits and drawbacks. Often it simplifies the handling of passed string literals, but the drawback is that inside `printV(T)` we can't distinguish between passing a pointer to a single element and passing a raw array. For this reason, we will discuss how to deal with string literals and other raw arrays in Section 7.2.4 on page 155.

### 7.2 Passing by Reference

Now let's discuss the different forms of passing by reference. In all cases, no copy gets created (because the parameter just refers to the passed argument). Also, passing the argument never decays. However, sometimes passing is not possible, and if passing is possible, there are some cases in which the resulting type of the parameter may cause problems.

### 7.2.1 Passing by Constant Reference

To avoid any (unnecessary) copying, when passing temporary objects, we can use constant references.

With this declaration, passing an object never creates a copy (whether it's cheap or not):

```cpp
std::string customString();
std::string s = "hi";
print(s);                         // no copy
print(customString());            // no copy
print(&s);                        // no copy
print(std::move(s));              // no copy
```

Even an `int` is passed by reference, which is a counterproductive but allowed way to pass that type:

```cpp
int i = 42;
print(i);                       // passes reference instead
```

results in `print()` being instantiated as:

```cpp
void print(int const& arg) {
    ...
}
```

Under the hood, passing an argument by reference is implemented by passing the address of the argument. Addresses are encoded compactly, and therefore transferring an address from the caller to the callee is efficient in itself. However, passing an address can create uncertainties for the compiler when it compiles the callee: What is the callee doing with that address? In theory, the callee can change all the values that are reachable through that address. That means that the compiler has to assume that all the values it may have reached (usually, in machine registers) are invalid after the call. Reloading all those values can be quite expensive. You may be thinking that we are passing by `const` reference: what the compiler deduces from that is that no change can happen! Unfortunately, this is not the case because the caller may have passed an object through its own non-`const` reference.

This can be improved by inlining: if the compiler can expand the call inline, it can reason about the caller and the callee together and in many cases “see” that the address is not used for anything but passing the underlying value. Function templates are often very short and therefore likely candidates for inline expansion. However, if a template encapsulates a more complex algorithm, inlining is less likely to happen.

### Passing by Reference Does Not Decay

When passing arguments to parameters by reference, they do not decay. This means that raw arrays are not converted to pointers and that qualifiers such as `const` and `volatile` are not removed. However, because the call parameter is declared as `T const&`, the template parameter `T` itself is not deduced as `const`. For example:

```cpp
template<typename T>
void print(T const& arg) {
    ...
}

std::string const c = "hi";
print(c);                           // T deduced as std::string, arg is
                                    // std::string const&

int arr[4];
print(arr);                         // T deduced as int[4], arg is
                                    // int const(&)[4]

int const a[4];
print(a);                           // T deduced as int[4], arg is
                                    // int const(&)[4]
```

Thus, local objects declared with type `T` in `print(T)` are not constant.

### 7.2.2 Passing by Nonconstant Reference

When you want to return values through passed arguments (i.e., when you want to use them as output parameters), you have to use nonconstant references (unless you prefer to pass them via pointers). Again, this means that when passing the arguments, no copy gets created. The parameters of the called function template just get direct access to the passed argument.

Consider the following:

```cpp
template<typename T>
void out(T& arg) {
    ...
}
```

Note that calling `out()` for a temporary (rvalue) or an existing object passed with `std::move()` (xvalue) usually is not allowed:

```cpp
std::string customString();
std::string s = "hi";
out(s);                         // ...
out(customString());             // ERROR: not allowed to pass a
                                 // temporary
```

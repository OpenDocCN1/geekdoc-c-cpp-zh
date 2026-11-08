# 23.1.1  Overloading

Strictly speaking, a function parameter consists of two parts: the *value* and its *type*. At runtime, you can call a function with different *values*: sometimes with 5, sometimes with 42, sometimes with -10. However, the *type* always remains the same.

A function where the type itself or variable is called a *function template*. Here, you must specify the type of a parameter in addition to its value when calling.

But first, let's consider a normal function like this:

```
```cpp
void print(int value) {
    cout << value;
}
```
```

You call it at runtime with the following:

```
```cpp
print(5);
print(42);
print(-10.25);
```
```

Here, the *value* of the parameter changes. Even if you pass a *double* value like in `print(-10.25)`, void `print(int)` is still called, and the parameter -10.25 is converted to an *int* value -10 for the call. So, for the last line, -10 would be output instead of -10.25.

This is not a problem for you, because you can write a function overload for the *double* type:

```
```cpp
void print(double value) {
    cout << value;
}
```
```

With this additional definition of `print(double)`, you also get the output -10.25. What do you get for the following line?

```
```cpp
print("Flamingo");
```
```

You get an error message stating that there is no suitable overload for `const char[]`. Said and done:

```
```cpp
void print(const char* value) {
    cout << value;
}
```
```

And now `print("Flamingo")`; works as well. But I’m starting to notice that the function body is always the same. It always says `{ cout << value; }`. If the program gets more types that you want to output to cout with `print()`, it becomes tedious. You also get a lot of code duplication, and you should avoid that.
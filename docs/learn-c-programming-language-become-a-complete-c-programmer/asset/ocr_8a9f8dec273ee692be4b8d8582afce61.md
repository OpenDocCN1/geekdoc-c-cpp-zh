```
```cpp
int a[max]; // error : arraybound not an integer
// ...
}
```
```

If **auto** causes surprises, the best cure is typically to make functions smaller, which most often is a good idea (§12.1).

We can decorate a deduced type with specifiers and modifiers (§6.3.1), such as **const** and **&** (reference; §7.7). For example:

```
```cpp
void f(vector<int>& v)
{
for (const auto& x : v) { // x is a const int&
// ...
}
}
```
```

Here, **auto** is determined by the element type of **v**, that is, **int**.

Note that the type of an expression is never a reference because references are implicitly dereferenced in expressions (§7.7). For example:

```
```cpp
void g(int& v)
{
auto x = v; // x is an int (not an int&)  auto& y = v; // y is an int&
}
```
```

# 6.3.6.2 auto and {}-lists

When we explicitly mention the type of an object we are initializing, we have two types to consider: the type of the object and the type of the initializer. For example:

```
```cpp
char v1 = 12345; // 12345 is an int
int v2 = 'c'; // 'c' is a char
T v3 = f();
```
```

By using the **{}**-initializer syntax for such definitions, we minimize the chances for unfortunate conversions:

```
```cpp
char v1 {12345}; // error : narrowing
int v2 {'c'}; // fine: implicit char->int conversion
T v3 {f()}; // worksfand only if the type of f() can be implicitly converted to a T
```
```

When we use **auto**, there is only one type involved, the type of the initializer, and we can safely use the **=** syntax:

```
```cpp
auto v1 = 12345; // v1 is an int
auto v2 = 'c'; // v2 is a char
auto v3 = f(); // v3 is of some appropriate type
```
```

In fact, it can be an advantage to use the **=** syntax with **auto**, because the **{}**-list syntax might surprise someone:

```
```cpp
auto v1 {12345}; // v1 is a list of int
auto v2 {'c'}; // v2 is a list of char
auto v3 {f()}; // v3 is a list of some appropriate type
```
```
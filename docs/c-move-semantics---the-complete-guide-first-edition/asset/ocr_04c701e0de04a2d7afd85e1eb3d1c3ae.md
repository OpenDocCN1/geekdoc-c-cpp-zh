# 10.1.2   Universal References in Detail

The previous example demonstrates that declaring an argument as a universal reference has more use than just perfectly forwarding it to another function. Let us analyze the mechanisms a little further.

Consider the following declaration:

```
```cpp
template<typename T>
void foo(T&& arg) {
    ...
}
```
```

When we declare arg, we have a reference that can bind universally to all types and value categories. For a non-const object v and a const object c the type T and the type of arg is deduced as follows:

|   | T | arg |
|---|---|---|
| `foo(v)` | `Type&` | `Type&` |
| `foo(c)` | `const Type&` | `const Type&` |
| `foo(Type&&)` | `Type` | `Type&&` |
| `foo(move(v))` | `Type` | `Type&&` |
| `foo(move(c))` | `const Type` | `const Type&&` |

That means that the information about the passed argument is split as follows:

+   - `arg` still knows the value and its value including whether or not it is const. It is an lvalue reference if an lvalue was passed and an rvalue reference if an rvalue was passed. `arg` also does know whether an lvalue or an rvalue was passed.
+   - `T` knows the type and has some information about the value category of the passed argument (whether an lvalue or rvalue was passed). According to a specific template type deduction rule, if an lvalue was passed, `T` is an lvalue reference; otherwise, `T` is not a reference.

Calling `std::forward<T>(arg)` brings all information together again to restore both constness and value category to perfectly forward the passed argument with its current value. However, if you do not need the value category of the passed argument for perfect forwarding, you do not need `std::forward<>`.

# Constness Dependent Code

If you only have to know whether the passed argument was const, you can use both arg and T. For example:

```
```cpp
template<typename T>
void foo(T&& arg)
{
    if constexpr(std::is_const_v<std::remove_reference_t<T>>) {
        ...    // passed argument is const
    }
    else {
        ...    // passed argument is not const
    }
}
```
```

Here, we use if constexpr (a compile-time if, introduced with C++17) to do different things depending on whether the passed argument is const.
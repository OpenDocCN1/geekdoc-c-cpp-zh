
## 8.4 左值何时变为右值

正如我们已经学到的，当函数声明了一个具体类型的右值引用参数时，你只能将这些参数绑定到右值。例如：

```
void rvFunc(std::string&&);    // forward declaration

std::string s{...};
rvFunc(s);                     // ERROR: passing an lvalue to an rvalue reference
rvFunc(std::move(s));          // OK, passing an xvalue
```

然而，请注意，有时传递左值似乎也能正常工作。例如：

```
void rvFunc(std::string&&);    // forward declaration

rvFunc("hello");              // OK, although "hello" is an lvalue
```

请记住，字符串字面量在作为表达式使用时是左值。因此，将它们传递给右值引用无法编译。然而，这里涉及一个隐藏的操作，因为实参的类型（六个常量字符组成的数组）与形参的类型不匹配。我们有一个由字符串构造函数执行的隐式类型转换，它会创建一个没有名字的临时对象。

因此，我们真正调用的是以下形式：

```
void rvFunc(std::string&&);    // forward declaration

rvFunc(std::string{"hello"});  // OK, "hello" converted to a string is a prvalue
```

## 8.5 右值何时变为左值

现在我们来看一个将形参声明为右值引用的函数的实现：

```
void rvFunc(std::string&& str) {
    ...
}
```

正如我们已经学到的，我们只能传递右值：

```
std::string s{...};
rvFunc(s);                     // ERROR: passing an lvalue to an rvalue reference
rvFunc(std::move(s));          // OK, passing an xvalue
rvFunc(std::string{"hello"}); // OK, passing a prvalue
```

然而，当我们在函数内部使用参数 str 时，我们处理的是一个有名字的对象。这意味着我们将 str 用作左值。我们只能做那些允许对左值做的事情。

这意味着我们不能直接递归调用我们自己的函数：

```
void rvFunc(std::string&& str) {
    rvFunc(str);                // ERROR: passing an lvalue to an rvalue reference
}
```

```
std::cout << std::is_reference<decltype(str)>::value;      // true
std::cout << std::is_lvalue_reference<decltype(str)>::value;  // false
std::cout << std::is_rvalue_reference<decltype(str)>::value;  // true
}
```

表达式 `decltype(str)` 始终产生 str 的类型，即 `std::string&&`。我们可以在表达式中任何需要此类型的地方使用它。类型萃取（type traits，例如 `std::is_same<>` 这样的类型函数）帮助我们处理这些类型。

例如，要声明一个传递参数类型的新对象，且该对象不是引用，我们可以这样声明：

```
void rvFunc(std::string&& str)
{
    std::remove_reference<decltype(str)>::type tmp;
    ...
}
```

在这个函数中，tmp 的类型是 `std::string`（我们也可以显式声明该类型，但如果我们将此函数做成针对类型 T 的对象的泛型函数，代码仍然可以正常工作）。

## 8.6.2 使用 decltype 检查值类别

到目前为止，我们只向 decltype 传递名字以查询其类型。然而，你也可以向 decltype 传递表达式（不仅仅是名字）。在这种情况下，decltype 还会根据以下约定给出值类别：

- 对于纯右值，它只给出其值的类型：type
- 对于左值，它给出其类型作为左值引用：type&
- 对于将亡值，它给出其类型作为右值引用：type&&

例如：

```
void rvFunc(std::string&& str)
{
    decltype(str + str)    // yields std::string because s+s is a prvalue
    decltype(str[0])       // yields char& because the index operator yields an lvalue
    ...
}
```

这意味着，如果你只是传递一个放在括号内的名字，那么它是一个表达式而不再只是一个名字，decltype 会给出它的类型和值类别。行为如下：

```
void rvFunc(std::string&& str)
{
    std::cout << std::is_same<decltype((str)), std::string>::value;      // false
    std::cout << std::is_same<decltype((str)), std::string&>::value;     // true
    std::cout << std::is_same<decltype((str)), std::string&&>::value;    // false

    std::cout << std::is_reference<decltype((str))>::value;              // true
    std::cout << std::is_lvalue_reference<decltype((str))>::value;       // true
    std::cout << std::is_rvalue_reference<decltype((str))>::value;       // false
}
```

将此与此前不使用额外括号的这个函数实现进行比较。这里，`decltype` 对 `(str)` 求值得到 `std::string&`，因为 `str` 是类型为 `std::string` 的左值。

对于 `decltype` 来说，在传递的名字周围加上额外的括号会产生不同的结果，这一事实在我们稍后讨论 `decltype(auto)` 时也会产生重要影响。

## 在代码内检查值类别

一般来说，现在你可以在代码中按如下方式检查特定的值类别：

- `!std::is_lvalue_reference_v<decltype((expr))>`  
  检查 *expr* 是否为 **纯右值**。
- `std::is_lvalue_reference_v<decltype((expr))>`  
  检查 *expr* 是否为 **左值**。
- `std::is_rvalue_reference_v<decltype((expr))>`  
  检查 *expr* 是否为 **将亡值**。
- `!std::is_lvalue_reference_v<decltype((expr))>`  
  检查 *expr* 是否为 **右值**。

再次注意这里使用的额外括号，以确保即使我们只传递一个名字作为 *expr*，也能使用 `decltype` 的值类别检查形式。

在 C++20 之前，你必须去掉 `_v` 后缀，改为追加 `::value`。

## 8.7 小结

- C++ 程序中的任何表达式恰好属于以下主要值类别之一：
  - **左值**（大致对应有名字的对象或字符串字面量）
  - **纯右值**（大致对应未命名的临时对象）
  - **将亡值**（大致对应使用 `std::move()` 标记的对象）
- C++ 中一次调用或操作是否有效取决于类型和值类别两者。
- 类型的右值引用只能绑定到右值（纯右值或将亡值）。
- 隐式操作可能会改变所传实参的值类别。
- 将右值传递给右值引用时，它被绑定为一个左值。
- 移动语义不会被传递。
- 函数和函数引用始终是左值。
- 对于右值（临时对象或使用 `std::move()` 标记的对象），普通值成员具有移动语义，但引用或静态成员则没有。
- `decltype` 既可以检查所传名字的声明类型，也可以检查所传表达式的类型和值类别。

## 第 9 章

## 完美转发

本章介绍泛型代码中的移动语义。特别是，我们将讨论*通用引用*（也称为*转发引用*）以及（完美）转发。

接下来的章节将讨论通用引用和完美转发中的棘手细节，以及如何处理泛型代码中可能具有也可能不具有移动语义的返回值。

## 9.1 完美转发的动机

我们已经了解到，移动语义不会自动传递。这会对泛型代码产生影响。

## 9.1.1 完美转发实参需要什么

要将以移动语义传递给某个函数的对象转发出去，它不仅必须绑定到右值引用；你还必须再次使用 `std::move()` 才能将其移动语义转发给另一个函数。

例如，请记住按引用重载的函数的主要情况下的重载解析规则：

```
class X {
    ...
};

// forward declarations:
void foo(const X&);          // for constant values (read-only access)
void foo(X&);                // for variable values (out parameters)
void foo(X&&);               // for values that are no longer used (move semantics)
```

在调用这些函数时，我们有以下规则：

```
X v;
const X c;
foo(v);                    // calls foo(X&)
```

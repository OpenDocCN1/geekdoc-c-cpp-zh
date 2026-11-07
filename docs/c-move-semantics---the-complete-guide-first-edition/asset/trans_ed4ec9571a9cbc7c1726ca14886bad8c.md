
## 用于引用或静态成员的 std::move()

如果成员是引用或静态成员，则适用不同规则。² 右值的引用成员或静态成员仍然是左值。同样，这条规则反映出此类成员的值实际上并不属于对象的一部分。说“我不再需要这个对象的值”不应意味着“我不再需要（某个成员的）不属于该对象一部分的值。”

因此，如果存在引用或静态成员，使用 `std::move()` 的方式会有所不同：

- 对*对象*使用 `std::move()` 没有效果：

  ```cpp
  struct S {
      static std::string statString;  // static member
      std::string& refString;         // reference member
  };

  S obj;
  ...
  coll.push_back(std::move(obj).statString);  // copies statString
  coll.push_back(std::move(obj).refString);   // copies refString
  ```

- 对*成员*使用 `std::move()` 会产生通常的效果：

  ```cpp
  struct S {
      static std::string statString;
      std::string& refString;
  };
  S obj;
  ...
  coll.push_back(std::move(obj).statString);  // moves statString
  coll.push_back(std::move(obj).refString);   // moves refString
  ```

这种移动是否有用则是另一个问题。窃取静态成员或被引用成员的值意味着你会修改所用对象之外的值。这可能是有意义的，但也可能令人意外且危险。通常，类型 S 最好保护对这些成员的访问。

在泛型代码中，你可能不知道成员是静态成员还是引用。因此，使用 `std::move()` 标记对象的方法危险性更低，尽管看起来有些奇怪：

```cpp
coll.push_back(std::move(obj).mem1);  // move value, copy reference/static
coll.push_back(std::move(obj).mem2);  // move value, copy reference/static
```

同样，我们稍后介绍的 `std::forward<>()` 可用于完美转发对象的成员。完整示例见 *basics/members.cpp*。

² 感谢 Andrey Upadyshev 指出这一点。

## 8.3 绑定引用时值类别的影响

值类别在我们把引用绑定到对象时起着重要作用。例如，在 C++98/C++03 中，它们规定可以把右值（没有名称的临时对象，或用 `std::move()` 标记的对象）赋值或传递给 const 值引用，但不能传递给非 const 值引用：

```cpp
std::string createString();        // forward declaration

const std::string& r1{createString()};    // OK

std::string& r2{createString()};           // ERROR
```

编译器在此处打印的典型错误消息是“无法将非 const 左值引用绑定到右值。”

在调用下面的 `foo2()` 时也会得到此错误消息：

```cpp
void foo1(const std::string&);       // forward declaration
void foo2(std::string&);              // forward declaration

foo1(std::string{"hello"});          // OK
foo2(std::string{"hello"});          // ERROR
```

### 8.3.1 右值引用的重载解析

让我们看看将对象传递给引用时的确切规则。

假设有一个类 X 的非 const 变量 `v` 和一个 const 变量 `c`：

```cpp
class X {
    ...
};

X v{...};
const X c{...};
```

绑定引用的规则表列出了当我们提供函数 `f()` 的所有引用重载时，将引用绑定到所传实参的正式规则：

```cpp
void f(const X&);    // read-only access
void f(X&);          // OUT parameter (usually long-living object)
void f(X&&);         // can steal value (object usually about to die)
void f(const X&&);   // no clear semantic meaning
```

这些数字列出了重载解析的优先级，以便你看出在提供多个重载时调用哪个函数。数字越小，优先级越高（优先级 1 表示最先尝试）。

注意，只能把右值（纯右值，例如没有名称的临时对象）或亡值（用 `std::move()` 标记的对象）传递给右值引用。右值引用之名即由此而来。

通常可以忽略表格的最后一列，因为 const 右值引用在语义上意义不大，也就是说我们得到以下规则：

| 调用 | `f(X&)` | `f(const X&)` | `f(X&&)` | `f(const X&&)` |
|---|---:|---:|---:|---:|
| `f(v)` | 1 | 2 | 无 | 无 |
| `f(c)` | 无 | 1 | 无 | 无 |
| `f(X{})` | 无 | 3 | 1 | 2 |
| `f(move(v))` | 无 | 3 | 1 | 2 |
| `f(move(c))` | 无 | 2 | 无 | 1 |

*表 8.1. 绑定引用的规则*

- 非 const 左值引用只接受非 const 值。
- 右值引用只接受非 const 右值。
- const 左值引用可以接受一切，并在未提供其他重载时充当回退机制。

下面从表格中间摘录的内容是移动语义回退机制的规则：

| 调用 | `f(const X&)` | `f(X&&)` |
|---|---:|---:|
| `f(X{})` | 3 | 1 |
| `f(move(v))` | 3 | 1 |

如果我们把右值（临时对象或用 `std::move()` 标记的对象）传递给函数，而没有针对移动语义的特定实现（通过接受右值引用来声明），则使用通常的复制语义，以 const& 接受实参。

请注意，稍后介绍通用引用/转发引用时，我们会扩展此表。

在那里我们还会了解到，有时可以把左值传递给右值引用（当使用模板参数时）。请注意，并非每个带 && 的声明都遵循相同规则。这里的规则适用于我们用 && 声明了一个*类型*（或类型别名）的情况。

### 8.3.2 按引用和按值重载

我们可以同时按引用参数和按值参数声明函数。例如：

```cpp
void f(X);         // call-by-value
void f(const X&);  // call-by-reference
void f(X&&);
void f(const X&&);
```

原则上，声明所有这些重载是允许的。然而，按值调用和按引用调用之间没有特定优先级。如果你有一个按值接受实参的函数声明（它可以接受任何值类别的任何实参），那么任何匹配的按引用接受该实参的声明都会造成歧义。

因此，通常应只按值或只按引用接受实参（引用重载数量可按你认为有用的来定），而绝不要两者兼用。

## 8.4 左值何时变为右值

正如我们所学，当函数声明了具体类型的右值引用参数时，只能把这些参数绑定到右值。例如：

```cpp
void rvFunc(std::string&&);      // forward declaration

std::string s{...};
rvFunc(s);                         // ERROR: passing an lvalue to an rvalue reference
rvFunc(std::move(s));             // OK, passing an rvalue
```

然而请注意，有时传递左值看起来可以工作。例如：

```cpp
void rvFunc(std::string&&);      // forward declaration

rvFunc("hello");                 // OK, although "hello" is an lvalue
```

请记住，字符串字面量在作为表达式使用时是左值。因此，把它们传递给右值引用无法编译。然而，这里涉及一个隐藏操作，因为实参的类型（包含六个字符的数组）与参数类型不匹配。我们有一个由 string 构造函数执行的隐式类型转换，它创建一个没有名称的临时对象。

因此，我们实际调用的是以下内容：

```cpp
void rvFunc(std::string&&);      // forward declaration

rvFunc(std::string{"hello"});    // OK, "hello" converted to a string is a prvalue
```

## 8.5 右值何时变为左值

现在让我们看看一个把参数声明为右值引用的函数实现：

```cpp
void rvFunc(std::string&& str) {
    ...
}
```

正如我们所学，只能传递右值：

```cpp
std::string s{...};
rvFunc(s);                         // ERROR: passing an lvalue to an rvalue reference
rvFunc(std::move(s));             // OK, passing an rvalue
rvFunc(std::string{"hello"});     // OK, passing a prvalue
```

然而，当我们在函数内部使用参数 `str` 时，处理的是一个有名称的对象。这意味着我们把 `str` 当作左值使用。我们只能做左值允许做的事情。

这意味着我们不能直接递归调用自己的函数：

```cpp
void rvFunc(std::string&& str) {
    rvFunc(str);                  // ERROR: passing an lvalue to an rvalue reference
}
```

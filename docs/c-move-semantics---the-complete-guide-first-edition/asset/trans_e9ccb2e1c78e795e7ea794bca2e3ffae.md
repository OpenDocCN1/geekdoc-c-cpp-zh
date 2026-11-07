
```cpp
foo(c);                       // calls foo(const X&)
foo(X{});                     // calls foo(X&&)
foo(std::move(v));            // calls foo(X&&)
foo(std::move(c));            // calls foo(const X&)
```

现在假设我们想通过辅助函数 `callFoo()` 间接地用相同的实参调用 `foo()`。这个辅助函数也需要这三个重载：

```cpp
void callFoo(const X& arg) {  // arg binds to all const objects
  foo(arg);                   // calls foo(const X&)
}
void callFoo(X& arg) {        // arg binds to lvalues
  foo(arg);                   // calls foo(X&)
}
void callFoo(X&& arg) {       // arg binds to rvalues
  foo(std::move(arg));        // needs std::move() to call foo(X&&)
}
```

在所有情况下，`arg` 都作为左值使用（因为它是一个有名字的对象）。第一个版本将其作为 `const` 对象转发，而另外两种情况实现了转发非 `const` 实参的两种不同方式：

- 声明为左值引用的实参（绑定到不具有移动语义的对象）按原样传递。
- 声明为右值引用的实参（绑定到具有移动语义的对象）通过 `std::move()` 传递。

这使我们能够完美地转发移动语义：对于任何以移动语义传递的实参，我们保留移动语义；但当我们得到不具有移动语义的实参时，我们不会添加移动语义。

只有采用这种实现，使用 `callFoo()` 调用 `foo()` 才是透明的：

```cpp
X v;
const X c;
callFoo(v);                   // calls foo(X&)
callFoo(c);                   // calls foo(const X&)
callFoo(X{});                 // calls foo(X&&)
callFoo(std::move(v));        // calls foo(X&&)
callFoo(std::move(c));        // calls foo(const X&)
```

请记住，传递给右值引用的右值在使用时会变成左值，这意味着我们需要 `std::move()` 才能再次将其作为右值传递。然而，我们不能在所有地方都使用 `std::move()`。对于其他重载，在传入左值时使用 `std::move()` 会调用 `foo()` 的右值引用重载。

对于泛型代码中的*完美转发*，我们总是需要为每个参数提供所有这些重载。为了支持所有组合，这意味着对于 2 个泛型实参需要 9 个重载，对于 3 个泛型实参需要 27 个重载。

因此，C++11 引入了一种特殊方式，可以在没有任何重载的情况下*完美转发*给定实参，同时仍然保留类型和值类别。

## 完美转发 const 右值引用

尽管 const 右值引用没有语义含义，但如果我们想保留用 `std::move()` 标记的常量对象的精确类型和值类别，甚至还需要第四个重载：

```cpp
void callFoo(const X&& arg) { // arg binds to const rvalues
  foo(std::move(arg));      // needs std::move() to call foo(const X&&)
}
```

否则，我们会调用 `foo(const X&)`。这通常没问题，但可能存在这样的情况：我们希望保留已传递 const 右值引用这一信息（例如，出于某种原因提供了 `foo(const X&&)` 重载时）。

这样一来，除非语言提供用于完美转发的特殊特性，否则泛型代码对于两个或三个参数甚至需要 16 个和 64 个重载。

### 9.2 实现完美转发

为了避免针对具有不同值类别的参数重载函数，C++ 引入了一种用于*完美转发*的特殊机制。你需要三样东西：

1. 将调用参数作为纯右值引用（用 `&&` 声明，但不带 `const` 或 `volatile`）。
2. 参数的类型必须是函数的模板参数。
3. 当将参数转发给另一个函数时，使用名为 `std::forward<>()` 的辅助函数，它声明在 `<utility>` 中。

你必须按如下方式实现一个完美转发实参的函数：

```cpp
template<typename T>
void callFoo(T&& arg) {
  foo(std::forward<T>(arg)); // equivalent to foo(std::move(arg)) for passed rvalues
}
```

`std::forward<>()` 实际上是一个有条件的 `std::move()`，因此我们得到与上面 `callFoo()` 的三个（或四个）重载相同的行为：

- 如果向 `arg` 传递右值，其效果与调用 `foo(std::move(arg))` 相同
- 如果向 `arg` 传递左值，其效果与调用 `foo(arg)` 相同

以同样的方式，我们可以完美转发两个实参：

```cpp
template<typename T1, typename T2>
void callFoo(T1&& arg1, T2&& arg2) {
  foo(std::forward<T1>(arg1), std::forward<T2>(arg2));
}
```

我们还可以将 `std::forward<>()` 应用于可变数量参数的每个实参，以完美转发它们全部：

```cpp
template<typename... Ts>
void callFoo(Ts&&... args) {
  foo(std::forward<Ts>(args)...);
}
```

注意，我们不是对所有实参调用一次 `forward<>()`；而是分别对每个实参调用它。因此，我们必须将省略号（`...`）放在 `forward()` 表达式的末尾之后，而不是直接放在 `args` 之后。

然而，这里究竟发生了什么相当棘手，需要仔细解释。

#### 9.2.1 万能（或转发）引用

首先，请注意我们将 `arg` 声明为右值引用参数：

```cpp
template<typename T>
void callFoo(T&& arg);   // arg is universal/forwarding reference
```

这可能会让人以为适用右值引用的通常规则。然而，事实并非如此。**函数模板参数**的**右值引用**（未用 `const` 或 `volatile` 限定）不遵循普通右值引用的规则。它是另一回事。

##### 两个术语：万能引用与转发引用

这样的引用称为*万能引用*。不幸的是，它还有另一个主要用在 C++ 标准中的术语：*转发引用*。这两个术语之间没有区别，只是这里存在历史遗留的混乱：有两个已确立的术语表示同一件事。

这两个术语都描述了万能引用/转发引用的基本方面：

- 它们可以通用地绑定到所有类型（const 和非 const）以及所有值类别的对象。
- 它们通常用于转发实参；但请注意，这并不是唯一用途（这也是我更偏好*万能引用*这一术语的原因之一）。

##### 万能引用可绑定到所有值类别

万能引用的重要特性是它们可以绑定到任何值类别的对象和表达式：

```cpp
template<typename T>
void callFoo(T&& arg);   // arg is a universal/forwarding reference
```

```cpp
X v;
const X c;
callFoo(v);              // OK
callFoo(c);              // OK
callFoo(X{});            // OK
callFoo(std::move(v));   // OK
callFoo(std::move(c));   // OK
```

此外，它们会保留所绑定对象的 const 性和值类别（无论我们拥有的是右值还是左值）：

```cpp
template<typename T>
void callFoo(T&& arg);   // arg is a universal/forwarding reference
```

```cpp
X v;
const X c;
callFoo(v);                  // OK, arg is X&
callFoo(c);                  // OK, arg is const X&
callFoo(X{});                // OK, arg is X&&
callFoo(std::move(v));       // OK, arg is X&&
callFoo(std::move(c));       // OK, arg is const X&&
```

根据规则，类型 `T&&`（即 `arg` 的类型）是

- 如果我们引用左值，则为左值引用
- 如果我们引用右值，则为右值引用

注意，用 const（或 volatile）限定的泛型右值引用**不是**万能引用。你只能传递右值：

```cpp
template<typename T>
void callFoo(const T&& arg);   // arg is not a universal/forwarding reference
```

```cpp
const X c;
callFoo(c);                  // ERROR: c is not an rvalue
callFoo(std::move(c));       // OK, arg is const X&&
```

还要注意，我还没有讨论 `T` 的类型。稍后我会解释在万能引用中 `T` 被推导为什么类型。

稍后，我们将讨论使用 lambda 的相应示例。

#### 9.2.2 `std::forward<>()`

在 `callFoo()` 内部，当我们按如下方式使用万能引用时：

```cpp
template<typename T>
void callFoo(T&& arg) {
    foo(std::forward<T>(arg));   // becomes foo(std::move(arg)) for passed rvalues
}
```

与 `std::move()` 一样，`std::forward<T>()` 也定义为头文件 `<utility>` 中的函数模板。

表达式 `std::forward<T>(arg)` 本质上按如下方式实现：

- 如果向函数传递类型为 `T` 的右值，则该表达式等价于 `std::move(arg)`。
- 如果向函数传递类型为 `T` 的左值，则该表达式等价于 `arg`。

也就是说，`std::forward<T>()` 仅对传递的右值而言才是 `std::move()`。

*就像 `std::move()` 一样，`std::forward<T>()` 的语义含义是：我在这里不再需要这个值了，额外的好处是我们保留了所传入的万能引用所绑定对象的类型（包括 const 性）和值类别。你可能会争辩说，你只是有条件地声明不再需要该值，但由于你不知道 `std::forward<T>()` 是否会变成 `std::move()`，因此假设该对象之后仍保留其值将是错误的。所以再次强调，你应该假设的只是：使用 `std::forward<T>()` 之后，对象通常是有效的，但你不知道它的值。*

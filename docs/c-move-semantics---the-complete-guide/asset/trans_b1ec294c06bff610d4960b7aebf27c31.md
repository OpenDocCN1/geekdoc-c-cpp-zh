

```
foo(c);                // calls foo(const X&)
foo(X{});              // calls foo(X&&)
foo(std::move(v));     // calls foo(X&&)
foo(std::move(c));     // calls foo(const X&)
```

现在假设我们想通过一个辅助函数 `callFoo()` 间接为相同的参数调用 `foo()`。该辅助函数也需要三个重载：

```
void callFoo(const X& arg) { // arg binds to all const objects
    foo(arg);               // calls foo(const X&)
}
void callFoo(X& arg) {      // arg binds to lvalues
    foo(arg);               // calls foo(X&)
}
void callFoo(X&& arg) {     // arg binds to rvalues
    foo(std::move(arg));    // needs std::move() to call foo(X&&)
}
```

在所有情况下，`arg` 都作为左值使用（是一个有名称的对象）。第一个版本将其作为 const 对象转发，但另外两个情况实现了转发非 const 参数的两种不同方式：

- 声明为左值引用（绑定到没有移动语义的对象）的参数只是原样传递。
- 声明为右值引用（绑定到具有移动语义的对象）的参数会使用 `std::move()` 传递。

这使我们能够完美地转发移动语义：对于以移动语义传递的任何参数，我们保留移动语义；但对于没有移动语义的参数，我们不会添加移动语义。

只有通过这种实现，使用 `callFoo()` 调用 `foo()` 才是透明的：

```
X v;
const X c;
callFoo(v);             // calls foo(X&)
callFoo(c);             // calls foo(const X&)
callFoo(X{});           // calls foo(X&&)
callFoo(std::move(v));  // calls foo(X&&)
callFoo(std::move(c));  // calls foo(const X&)
```

记住，传递给右值引用的右值在使用时变成左值，这意味着我们需要 `std::move()` 再次将其作为右值传递。然而，我们不能在所有地方都使用 `std::move()`。对于其他重载，使用 `std::move()` 会在传递左值时调用 `foo()` 的右值引用重载。

在通用代码中实现完美转发时，我们将始终需要为每个参数提供所有这些重载。为了支持所有组合，这意味着对于 2 个通用参数需要 9 个重载，对于 3 个通用参数需要 27 个重载。

因此，C++11 引入了一种特殊的完美转发方式，无需任何重载即可转发给定参数，同时仍保留类型和值类别。

## 完美转发 const 右值引用

尽管 const 右值引用对我们没有语义意义，如果我们想保留用 `std::move()` 标记的常量对象的确切类型和值类别，我们甚至需要第四个重载：

```
void callFoo(const X&& arg) { // arg binds to const rvalues
    foo(std::move(arg));      // needs std::move() to call foo(const X&&)
}
```

否则，我们将调用 `foo(const X&)`。这通常是可以的，但在某些情况下我们可能希望保留传递了 const 右值引用的知识（例如，当出于某种原因提供了 `foo(const X&&)` 重载时）。

有了它，通用代码将需要 16 个和 64 个重载用于两个或三个参数，除非语言提供完美转发的特殊功能。

## 9.2 实现完美转发

为了避免为具有不同值类别的参数重载函数，C++ 引入了一种用于 *完美转发* 的特殊机制。你需要三件事：

1. 将调用参数作为纯右值引用接收（声明为 `&&` 但不带 `const` 或 `volatile`）。
2. 参数的类型必须是函数的模板参数。
3. 转发参数到另一个函数时，使用声明在 `<utility>` 中的辅助函数 `std::forward<>()`。

你需要实现一个完美转发参数的函数，如下所示：

```
template<typename T>
void callFoo(T&& arg) {
    foo(std::forward<T>(arg));  // equivalent to foo(std::move(arg)) for passed rvalues
}
```

`std::forward<>` 本质上是一个条件 `std::move()`，因此我们得到的行为与上面 `callFoo()` 的三个（或四个）重载相同：

- 如果我们将一个右值传递给 `arg`，其效果等同于调用 `foo(std::move(arg))`
- 如果我们将一个左值传递给 `arg`，其效果等同于调用 `foo(arg)`

以同样的方式，我们可以完美转发两个参数：

```
template<typename T1, typename T2>
void callFoo(T1&& arg1, T2&& arg2) {
    foo(std::forward<T1>(arg1), std::forward<T2>(arg2));
}
```

我们也可以将 `std::forward<>` 应用于可变数量参数的每个参数，以完美转发它们全部：

```
template<typename... Ts>
void callFoo(Ts&&... args) {
    foo(std::forward<Ts>(args)...);
}
```

请注意，我们不会对所有参数一次性调用 `std::forward<>()`；我们对每个参数单独调用。因此，我们必须将省略号（“...”）放在 `forward()` 表达式的末尾，而不是直接放在 args 后面。

然而，这里发生的事情相当棘手，需要仔细解释。

### 9.2.1 通用（或转发）引用

首先，注意我们将 `arg` 声明为右值引用参数：

```
template<typename T>
void callFoo(T&& arg);  // arg is universal/forwarding reference
```

这可能会让人觉得通常的右值引用规则适用。然而，情况并非如此。函数模板参数的未限定 const 或 volatile 的右值引用并不遵循普通右值引用的规则。它是另一回事。

### 两个术语：通用和转发引用

这种引用被称为通用引用。不幸的是，它还有另一个术语，主要在 C++ 标准中使用：转发引用。这两个术语之间没有区别，只是我们在这里有一个历史混乱，两个已建立的术语含义相同。

这两个术语都描述了通用/转发引用的基本方面：

- 它们可以通用地绑定到所有类型（const 和非 const）的对象和值类别。
- 它们通常用于转发参数；但请注意，这不是唯一的用途（我更喜欢通用引用这个术语的一个原因）。

### 通用引用绑定到所有值类别

通用引用的重要特性是它们可以绑定到任何值类别的对象和表达式：

```
template<typename T>
void callFoo(T&& arg);     // arg is a universal/forwarding reference
```

```
X v;
const X c;
callFoo(v);                // OK
callFoo(c);                // OK
callFoo(X{});              // OK
callFoo(std::move(v));     // OK
callFoo(std::move(c));     // OK
```

此外，它们保留所绑定对象的 const 性和值类别（我们是否有右值或左值）：

```
template<typename T>
void callFoo(T&& arg);     // arg is a universal/forwarding reference

X v;
const X c;
callFoo(v);                         // OK, arg is X&
callFoo(c);                         // OK, arg is const X&
callFoo(X{});                       // OK, arg is X&&
callFoo(std::move(v));              // OK, arg is X&&
callFoo(std::move(c));              // OK, arg is const X&&
```

按规则，`arg` 的类型 `T&&` 是

- 如果我们引用一个左值，则为左值引用
- 如果我们引用一个右值，则为右值引用

请注意，被 `const`（或 `volatile`）限定的通用右值引用**不是**通用引用。你只能传递右值：

```
template<typename T>
void callFoo(const T&& arg);  // arg is not a universal/forwarding reference

const X c;
callFoo(c);                    // ERROR: c is not an rvalue
callFoo(std::move(c));         // OK, arg is const X&&
```

请注意，我还没有谈论 `T` 的类型。我稍后会解释使用通用引用时推导出的 `T` 的类型是什么。

稍后，我们将讨论使用 lambda 的相应示例。

### 9.2.2 `std::forward<>`

在 `callFoo()` 内部，我们随后按如下方式使用通用引用：

```
template<typename T>
void callFoo(T&& arg) {
  foo(std::forward<T>(arg));  // becomes foo(std::move(arg)) for passed rvalues
}
```

与 `std::move()` 一样，`std::forward<>()` 也定义为头文件 `<utility>` 中的函数模板。
表达式 `std::forward<T>(arg)` 本质上实现如下：

- 如果将 `T` 类型的右值传递给函数，则该表达式等价于 `std::move(arg)`。
- 如果将 `T` 类型的左值传递给函数，则该表达式等价于 `arg`。

也就是说，`std::forward<>()` 仅对传递的右值是 `std::move()`。

与 `std::move()` 一样，`std::forward<>()` 的语义含义是 *我不再需要这个值在这里*，额外的好处是我们保留了传递的通用引用所绑定对象的类型（包括 const 性和值类别）。你可以认为你只是有条件地说你不再需要该值，但因为你不知道 `std::forward<>()` 是否会变成 `std::move()`，所以假设对象之后仍有其值是错误的。所以再次强调，你唯一应该假设的是，使用 `std::forward<>()` 之后对象通常是有效的，但你不知道其值。


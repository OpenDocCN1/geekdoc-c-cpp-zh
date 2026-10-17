
[Note 3：指向 mutable 非静态成员的指针 (9.2.2) 不反映 mutable 限定符。 — 示例]

只有当使用表达式 `&` 且运算符为包含在括号内的 qualified-id 时，才会形成指向成员的指针。
[Note 4：即，在 unqualified-id 的作用域内，包含在括号内的 qualified-id 不会形成从该表达式的值到“指向成员” (7.3.4)。而且即使在 unqualified-id 的类范围内，unqualified-id 也不是指向成员。 — 脚注]

5 如果 `&` 应用于 unqualified 类型，它决定了调用位运算运算符还是成员函数。运算符 `&` 不应是位域（bit-field）。
[Note 5：重载函数的结果（第 12 节）只能在确定表达式版本的上下文中获取（见 5.2.6）。由于上下文可以判断操作数是静态成员还是非静态成员函数，上下文也可以判断表达式是“指向成员”还是“函数成员”。 — 脚注]

7 一元运算符 — 是算术或无符号运算符类型，结果是操作数的值。对整数或无符号操作数进行整数提升。结果的类型是提升操作数的类型。

8 一元运算符 `~` 是算术或无符号运算符类型，结果是操作数的取反。对操作数进行整数提升。无符号操作数的取反是通过从 2^n 中减去实现的，其中 n 是提升操作数的位数。

9 逻辑运算符 `!=` 在概念上转换为 `bool` (7.3)；如果转换的操作数为 false，则其值为 true。结果的类型是 `bool`。

10 `++` 的操作数应具有整数或无符号类型，结果是操作数的递增。进行整数提升。当 `++` 后面跟随类型名或指定符时，语法中存在歧义。通过将一元运算符视为 unqualified-id 的开头来解决歧义。
[Note 6：由于语法不允许运算符紧跟在 ... 之后，或者作为跟随类型名或指定符的成员表达式或 unqualified-id，它被解析为析构函数。 — 脚注]

## 7.6.3 递增与递减

1 `++` 的操作数通过加 1 进行修改 (3.1)。操作数的类型应为算术类型或 `bool`，或者指向良定义对象的指针。`volatile` 限定符的类型已弃用；结果是更新后的操作数；它是一个值，如果操作数是位域，它也是位域。表达式 `++` 等同于 `x++`。
[Note 1：信息参见加法 (7.6.6) 和赋值运算符 (7.6.19) 的讨论。]

2 `--` 的操作数通过减 1 进行修改 (3.1)。对 `--` 的要求及其结果的属性与前缀相同。
[Note 2：对于后缀递增和递减，见 7.6.16。 — 脚注]

§ 7.6.2

### 7.6.2.4 等待 (Await)

`co_await` 表达式用于挂起协程 (9.5.4) 的评估，同时等待操作数表达式所代表的计算完成。

```cpp
await-expression
    cast-expression
```

`await-expression` 只能出现在函数体复合语句 (14.1) 内完全表达式。在声明语句或初始化语句的简单声明（如果有）中，它仅出现在该声明语句或简单声明的初始化器中。`await-expression` 不出现在默认参数 (9.3.4) 中。`await-expression` 不出现在具有静态存储的块作用域变量的初始化器中。出现 `await-expression` 的上下文被视为函数的挂起上下文。

求值 `await-expression` 涉及以下类型、表达式对象：

* `p` 是封装协程的等待 (9.5.4)，`P` 是以下内容的类型：
* 如果 `await-expression` 是通过 `yield-expression` (6.17.2)、初始挂起点或最终挂起点 (9.5.4) 隐式转换的，则 `a` 为 `cast-expression`。否则，在 `P` 的作用域内通过成员访问查找 (6.5.6)  unqualified-id，如果查找找到一个声明，则 `a` 为 `cast-expression`。
* `o` 通过对参数 `a` 计算相应的 `operator co_await` 函数 (12.4.2.3) 并选择最佳重载解析 (12.4) 来确定。如果重载解析存在义，程序是格式错误的。如果没有找到值，`o` 是 `a`。否则，`o` 是带参数 `a` 的函数调用。如果 `o` 是一个值，则应用实例化 (7.3.5)。
* `e` 是结果 `o` 的结果引用。
* `h` 是类型为 `std::coroutine_handle<P>` 的对象，引用封装协程。
* `await-ready` 是表达式 `e.await_ready()`，转换为 `bool`。
* `await-suspend` 是表达式 `e.await_suspend(h)`，其应为 `void`、`bool` 或某些类型 `Z` 的 `std::coroutine_handle<Z>` 类型的值。
* `await-resume` 是表达式 `e.await_resume()`。

`await-expression` 的类型和值与 `await-ready` 和 `await-resume` 表达式相同，然后：

`await-expression` 求值转换表达式和 `await-ready` 表达式，然后：

* 如果 `await-ready` 的结果为 false，协程被视为挂起。然后：
* 如果 `await-suspend` 的类型是 `std::coroutine_handle<Z>`，执行 `await_resume()`。
> 注意：指向 `await-suspend` 结果的协程。可以通过这种方式成功恢复任意协程，将控制流返回给当前协程调用者或恢复者 (9.5.4)。 — 脚注
* 否则，如果 `await-suspend` 的类型为 `bool`，执行 `await-suspend`，如果结果为 false，则恢复协程。
* 否则，执行 `await-resume`。

* 如果 `await-ready` 的结果为 true，恢复协程，并执行 `await-resume` 表达式，其结果为 `await-expression` 的结果。

# ISO/IEC 14882:2020(E)

```cpp
T await_resume();;

template <class Rep, class Period>
auto co_await(std::chrono::duration<Rep, Period> d) {
    struct await {
        /* ... */
        std::chrono::system_clock::duration duration;
        await(std::chrono::system_clock::duration d) : duration(d) {}
        bool await_ready() const { return duration.count() <= 0; }
        void await_resume() {}
        void await_suspend(std::coroutine_handle<...> h) { /* ... */ }
    };
    return await(d);
}
```

`using namespace std::chrono;`

`my_future<int> h();`

```cpp
my_future<void> g() {
    std::cout << "just about go to sleep...\n";
    co_await 10ms;
    std::cout << "resumed\n";
    co_await h();
}
```

```cpp
auto f(int x = co_await h()); // error: await-expression outside of function context
int self = { co_await h(); }; // error: await-expression outside of function context
```

## 7.6.2 Sizeof

[expr:sizeof]

1 `sizeof` 运算符产生其操作数类型类型的非潜在重叠对象所占的字节数。操作数可以是一个表达式、一个未求值的表达式 (7.2)，或者是指向某些类型的指针。`sizeof` 运算符不应应用于函数类型或不完整类型的表达式，也不应应用于此类类型的参数化名称，或作用于粘接字段（glue-field）。`sizeof` 应用于任何数字的 result均为 1。`sizeof` 应用于任何基本类型 (6.8) 的结果由实现定义。

> 注释 [1: `sizeof(bool)`, `sizeof(char16_t)`, `sizeof(char32_t)` 和 `sizeof(char_t)` 的结果由实现定义。 — 注释结束]

> 注释 [2: 字节的定义参见 6.7.1，对象表示的定义参见 6.8。 — 注释结束]

2 当应用于引用时，结果是所引用对象的大小。当应用于类时，结果是该类对象的字节数，其中包括为了数组中该类型的成员而所需的任何填充（padding）。`sizeof` 应用于潜在重叠的子对象，结果是该子对象的大小。当应用于数组时，结果是数组中的总字节数，这意味着一个包含 n 个元素的数组的大小是元素大小的 n 倍。

3 左值到引用 (7.3.2)、数组到指针 (7.3.3) 和函数到指针 (7.3.4) 标准转换不应用于 `sizeof` 的操作数。如果操作数是函数，则应用临时实物化转换 (7.3.5)。

4 `sizeof...` 表达式中的标识符应该有一个名称。`sizeof...` 运算符产生参数包 (13.7.4) 中的元素个数。`sizeof...` 是一个包展开 (13.7.4)。

```cpp
示例 1:
template<class... Types>
struct count {
    static const std::size_t value = sizeof...(Types);
};
// 示例示例结束
```

5 `sizeof` 和 `sizeof...` 的结果是类型为 `std::size_t` 的纯右值 (prvalue)。

> [注释 3 `sizeof` 表达式是一个整型常量表达式 (7.7)。`std::size_t` 类型定义在头文件 `<cstddef>` 中 (17.2.1, 17.2.4.) — 注释结束]

## 7.6.2 Alignof

1 `Alignof` 产生操作数的对齐要求。操作数应该是表示完整对象、数组或这些类型的引用类型标识。

2 结果是类型为 `std::size_t` 的值。

> [注释 1 `alignof` 表达式是一个整型常量表达式 (7.7)。`std::size_t` 类型定义在头文件 `<cstddef>` 中 (17.2.4.) — 注释结束]

3 当 `alignof` 应用引用时，结果是所引用类型的对齐。当 `alignof` 应用于数组时，结果是元素的对齐。

## 7.6.2 noexcept

1 `noexcept` 运算符决定其操作数 (一个未求值的操作数 (14.2)) 是否可能抛出异常。

```cpp
noexcept-expression:
noexcept (
```

2 `noexcept` 运算符的结果是类型为 `bool` 的值。

> [注释 1 `noexcept` 表达式是一个整型常量表达式 (7.7) — 注释结束]

3 除非表达式是可能抛出的 (14.5)，否则 `noexcept` 运算符为 true。

## New

1 `new` 表达式尝试创建 `type-id` (9.3.2) 或分配的对象。该对象的类型必须是完整对象，但不能是抽象类类型或数组。[注释 1 因为引用不是对象，因此无法通过 `new` 表达式创建。 — 注释结束]

> [注释 2 `type-id` 可以是限定类型，在这种情况下，`new` 表达式创建的对象具有限定类型。 — 注释结束]

```cpp
new-expression:
:opt new-placement,opt new-type-id new-initializer
:opt new-placement,opt (type-id ) new-initializer
new-placement:
( expression )
new-type-id:
type-specifier-seq new-declarator
new-declarator:
ptr-operator-new-declarator
noptr-declarator:
[ expression ] attribute-specifier-seq
noptr-declarator:
[ constant-expression ] attribute-specifier-seq
new-initializer:
( expression-list )
braced-init-list
```

2 如果占位符类型 (9.2.6) 出现在 `type-specifier-seq` 中，且 let 是初始化列表（如果有），且 `T` 是 `new` 表达式的 `new-type-id`，那么分配类型取决于变量 `x` (9.2.6)：

```cpp
T x;
示例 1:
new auto(1); // 分配类型为 int
auto x = new('a'); // 分配类型为 char，x 类型为 char*
template<class T> struct A {A(T, T);};
y = new A(1, 2); // 分配类型为 A<int>
// 示例结束
```

3 `new` 表达式中的 `new-type-id` 是最可能的序列。防止了声明与其对应的表达式形式之间的歧义。

```cpp
示例 2:
new int * i; // 语法错误：解析为 (new int*) i，而不是作为乘法运算符的 (new int*)i。
```

4 注释 4：`new` 表达式中 `new-type-id` 的括号可能会产生意外影响。

```cpp
示例 3:
new int(<10>); // 错误，因为绑定为 (new int*)(<10>())
可以使用 new 的前缀版本创建复合类型对象 (6.8.3);
new int (*<10>)(); // 分配 10 个函数指针（无参数并返回 int）。
```

5 `new` 表达式创建的对象具有动态存储期 (6.7.5.5)。注释 5：对象的生命周期并不一定与其创建的作用域相关。 — 注释结束]

当分配的对象是数组时，`new` 表达式的结果指向所创建对象的指针。

6 当分配的对象是数组时（即使用 `ptr-new-declarator` 语法或 `new-type-id` 表示数组），`new` 表达式产生数组第一个元素（如果有）的指针。[注释 6：`int` 和 `new int[10]` 的类型都是 `int*`，`new int[10]` 的类型是 `int (*10)` — 注释结束]

`ptr-new-declarator` 中的 `attribute-specifier-seq` 关联相关的数组类型。

7 `ptr-new-declarator` 中的每个常量表达式必须是类型为 `std::size_t` 的常量表达式 (7.7) 且必须大于零。

```cpp
示例 4:
给定输入 n = 42，new float[n] 是格式错误的，因为 n 不是常量表达式。
// 示例结束
```

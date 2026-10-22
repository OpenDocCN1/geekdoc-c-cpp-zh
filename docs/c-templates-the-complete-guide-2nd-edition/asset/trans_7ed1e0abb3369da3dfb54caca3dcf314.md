
```cpp
static int count; //#10
};
void print() const { //#11
}
};
```

在泛型模板 `Outer` #1 中，位于点 #4 的普通成员 `code` 和位于点 #5 的 `print()` 只有一个外围类模板，因此需要用一个 `template<>` 前缀来为特定的模板实参集完全特化它们：

```cpp
template<>
int Outer<void>::code = 12;

template<>
void Outer<void>::print() const
{
std::cout << "Outer<void>";
}
```

对于类 `Outer<void>`，这些定义会取代点 #4 和 #5 处的泛型定义，但类 `Outer<void>` 的其他成员仍然从点 #1 处的模板生成。注意，在这些声明之后，再为 `Outer<void>` 提供显式特化就不再合法了。

正如函数模板完全特化一样，我们需要一种方式来声明类模板的普通成员的特化，而无需指定定义（以防止多重定义）。虽然在 C++ 中，对于普通类的成员函数和静态数据成员，不允许在类外进行非定义声明，但在特化类模板的成员时，这种做法是允许的。前面的定义可以用以下方式声明：

```cpp
template<>
int Outer<void>::code;

template<>
void Outer<void>::print() const;
```

细心的读者可能会指出，`Outer<void>::code` 的完全特化的非定义声明看起来就像是使用默认构造函数初始化的定义。事实确实如此，但这种声明总是被解释为非定义声明。对于类型只能使用默认构造函数初始化的静态数据成员的完全特化，我们必须借助初始化列表语法。考虑以下代码：

```cpp
class DefaultInitOnly {
public:
DefaultInitOnly() = default;
DefaultInitOnly(DefaultInitOnly const&) = delete;
};

template<typename T>
class Statics {
private:
static T sm;
};
```

下面是一个声明：

```cpp
template<>
DefaultInitOnly Statics<DefaultInitOnly>::sm;
```

而下面则是一个调用默认构造函数的定义：

```cpp
template<>
DefaultInitOnly Statics<DefaultInitOnly>::sm{};
```

在 C++11 之前，这是不可能的。因此，对于此类特化，默认初始化并不可用。通常使用一种复制默认值的初始化器：

```cpp
template<>
DefaultInitOnly Statics<DefaultInitOnly>::sm = DefaultInitOnly();
```

不幸的是，对我们的示例而言这并不可行，因为拷贝构造函数已被删除。不过，C++17 引入了强制性拷贝省略规则，使得这种替代方案变得有效，因为不再涉及拷贝构造函数的调用。

成员模板 `Outer<T>::Inner` 也可以针对给定的模板实参进行特化，而不会影响 `Outer<T>` 特定实例化的其他成员，我们正是在为该实例化特化成员模板。同样，由于有一个外围模板，我们需要一个 `template<>` 前缀。这会产生如下代码：

```cpp
template<>
template<typename X>
class Outer<wchar_t>::Inner {
public:
static long count; // member type changed
};
```

```cpp
template<>
template<typename X>
long Outer<wchar_t>::Inner<X>::count;
```

模板 `Outer<T>::Inner` 也可以进行完全特化，但只能针对 `Outer<T>` 的给定实例进行。现在我们需要的 `template<>` 前缀有两个：一个是因为外围类，另一个是因为我们正在完全特化内部模板：

```cpp
template<>
template<>
class Outer<char>::Inner<wchar_t> {
public:
enum { count = 1 };
};

// the following is not valid C++:
// template<> cannot follow a template parameter list
template<typename X>
template<> class Outer<X>::Inner<void>; // ERROR
```

将此与 `Outer<bool>` 的成员模板的特化进行对比。由于后者已被完全特化，不再有外围模板，因此我们只需要一个 `template<>` 前缀：

```cpp
template<>
class Outer<bool>::Inner<wchar_t> {
public:
enum { count = 2 };
};
```

## 16.4 类模板的部分特化

完全模板特化通常很有用，但有时我们自然希望针对一族模板实参而非仅一组特定模板实参来特化类模板或变量模板。例如，假设我们有一个实现链表的类模板：

```cpp
template<typename T>
class List { // #1
public:
...
void append(T const&);
inline std::size_t length() const;
...
};
```

使用此模板的大型项目可能会为许多类型实例化其成员。对于未内联展开的成员函数（例如 `List<T>::append()`），这可能导致目标代码明显增大。然而，我们可能知道，从底层角度看，`List<int*>::append()` 和 `List<void*>::append()` 的代码是相同的。

换句话说，我们希望指定所有指针的 `List` 共享一个实现。虽然这在 C++ 中无法直接表达，但我们可以通过指定所有指针的 `List` 应从不同的模板定义实例化来实现非常接近的效果：

```cpp
template<typename T>
class List<T*> { // #2
private:
List<void*> impl;
...
public:
...
inline void append(T* p) {
impl.append(p);
}
inline std::size_t length() const {
return impl.length();
}
...;
};
```

在此上下文中，点 #1 处的原始模板称为主模板，而后面的定义称为部分特化（因为必须使用此模板定义的模板实参仅被部分指定）。部分特化的特征语法是模板参数列表声明（`template<...>`）与类模板名称上的一组显式指定的模板实参（在我们的示例中为 `<T*>`）的组合。

我们的代码包含一个问题，因为 `List<void*>` 递归地包含了同一 `List<void*>` 类型的成员。为了打破这个循环，我们可以在前面的部分特化之前加上一个完全特化：

```cpp
template<>
class List<void*> { // #3
...
void append (void* p);
inline std::size_t length() const;
...;
};
```

这样做是有效的，因为匹配的完全特化优先于部分特化。结果，所有指针 `List` 的成员函数都（通过易于内联的函数）转发到 `List<void*>` 的实现。这是一种对抗代码膨胀的有效方法（C++ 模板常被指责会导致代码膨胀）。

部分特化声明的参数列表和实参列表存在若干限制。其中一些如下：

1. 部分特化的实参与主模板的相应参数在种类上（类型、非类型或模板）必须匹配。
2. 部分特化的参数列表不能有默认实参；而是使用主类模板的默认实参。
3. 部分特化的非类型实参应为非依赖值或普通的非类型模板参数。它们不能是更复杂的依赖表达式，例如 `2*N`（其中 `N` 是模板参数）。
4. 部分特化的模板实参列表（忽略重命名）不应与主模板的参数列表相同。
5. 如果其中一个模板实参是包展开，它必须位于模板实参列表的末尾。

下面这个示例说明了这些限制：

```cpp
template<typename T, int I = 3>
class S; // primary template

template<typename T>
class S<int, T>; // ERROR: parameter kind mismatch

template<typename T = int>
class S<T, 10>; // ERROR: no default arguments

template<int I>
class S<int, I*2>; // ERROR: no nontype expressions

template<typename U, int K>
class S<U, K>; // ERROR: no significant difference from primary template

template<typename... Ts>
class Tuple;

template<typename Tail, typename... Ts>
class Tuple<Ts..., Tail>; // ERROR: pack expansion not at the end

template<typename Tail, typename... Ts>
class Tuple<Tuple<Ts...>, Tail>; // OK: pack expansion is at the end of a
// nested template argument list
```

每个部分特化——如同每个完全特化——都与主模板相关联。当使用模板时，主模板总是

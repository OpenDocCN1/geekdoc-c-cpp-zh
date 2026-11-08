
```cpp
template<typename... Types>
class MyAllocator {
    Container storage; // implicitly equivalent to
    std::allocator<Types...>
};
```

```cpp
class Map {
    Container storage;
};
```

### 12.2.4 模板参数包

自 C++11 起，通过在模板形参名之前引入省略号（...），任何类型的模板形参都可以转变为模板参数包。如果模板形参未命名，则省略号出现在原本应出现模板形参名的位置：

```cpp
template<typename... Types> // declares a template parameter pack
class Tuple;
```

模板参数包的行为类似于其底层模板形参，但有一个关键区别：普通模板形参必须恰好匹配一个模板实参，而模板参数包可以匹配任意数量的模板实参。这意味着上面声明的 tuple 类模板接受任意数量（可能互不相同）的类型作为模板实参。

```cpp
template<size_t... Dimensions>
class MultiArray; // OK: declares a nontype template parameter pack

template<typename... Types>
class MultiArray; // OK: declares a type template parameter pack
```

MultiArray 示例要求所有非类型模板实参都具有相同的类型 unsigned。C++17 引入了推导非类型模板实参的可能性，这使我们能够在一定程度上绕过该限制——详情参见第 298 页 15.1.10 节。

对于类模板，最多允许一个模板参数包；如果存在，该模板参数包必须是最后一个模板形参。函数模板的限制更宽松：允许多个模板参数包，只要模板参数包之后的每个模板形参要么具有默认值（见下一节），要么可以被推导。

```cpp
template<typename... Types>
class ListType; // ERROR: a template parameter pack is not the last template parameter

template<typename... T>
void round(T value); // OK: by a deducible template parameter

template<typename... T, typename U>
class Tuple; // ERROR: a template parameter pack is not last
```

最后一个示例是带推导返回类型的函数声明——C++14 特性。另见第 396 页 15.10 节。

类和变量模板的部分特化声明（见第 16 章）可以具有多个参数包，这一点与对应的主模板不同。这是因为部分特化通过一个与函数模板所用过程几乎相同的推导过程来选择。

```cpp
template<typename... Types>
class Tuple<Types...> {
    // OK: partial specialization uses deduction to
    // determine the template arguments
};
```

```cpp
template<typename T, Ts, Ta, void staticValue() {
    // ...
}
```

包含模板参数包的模板称为可变参数模板，因为它接受可变数量的模板实参。第 4 章和第 300 页 12.4 节描述了可变参数模板的用法。

然而，嵌套模板可以产生类似的有效情形：

```cpp
template<typename T, struct ArgList {
    template<T> void value(T...);
};

ArgList<int, char, short> val;
```

包含模板参数包的模板称为可变参数模板，因为它接受可变数量的模板实参。第 4 章和第 300 页 12.4 节描述了可变参数模板的用法。

### 12.2.5 默认模板实参

任何不是模板参数包的模板形参都可以配备默认实参，不过它在种类上必须与对应的形参匹配（例如，类型形参不能具有非类型默认实参）。默认实参不能依赖于其自身形参，因为该形参的名字在默认实参之后才进入作用域。不过，它可以依赖前面的形参：

```cpp
template<typename T, typename Allocator = allocator<T>>
class List;
```

类模板、变量模板或别名模板的模板形参可以具有默认模板实参，仅当后续形参也提供了默认实参时。（默认函数调用实参也存在类似约束。）后续默认值通常在模板声明中提供，但也可能已在该模板之前的声明中声明。以下示例说明了这一点：

```cpp
template<typename T1, typename T2, typename T3>
class OutputBuffer { // T4 and T5 already have defaults
};

template<typename T1, typename T2, typename T3 = char,
         typename T4 = char>
class OutputBuffer { // T4 and T5 already have defaults
};
```

函数模板的模板形参的默认模板实参不要求后续模板形参具有默认模板实参：

```cpp
template<typename T = void, typename U>
void f(); // T is not explicitly specified
```

默认模板实参不能重复：

```cpp
template<typename T = void>
class Value;

template<typename T = void>
class Value; // Error: repeated default argument
```

若干上下文不允许默认模板实参：

- 部分特化：

    ```cpp
    template<typename T>
    class C;

    template<typename T = int>
    class C<T>; // error
    ```

- 参数包：

    ```cpp
    template<typename... T = int> struct X; // ERROR
    ```

- 类模板成员的类外定义：

    ```cpp
    template<typename T = int> struct X
    {
        T f();
    };

    template<typename T = int> T X<T>::f() { // ERROR
        ...
    }
    ```

```cpp
struct S {
    template<typename = void> friend struct F;
};
```

- 友元函数模板声明，除非它是定义，并且其声明未出现在翻译单元中的其他任何地方：

    ```cpp
    struct S {
        template<typename = void> friend void f() {}  // ERROR

        // A definition
        template<typename = void> friend void f();    // OK
    };
    ```

## 12.3 模板实参

实例化模板时，模板形参由模板实参替换。这些实参可以通过几种不同的机制确定：

- **显式模板实参：** 模板名后可以跟用尖括号括起的显式模板实参。所得名字称为 *模板标识*。

- **注入类名：** 在具有模板形参 `P1`、`P2`、... 的类模板 `X` 的作用域内，该模板的名字（`X`）可以等价于模板标识 `X<P1, P2, ...>`。

- **默认模板实参：** 如果默认模板实参可用，则模板实例中可以省略显式模板实参。然而，对于类模板或别名模板，即使所有模板形参都有默认值，也必须提供（可能为空的）尖括号。

- **实参推导：** 未显式指定的函数模板实参可以从函数调用实参的类型推导出来。在调用中，这一点在第 15 章详细描述。推导也会在其他少数情形中进行。如果所有模板实参都可以被推导，则函数模板名后无需指定尖括号。C++17 还引入了从变量声明的初始化器或函数式类型转换中推导类模板实参的能力；讨论参见第 73 页 15.2 节。

### 12.3.1 函数模板实参

函数模板的模板实参可以显式指定、根据模板的使用方式推导，或作为默认模板实参提供。例如：

`detail/max.cpp`

```cpp
template<typename T>
T max (T a, T b)
{
    return b < a ? a : b;
}

int main()
{
    auto x = max<double>(1.0, -3.0);   // explicitly specify each
    auto y = max(1.0, -3.0);           // template argument is deduced
    auto z = max<int>(1.0, 2.0);       // explicit template argument
                                       // hence the result has type int
}
```

某些模板实参永远无法推导，因为其对应的模板形参未出现在函数形参类型中，或由于其他原因（见第 73 页 15.2 节）。对应的形参通常放在模板实参列表的开头，以便可以显式指定它们，而所有其他实参则进行推导。例如：

`detail/implicit.cpp`

```cpp
template<typename DestT, typename SrcT>
DestT implicit_cast(SrcT const& x)  // SrcT can be deduced
{
```

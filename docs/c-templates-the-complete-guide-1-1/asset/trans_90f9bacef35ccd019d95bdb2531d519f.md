
模板实参列表通常会通过用 A2 替换 T 而成功。反方向上，这第三个模板针对第一个模板的合成实参列表进行推导时，会通过用单元素序列 (A) 替换参数包 P 而成功。第一个和第三个模板之间的偏序通常会导致歧义。然而，一条特殊规则禁止最初来自函数参数包的实参（例如第三个模板的参数包 T...）匹配参数包（例如第一个模板的参数包）。

因此，第一个模板针对第三个模板的合成实参列表的模板推导失败，并且第一个模板被认为比第三个模板更特化。这条特殊规则实际上认为非可变参数模板（参数数量固定的模板）比其可变参数模板对应物更特化。

上述规则同样适用于函数签名中类型内出现的包展开。例如，我们可以将上一个示例中每个函数模板的参数作为实参包装进一个可变参数类模板 Tuple，从而得到一个不涉及函数参数包的类似示例：

details/tupleoverload.cpp

```cpp
template<typename... Ts> class Tuple
{
};

template<typename T>
int f(Tuple<T>)
{
    return 1;
}

template<typename... Ts>
int f(Tuple<Ts...>)
{
    return 2;
}

template<typename T, typename... Ts>
int f(Tuple<T, Ts...>)
{
    return 3;
}

int main()
{
    std::cout << f(Tuple<int, double>{});    // calls f
    std::cout << f(Tuple<int, double>{});    // calls f
    std::cout << f(Tuple<int>{});            // calls f
}
```

函数模板排序将 Tuple 的模板实参中的包展开视为类似于上一个示例中的函数参数包，从而产生相同的输出：

## 16.3 显式特化

函数模板的重载能力，结合用于选择“最佳”匹配函数模板的偏序规则，使我们能够为泛型实现使用特化模板，从而适当地使用代码以获得更高效率。然而，类模板和变量模板不能重载；相反，选择偏特化来实现类模板的透明定制：类模板的显式特化类似于函数模板特化。例如，程序员可能想为模板参数已完全替换的模板提供特化模板。不再保留模板参数。类模板、函数模板和变量模板都可以完全特化。

类模板中可以在类定义体之外定义的成员（即成员函数、嵌套数据成员和成员枚举类型）也可以完全特化。完整特化和偏特化在源代码中都同样“显式”，这就是我们在讨论中避免使用“显式特化”一词的原因。完整特化和偏特化都不会引入全新的模板或模板实例。相反，这些定制为已在泛型（或未特化）模板中隐式声明的实例提供替代定义。这是一个相对重要的实现观察，也是与重载模板的关键区别。

### 16.3.1 完整类模板特化

完整特化由三个记号序列引入：`template`、`<` 和 `>`。此外，类名后跟声明特化所用的模板实参。以下示例说明了这一点：

```cpp
template<typename T>
class S {
public:
    void info() {
        std::cout << "generic (S<T>::info())\n";
    }
};

template<>
class S<int> {
public:
    void info() {
        std::cout << "fully specialized (S<int>::info())\n";
    }
};
```

注意完整特化的实现不必以任何方式与泛型定义相关：这允许我们拥有不同名称的成员函数。然而，功能仅由类模板的名称决定。

指定的模板实参列表必须与模板形参列表对应。例如，为模板类型形参指定非类型值是非法的。然而，对于具有默认模板实参的形参，其模板实参是可选的：

```cpp
template<typename T> class Types {
public:
    using Type = int;
};

template<typename T, typename U = typename Types<T>::Type>
class S;

template<> class S<> {        // #1
};

template<> class S<int> {     // #2
public:
    void f();
};

template<> class S<char, char> {  // #3
};

int main()
{
    S<int> p;             // OK: uses #2, no definition needed
    S<int, int> q;        // ERROR: uses #1, but no definition available
    S<double> rv;         // OK: uses #2, definition available
    S<double, char> s;    // OK: uses #3
    S<char> e;            // ERROR: uses #3, but no definition available
}
```

正如示例还显示的，完整特化的声明（以及模板的声明）不一定必须是定义。然而，当声明了完整特化时，泛型定义绝不会用于给定的模板实参集合。因此，如果需要定义但未提供，程序就是错误的。对于类模板特化，有时“前向声明”类型是有用的，以便可以构造可能依赖的类型。在这方面，完整特化声明非常类似于普通类声明（它不是模板声明！）。唯一区别是语法，以及该声明必须匹配先前的模板声明。因为它不是模板声明，完整类模板特化的成员可以使用普通的类外成员定义语法定义（换句话说，不能省略 `template<>` 前缀）：

```cpp
template<typename T>
class S {
public:
    ...
};

template<> class S<char**> {
public:
    void print() const;
};
```

```cpp
template<>
void S<char**>::print() const
{
    std::cout << "pointer to pointer to char\n";
}
```

更复杂的例子可以强化这一概念：

```cpp
template<typename T>
class Outside {
public:
    template<typename U>
    class Inside {
    };
};
```

完整特化是对某个泛型模板实例化的替换，同一程序中同时存在模板的显式版本和生成版本是非法的。在同一文件中同时使用两者的尝试通常会被编译器捕获：

```cpp
template<typename T>
class Invalid {
};

Invalid<void> x1;       // causes the instantiation of Invalid<void>

template<>
class Invalid<void> {  // ERROR: Invalid<void> already
                        // instantiated
};
```

不幸的是，如果这发生在不同的翻译单元中，编译器可能无法捕获此问题。以下无效的 C++ 示例包含两个使用模板并调用许多实现的文件，但它是无效且危险的：

```cpp
// Translation unit 1:
template<typename T>
class Danger {
public:
    enum {
        max = 100
    };
};

char buffer[Danger<void>::max]; // use generic value

extern void clear(char*);

int main()
{
    clear(buffer);
}

// Translation unit 2:
template<typename T>
class Danger {
};

template<>
class Danger<void> {
public:
    enum { max = 100 };
};

void clear(char* buf)
{
    // mismatch in array bounds?
    for (int i = 0; i < Danger<void>::max; ++i) {
        buf[i] = 0;
    }
}
```

这个例子显然注定要保住它的衬衫，但它说明必须小心确保特化的声明对泛型模板的所有使用者可见。实际而言，这意味着特化的声明应在其头文件中紧随模板的声明。当泛型实现来自外部源，因而不应修改相应头文件时，这未必实际，但可能值得创建一个头文件，其中包含泛型模板，随后是特化的声明，以避免这些难以发现的错误。我们发现，一般而言，最好避免特化来自外部源的模板，除非它明确标记为为此目的而设计。

### 16.3.2 完整函数模板特化

（显式）完整函数模板特化背后的语法和原理……

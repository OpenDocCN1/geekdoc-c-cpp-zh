
# ISO/IEC 14882:2017(E)

```cpp
};
template<class T> void f(T t) {
  typename T::x;
  void foo() {
    A a;
    B b;
    f(b);
    f(a);
    // OK: T::X refers to the data member A::X
    // error: T::X is not permitted by the syntax of these constructs. — A::X
}

// end example;
```

- 5 一个限定名被用作类或 `decltype`（第 13 条）中的名称，或者被隐式地命名为类型，而没有使用 `typename` 关键字。在立即包含依赖于模板的嵌套限定符的嵌套限定符中，标识符或简单模板 ID 被隐式地命名为类型，而没有使用 `typename` 关键字。[注：不允许使用 `typename` 关键字]

- 6 如果对于给定的模板参数集，实例化了一个模板特化，其指向一个表示类型或类模板的限定标识符，则模板 ID 指向一个特化，该限定标识符应以 `typename` 为前缀，或者该限定标识符指向未知特化的成员，该限定标识符应以 `typename` 为前缀，或者在上述描述的隐式命名为类型的文中中使用。[示例：

```cpp
template<class T> void f(int i) {
  T::x =; // T::x 不能是一个类型
}

struct Foo {
  typedef int x;
};

struct Bar {
  static const x = 5;
};

int main() {
  f<Bar>(1);
  f<Foo>(1);
} // error: Foo::x 是一个类型
```

// end example;
```

- 7 在类模板的定义内，或在 `declator-or` 之后的类模板成员的成员中，当引用之前声明的表示类型或类模板的类模板成员名称时，不允许使用 `typename` 关键字。[注：此类名称可以使用未限定名 (6.4.1)、进入当前实例化 (17.6.2.1) 的类成员查找 (6.4.3.1)，或对当前实例化对象表达式类型查找 (17.6.2.2) 的类成员表达式查找 (6.4.5) 来找到。——示例：

```cpp
template<class T> struct A {
  typedef T B;
  // OK, 不需要 typename
};
```

// end example;
```

- 8 知道哪些名称是类型名称允许对每个模板的语法进行检查。如果满足以下，程序是格式错误的，不需要诊断：

(8.1) — 对于模板或 `constexpr pr` 的子语句无法生成有效的特化，如果在模板内状态- (9.4.1) 且模板未被实例化，或

(8.2) — 变长模板的每个特化都需要一个空的模板参数包，或

(8.3) — 紧跟在其定义之后的模板的假设实例化由于一个不依赖于模板参数的构造而导致格式错误，或

(8.4) — 此类构造在假设实例化中的解释与该模板的任何实际实例化中相应对应构造的解释不同。[注：这在实例化以下内容时可能会发生：

(8.4.1) — 在非依赖名称中使用的名称在模板定义点是不完整的，但在执行实例化点是完整的，或

(8.4.2) — 在模板定义中查找名称找到了 `using-declaration`，实例化中对应的作用域没有找到任何声明，因为该 `using-declaration` 是展开且对应的包是空的，或

(8.4.3) — 实例化使用了默认参数或默认模板参数，而这些参数在模板定义点尚未定义，或

(8.4) — 模板实例化内的常量表达式实例化 (8.20) 使用了

(8.4.1) — 整数或未转义枚举类型的 `const` 对象的值，或

(8.4.2) — `constexpr` 对象的值

(8.4.3) — 用的的值，或

(8.4.4) — `constexpr` 函数的定义，且该函数在模板定义时未被定义，或

(8.4.5) — 模板使用了由非依赖简单模板 ID 指定的类模板特化或变量特化，且它它是从一个在模板定义时未定义的部分特化实例化的，或者它命名了一个在模板定义时未声明的显式特化。——注]

否则，对于可以生成有效特化的模板，不应发布诊断。
[注：如果模板被实例化，将根据本文档中的其他规则进行诊断。——注] 示例：
具体何时诊断这些错误是一个实现质量问题。

```cpp
int;
template<class T> class X {
void f(T t, int i, char p) {
	t = i;           // 如果实例化了 X::f 且对 t 的赋值是错误，可能会被诊断
	p = 1;           // 如果没有实例化 X::i，可能会被诊断
	p = j;           // 如果没有实例化 X::f，可能会被诊断
}

void g(T t) {
	*;             // 如果没有实例化 X::g，可能会被诊断
}

template<class... T> struct A {
void operator++(int, T...) {
	} // error: 参数过多
}
tntemplate<class... T> union A : T... { };
                               // error: 带有基类的联合体
template<class... T> struct A : T... { T... { };
                               // error: 重复的基类
```

- end example|

- 9 在查找模板定义中使用的名称的声明时，非依赖名称使用通常查找规则 (6.4.1, 6.4.2)。依赖名称的查找推迟到模板参数已知 (17.6.2)。[示例：

```cpp
#include <iostream>
using namespace std;

template<class T> class Set {
    T p;
    int cnt;
public:
    Set();
    Set(const Set<T>& k);
    void print() {
        for (int i = 0; i<cnt; ++i)
            cout << p << "\n";
    }
};
```

在示例中，局部变量 `i` 在 `print` 中声明。然而，并不是每个声明都能以此方式找到；某些名称的解析推迟到模板参数已知。例如，尽管 `operator<<` 在 `print()` 的定义内是已知的且有声明，但 `print(i)` 需要的 `operator<<` 的实际声明直到 `T` 类型已知 (17.6.2)。——示例

- 10 如果一个名称不依赖于模板参数（如在 17.6.2 中定义），则声明（或一组声明）绑定到模板定义点。


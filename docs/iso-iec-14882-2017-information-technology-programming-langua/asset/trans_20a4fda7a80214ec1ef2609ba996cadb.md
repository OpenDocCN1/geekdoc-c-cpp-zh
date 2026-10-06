

# ISO/IEC 14882:2017(E)

每一个使用声明（using-declaration）都是一个声明，也是一个成员声明，因此可以在类定义中使用。[示例：
```cpp++
struct B {
    void f(char);
    void g(char);
    enum E { e };
    union { int x; };
};

struct D : B {
    using B::f;
    void f(int) f('c'); // 调用 B::f(char)
    void g(int) g('c'); // 递归调用 D::g(int)
};
 end example
```

在作为成员声明使用的使用声明中，每个使用声明的嵌套名限定符（nested-name-specifier）应当命名为所定义类的某个基类。如果使用声明命名了一个构造函数，则其嵌套名限定符应当命名为所定义类的直接基类。[示例：
```cpp++
template <typename bases>
struct X : bases {
    using bases::g;
};

nX<B, D> x;
 end example
```
```cpp
class C {
    int g();
};

class D2 : public B {
    using B::f; // OK: B 是 D2 的基类
    using B::e; // OK: e 是基类 B 的枚举成员
    using B::x; // OK: x 是基类 B 的联合体成员
    using C::g; // error: C 不是 D2 的基类
};
 end example
```

[注：析构函数没有名称，使用声明不能引用基类的析构函数；转换函数的成员模板特化不会通过查找找到，它们不被视为指定转换函数的使用声明 (17.5.2)。——注结束] 如果从基类到派生类的构造函数或赋值运算符具有与派生类的拷贝/移动构造函数或赋值运算符相同的签名 (15.8)，则基类的使用声明本身不会抑制派生类的隐式声明；成员会被派生类隐式定义的拷贝/移动构造函数或赋值运算符隐藏或覆盖，如下所示。

使用声明不应命名模板标识符（template-id）。[示例：
```cpp
template <class T> void f(T);
template <class T> struct X { 
};

struct B : A {
```
using A::f<double>;      // 错误
using A::X<int>;         // 错误
};
// end example[]
```

- 6 使用声明不应命名命名空间。

- 7 使用声明不应命名作用域内的枚举成员（scoped enumerator）。

- 8 命名类成员的使用声明应当是一个成员声明。[示例：

```
struct X {
    int i;
    static int s;
};

void f() {
    using X::i;              // error: X::i 是类成员，且此处不是成员声明。
    using X::s;              // error: X::s 是类成员，且此处不是成员声明。
}
// end example[]
```

- 9 由使用声明的成员可以像其他成员一样通过显式限定（explicit qualification）引用（6.4.3.2）。[示例：

```
namespace A {
    void gO();
}

namespace X {
    using A::f;               // 全局 f
    using A::g;               // A::g
}

void hO() {
    X::f();                  // 调用 ::f
    X::g();                  // 调用 A::g
}
// end example[]
```

- 10 使用声明是一个声明，因此可以在允许多个声明的地方（且仅在这些地方）重复使用。[示例：

```
namespace A {
    int i;
}
```

```
namespace A1 {
    using A::i, A::i;          // OK: double 声明
}
```

struct B {
    int i;
}

```
struct X : B {
    using B::B;
    // error: double 声明
};
// end example
```

- 11 [注：对于嵌套名限定符命名命名空间的使用声明，在声明之后添加的成员不在引入的声明集中，因此在使用该名称时不会被考虑。相反，默认函数 (11.3) 和模板特化 (17.5.5) 会被考虑。——注结束] 示例：

```
namespace A {
    void f(int);
}

using A::f; // f 是 A::f 的同义词，对于 A::f(int)。
namespace A {
    void f(char);
}

void foo() {
    f('a'); // 调用 f(int)，尽管存在 f(char)。
}
void bar() {
    using A::f;
    f('a'); // f 是 A::f 的同义词，对于 A::f(int) 和 A::f(char)。
// 调用 f(char)
// end example
```

- 12 [注：通过查找主模板并考虑所有特化来找到类模板。如果使用声明命名类模板，则声明之后引入的特化是可见的，因为主模板是可见的 (17.5.5)。——注结束]

- 13 由于使用声明是一个声明，对作用域内相同名称的限制 (6.3) 也适用于使用声明。[示例：
```
namespace A {
    int x;
}

namespace B {
    int i;
    struct g {
    };
    struct x {
    };
    void f(int);
    void f(double);
    void g(char);
}

void func() {
    int i;
    using B::i;
    void f(char); // error: 重复声明
    using B::f; // OK: 每个 f 都是函数
}
f(3.5);
  using B::f;
  g(); // 调用 f(double)
// 调用 B(char)
// 有类 B::g
// OK: 隐藏 x
```

struct B1 {
    B1(int);
};

struct B2 {
    B2(int);
};

```
struct D1 : B1, B2 {
    using B1::B1;
    using B2::B2;
};
D1 d1(o); // 错误：模糊
```

```
struct D2 : B1, B2 {
    using B1::B1;
    using B2::B2;
    D2(int);
};
D2 d2(0); // 调用 D::D2(int)
```
- end example --

16 为了重载解析解析的目的，通过使用声明引入到派生类的函数被视为派生类的成员。特别是，隐式的 `this` 参数被视为指向派生类的指针而非基类指针。这对函数的类型没有影响，在所有其他方面它仍然是基类的成员。同样，通过使用声明引入的构造函数在查找派生类的构造函数 (6.4.3.1) 或形成重载候选集 (16.3.15, 16.3.6, 16.3.17) 时，被视为派生类的构造函数。如果选择此类构造函数执行类类型对象的初始化，除了源基类以外的所有子对象都将进行隐式初始化 (15.6.3)。

17 在不命名构造函数的使用声明中，引入集合中的所有成员应该是可访问的。在命名构造函数的使用声明中不进行访问检查。特别是，如果派生类使用使用声明访问基类的成员，则该成员名称应该是可访问的。如果名称是重载成员函数的名称，则所有命名的函数都应该是可访问的。使用声明提到的基类应当在指定该声明的类的至少一个直接基类的作用域内是可见的。


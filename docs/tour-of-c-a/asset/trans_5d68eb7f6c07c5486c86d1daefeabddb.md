
如果你显式指定了某些默认值，其他的默认定义将不会生成。

当类拥有指针成员时，显式地定义拷贝和移动操作通常是一个好主意。这是因为指针可能指向类需要删除的内存，在这种情况下，默认的成员函数将是错误的。或者，指针可能指向类并不需要删除的内容。无论哪种情况，代码层面都应该知道这一点。例如，请参见 §6.2.1。

一个好的经验法则（有时被称为“零规则”）是要么定义所有的基本操作，要么一个都不定义（对所有操作使用默认）。例如：

点击此处查看代码

```cpp
struct Z {
  Vector v;
  string s;
};

Z z1; // Default initialize z1.v and z1.s
Z z2 = z1; // Default copy z1.v and z1.s
```

在这里，编译器将根据需要合成成员的默认构造、拷贝、移动和析构函数，并具有正确的语义。

使用 `=delete` 来补充 `=default`，指示不生成某个操作。类层次结构中的基类是一个不允许成员拷贝的经典例子。例如：

点击此处查看代码

```cpp
class Shape {
public:
  Shape(const Shape&)=delete; // No copying
  Shape& operator=(const Shape&)=delete;
  // ...
};

void copy(Shape& s1, const Shape& s2)
{
  s1 = s2; // Error: Shape copy is deleted
}
```

`=delete` 会使删除的函数成为编译错误；`=delete` 可以用于任何函数，而不只是基本成员函数。

## 6.1.2 转换

接受单个参数的构造函数定义了从其参数类型的转换。例如，complex (§5.2.1) 提供了一个从 `double` 的构造函数：

点击此处查看代码

```cpp
complex z1 = 3.14; // z1 becomes (3.14,0.0)
complex z2 = *z1; // z2 becomes z1*(2.0,0) == (6.28,0.0)
```

这种隐式转换有时是理想的，但并非总是如此。例如，Vector (§5.2.2) 提供了一个从 `int` 的构造函数：

点击此处查看代码

```cpp
Vector v1 = 7; // OK: v1 has 7 elements
```

这通常被认为是不利的，标准库中的 `vector` 不允许这种从 `int` 到 `vector` 的“转换”。

避免此问题的方法是说明只允许显式“转换”；即，我们可以这样定义构造函数：

点击此处查看代码

```cpp
class Vector {
public:
    explicit Vector(int s); // No implicit conversion from int to Vector
    // ...
};
```

这使得：

点击此处查看代码

```cpp
Vector v1 = 7; // OK: v1 has 7 elements
Vector v2 = 7; // Error: no implicit conversion from int to Vector
```

涉及转换时，更多像 Vector 这样的类型与 complex 类似，因此除非有充分理由，否则对接受单个参数的构造函数使用 `explicit`。

## 6.1.3 成员初始化

当类的成员被定义时，我们可以提供一个称为默认成员初始化器的默认初始化值。complex (§5.2.1) 的修订版：

点击此处查看代码

```cpp
class complex {
    double re = 0;
    double im = 0; // representation: two doubles with default value 0.0
public:
    complex(double r, double i) : re(r), im(i) {} // construct complex from two scalars: {r,i}
    complex(double r) : re(r) {} // construct complex from one scalar: {r,0}
    complex() {} // default complex: {0,0}
};
```

当构造函数没有提供值时，就会使用默认值。这简化了代码并帮助我们避免意外遗漏成员初始化。

## 6.2 拷贝和移动

默认情况下，对象是被拷贝的。这对于用户定义的类型以及内置类型都是如此。拷贝的默认含义是成员拷贝：拷贝每个成员。例如，使用 §5.2.1 中的 complex：

点击此处查看代码

```cpp
void test(complex z1)
{
    complex z2 (z1); // Il initialization
    complex z3;
    z3 = z2; // Il copy assignment
    // ...
}
```

现在 z1、z2 和 z3 具有相同的值，因为赋值和初始化都拷贝了两个成员。

当我们设计一个类时，必须始终考虑对象可能何时以及如何被拷贝。对于简单的具体类型，成员拷贝是拷贝的正确语义。对于复杂的复合类型（如 Vector），成员拷贝不是拷贝的正确语义；对于抽象类型，它几乎永远不是。

### 6.2.1 拷贝容器

当一个类是一个资源句柄时——也就是说，该类负责通过指针访问的对象——默认的成员拷贝通常是灾难性的。成员拷贝将违反资源句柄的不变性 (§4.3)。例如，默认拷贝将留下一个指向与原始对象相同元素的 Vector 副本：

点击此处查看代码

```cpp
void bad_copy(Vector v1)
{
    Vector v2 = v1; // Il copy
}
```

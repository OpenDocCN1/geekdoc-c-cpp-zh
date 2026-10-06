

# ISO/IEC 14882:2017(E)

```cpp
};
struct B : virtual A {
  virtual void fO();
};
struct C : B , virtual A {
using A::f;
};
```

```cpp
void foo() {
  C c;
  c.fO(); // calls B::f, the final overrider
  c.f(); // calls A::f because of the using-declaration
}
```

- 示例结束

```cpp
[示例:
struct A { virtual void fO(); };
struct B : A { };
struct C : A { void fO(); };
struct D : B, C { }; // OK: A::f and C::f are the final overriders
// 分别对应 B 和 C 子对象
```

- 示例结束

+ 3 虚成员函数并不一定需要重写，例如：
```cpp
struct B {
  virtual void fO();
};
struct D : B {
  void fint();
};
struct D2 : D {
  void fO();
};
```
类 D 中的函数 f(int) 隐藏了其基类中的虚函数 f()；D::f(int) 不是虚函数。然而，在 D2 中声明的 f() 与 B::f() 具有相同的名称和参数列表，因此它是一个虚函数，重写了函数 B::f()，即使 B::f() 在类 D2 中是不可见的。 — 注释结束

+ 4 如果类 B 中的虚函数被标记了虚函数限定符 final，并且在派生自 B 的类中函数 D : 重写了 B::f，则该程序是不符合形式的。[示例:
```cpp
struct B {
  virtual void fO() const final;
};
struct D : B {
  void fO() const; // D::f 尝试重写 final B::f
};
```
 注释结束

+ 5 如果虚函数被标记了虚函数限定符 override 且没有重写基类的成员函数，则该程序是不符合形式的。[示例:
```cpp
struct B {
  virtual void f(int);
};

```

```cpp
struct D : B {
    virtual void f(long) override; // 错误：重写 B::f 时签名错误
    virtual void f(int) override;  // OK
};

// 示例结束
```

尽管析构函数不继承，但派生类中的析构函数会重写在 15.4 和 15.5 中声明的基类析构函数。

重写函数的返回值可以是与被重写函数的返回值相同，也可以与函数的类保持协变。如果函数 D::f 重写了 B::f，当它们满足以下标准时，这些返回类型是协变的：

+ (7.1) 两者都是指向类的指针、类的引用，或指向类的值引用

+ (7.2) B::f 返回类型中的类与 D::f 返回类型中的类相同，或者是 D::f 返回类型中类的无歧义的直接基类

+ (7.3) 两个指针或引用都具有相同的类限定符，且 D::f 返回类型中的类类型与 B::f 返回类型中的类具有相同的类限定符

如果 D::f 协变类型中的类与 B::f 的类不同；则 D::f 的返回值在 D::f 声明处将是完整的，或者是类类型 D。当作为被重写函数的最终覆盖者调用重写函数时，其结果将转换为由（静态选择的）被重写函数返回的类型。示例：

```cpp
struct B {
    struct Base : private friend class Derived;
    virtual void vf1();
    virtual void vf2();
    virtual void vf3();
    virtual B* vf4();
    virtual B* vf5();
    void f0();
};

struct No_good : public Base {
    D* vf4(); // 错误：D（基类）不可访问
};

class A {
struct Derived : public Base {
    virtual void vf1();
    virtual void vf2(int);
    char* vf3(); // 错误：仅返回类型不同
    D* vf4(); // OK：返回派生类指针
    A* vf5(); // 错误：返回不完整类
    void f0();
};

void g0() {
    Derived d;
    Base* bp = &d; // 标准转换：
    Derived* to Base*
```

多级类指针或类引用是不允许的。

```cpp
bp->vf1();                          // 调用 Derived::vf1()
bp->vf2();                          // 调用 Base::vf2()
bp->f();                           // 调用 Base::f()（非虚）
B* p = dp->vf4();                   // 调用 Derived::pf() 且
                                   结果转换为 B*
Derived* dp = &d;                                // 
dp->vf2();                         // 不符合形式：参数匹配
```

[注：虚函数的解释取决于调用它的对象（动态类型），而非虚成员函数的解释仅取决于指针或引用（静态类型）（8.2）。 — 注释][注：虚指定了成员，因此虚函数不能是非成员（10.1）。在一个类中声明的虚函数可以在另一个类中声明为友元。 — 注释] 

一个在类中声明的虚函数应当在该类中声明，或者声明为纯（13.4），或者两者兼顾；不需要诊断（6.2）。示例：以下是具有多个基类的虚函数示例：

```cpp
struct A {
    virtual void f0();
};

struct B1 : A {\                   // 非虚派生
    void f0();
};

struct B2 : A {
    void f0();
};

struct D : B1, B2 {\               // D 有独立的 A 子对象
};

void foo() {
    D d;
    // A* b = &d; 不符合形式：歧义
    B1* bp = &d;
    A* ap = bp;
    D* dp = &d;

    ap->f();                         // 调用 D::B1::f
    dp->f();                         // 不符合形式：歧义
}

在上面的类 D 中有两个 A 的出现，因此有两个 A::f。B1::A::f 的最终覆盖者是 B1::f，B2::A::f 的最终覆盖者是 B2::f。 — 示例结束

# ISO/IEC 14882:2017(E)

```cpp
示例：以下示例显示了一个没有唯一覆盖者的函数：
struct A {
    virtual void f();
};

struct B1 : virtual A {\ // 虚派生
    void f();
};

struct B2 : virtual A {
    void f();
};

struct Error : B1, B2 {\ // 不符合形式
    struct Okay : B1, B2 {
        void f();
    };
```
B1::f 和 B2::f 都重写了 A::f，但在 Error 类中没有覆盖者。然而，这个示例是不符合形式的，因为 Okay::f 是最终覆盖者。 — 示例结束

```cpp
示例：以下示例使用了上述正确的类。
struct B1 : virtual A {}; // 未声明 f
struct Da : B1, B2 { };

void foo() {
    B1* vtap = new Da; // 调用 B2::f
    vtap->f();
}
```

使用作用域运算符（8.1）进行限定会抑制虚调用。 示例：
```cpp
class B : public { virtual void f(); };
class D : public B { public void f(); };

void D::f() { /* ... */ B::f(); };
```
在这里，对 D::f 的调用实际上调用的是 B::f 而不是 D::f。 — 示例结束

具有删除函数（11.4）的类不应重写一个删除定义的函数。同样，具有删除定义的函数不应重写一个具有删除定义的函数。通用概念（如形状）或更具体的变体（如圆形和正方形）实际上是可以使用的。抽象类还可以用于为派生类定义接口，以提供多种实现。 — 注释结束

抽象类是一种只能作为其他类的基类使用的类；除非它至少有一个纯虚函数，否则无法创建抽象类的对象。注：此类函数可能被继承：见下文。 — 注释结束。虚函数在类定义中的函数声明中使用纯函数限定符（12.2）指定为纯函数。一个

# 13.4 抽象内容

# ISO/IEC 14882:2017(E)

纯虚函数只有在带有限定 ID 语法（8.1）调用或如同（15.4）时才需要定义。示例：

```cpp
class point { /* ... */ };
// 抽象类
class shape {
    point center;
    public:
    shape() { return center; }
    void move(point p) {center=p; draw(); }
    virtual rotate(int) = 0; // 纯虚
    virtual draw() = 0; // 纯虚
};
```

-- 示例结束 [注：函数声明不能同时提供纯函数限定符和定义]: [示例:
```cpp
struct C {
    virtual void f() = 0; // 不符合形式
```
 示例结束

+ 3 抽象类不应作为参数类型、函数返回值或显式转换的类型。可以声明抽象类的指针和引用。示例：
```cpp
shape x;
shape* p; // 错误：抽象类对象
shape f(); // OK
void draw(shape); // 错误
shape b(shape); // 错误
``` 示例

+ 4 如果一个类包含或继承了至少一个最终覆盖者为纯虚函数的虚函数，则该类是抽象的。示例：
```cpp
class ab_circle : public shape {
    int radius;
    public:
    void rotate(int) {}
    //ab_circle::draw() 是纯虚
};
```
由于 shape::draw() 是纯虚函数，ab_circle::draw() 默认是纯虚。另一种声明，
class circle : public shape {
    int radius;
    public:
    void rotate(int) {}
    void draw(); // 某处需要定义
};
将使 circle 变为非抽象。 — 示例

+ 5 [注：抽象类可以派生自非抽象类，且纯虚函数可以重写非纯的虚函数。 — 注释]


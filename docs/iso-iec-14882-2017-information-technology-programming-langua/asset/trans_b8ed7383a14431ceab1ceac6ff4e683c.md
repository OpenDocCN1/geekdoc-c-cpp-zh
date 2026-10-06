

# ISO/IEC 14882:2017(E)

对普通 `aa` 的赋值是非形式的，因为该成员名在联合体外部是不可的，即使它是可见的，它也没有与任何特定对象关联。 — 示例结束 [注：无声明构造函数的联合体的初始化在 11.6.1 中描述。 — 备注结束]

- 4 联合体类（union-like class）是指联合体或一个具有匿名联合体作为直接成员的类。一个联合体类 X 拥有一组变体成员。如果 X 是一个类，则 X 中不是匿名联合体的非静态数据成员是 X 的变体成员。匿名联合体最多有一个变体成员具有默认初始化器。 — 示例：

```
union U {
int z = 0;
union {
int k;
union {
int y = 1; // 初始化 U 的第二个变体成员
};
};
```
— 示例结束

12.4 局部类声明 [class.local]

- 1 可以在函数定义内部声明类；此类类被称为局部类。局部类的名称对于它的作用域是局部的。局部类位于封装函数的作用域内，并与封装函数对非静态变量具有相同的访问权限。局部类中的声明不使用（6.2）封装作用域中的变量。 — 示例：

```
int x;
void f() {
static int s;
int x;
const int N = 5;
extern q();

struct local {
int g() { return x; } // 使用 x
int h() { return s; } // OK
int k() { return q(); } // OK
int l() { return q(); } // OK
int m() { return N; } // OK
}
local* p = 0; // 局部：不在作用域
```
— 示例结束

- 2 封装函数访问局部类的成员；它遵循访问规则（第14节）。局部类的成员函数应在其定义内部定义。

- 3 如果 X 是类，局部类 Y 可以在类 X 中声明并在类 X 的定义中或类 X 相同的作用域内定义。嵌套在局部类中的类是局部类。

- 4 局部类不应有静态数据成员。

13 派生类 [class.derived]

- 1 类定义可以使用以下符号指定基类列表：
base-class:
  - base-specifier-list
base-specifier-list:
  base-specifier ...
  base-specifier-list, base-specifier ...opt
base-specifier:
  attribute-specifier-seq_opt class-or-detype
  attribute-specifier-seq_opt virtual access-specifier_opt class-or-detype
  attribute-specifier-seq_opt virtual access-specifier class-or-detype
class-or-detype:
  nested-specifier_opt class-name
  nested-specifier_opt template simple-template-id
  detype-specifier:
access-specifier:
  private
  public

- 2 可选属性表示一个未完全定义的类（第12节）。由 base-specifier 的 class-detype 指出的类是所定义类的基类。如果在查找 D 的基类时未找到名称，则忽略非类型名称（6.3.10）。如果 B 是 D 的基类，且它是 D 的直接基类，则称其（直接或间接）派生自其基类。如果一个类是基类但不是直接基类，则它是间接基类。[注：参见第14节关于访问说明符的含义。] 未在派生类中声明的成员也被视为派生类的成员。除构造函数外的基类成员由派生类继承。类的构造也可以被继承（10.3.3）。如果在表达式中引用的名称与派生类的成员相同，它们的名称会被隐藏或产生（13.2）。[注：作用域运算符 :: (8.1) 可引用直接或间接基类成员。这允许访问在派生类中重新声明的名称。派生类本身可以作为受访问控制的基类；参见14.2。指向派生类的指针可以隐式转换为无歧基类的引用（11.6）。 — 备注结束

- 3 基类列表指定派生类型对象中所包含的基类子对象的类型。[示例：]

```
struct Base {
  int a, b, c;
};

struct Derived : Base {
  int b;
};
```

```
struct Derived2 : Derived {
    int c;
};
```

在这里，类 Derived2 的对象将拥有一个 Derived 子对象，而 Derived 又将拥有一个 Base 子对象。 — 示例结束

- 4 基类说明符后跟省略号（17.5.3）。

- 5 基类对象在最派生对象中分配的顺序 [注：派生类及其基类子对象可以用有向无环图（DAG）表示，其中箭头表示“直接派生自”。箭头不需要在内存中具有物理表示。子对象的 DAG 通常被称为“子对象格](img/feea898746c066176386930de0105d_267.png) 

- 6 [注：基类的初始化可以在构造函数中指定；参见 15.2。基类子对象的布局（6.7）可能与大多数派生对象的布局不同。基类子对象的多态行为（15.7）可能与同类型的大多数派生对象的多态行为不同。基类子对象的大小（第12节）可能不同；然而，对于派生对象，相同类型的子对象必须位于相同的地址。 — 备注结束]

13 多重基类 [class.mi]

- 1 类可以派生自任意数量的基类。[注：多个直接基类被称为继承。 — 备注结束]:[示例：]

```
class A { /* ... };
class B { /* ... };
class C { /* ... };
class D : public A, public B, public C { /* ... };
```

- 3 类不应多次作为派生类的直接基类。[注：类可以多次作为间接基类，且作为直接基类时是有效的。4.5 直接基类的成员在封装函数的作用域内是有效的。然而，静态成员、枚举类型是可以引用的。 — 备注结束]:[示例：]

```
class X { /* ... };
class Y : public X, public X { /* ... }; // 错误

```

```
class L : public int next; /* ... */ };
class A : public L { /* ... };
class B : public L { void f0(); /* ... }; // OK
class C : public A, public L { void f0(); /* ... }; }; // OK
```
— 示例结束

- 4 不包含 virtual 关键字的基类说明符指定非虚基类。包含 virtual 关键字的基类说明符指定虚基类。对于派生类类格中的每个不同的非虚基类，派生类应包含相应的基类子对象。对于每个不同的虚基类，派生类应包含一个单一的基类子对象。

- 5 [注：对于类 C 的对象，C 格中每个不同的（非虚）基类 L 与类型 C 对象内部的每个 L 一一对应。给定上述类 C，类 C 的对象将有两个 L 子对象，如图 3 所示。](img/feea898746c066176386930de0105d_268_0.png)

图 3 — 非虚

在这种图中，可以使用显式限定来指定哪个子对象。函数 C::f 的体可以引用每个 L 子对象的成员 next：

```
void C::f() { A::next = B::next; }; // OK
```

如果没有 A:: 或 B:: 限定符，上述 C::f 的定义将因为歧义（13.2）而是非形式。[注：相比之下，考虑具有虚基类的情况：]

```
class V { /* ... */; };
class A : virtual public V { /* ... */; };
class B : virtual public V { /* ... */; };
class C : public A, public B { /* ... */; };
```](img/feea898746c066176386930de0105d_268_1.png)

图 4 — 虚基

对于类型 C 的对象，单一的 V 子对象被每个基类子对象共享




# ISO/IEC 14882:2017(E)

如 10.3.1.2) 所示。此类重声明与原始声明具有相同的嵌套命名空间。

```cpp
Example:
namespace Q {
    namespace V {
        void f();
        class C { void m(); } // 嵌套命名空间为全局命名空间、Q 和 Q::V
    }
    namespace V:f {
        external void h(); // 嵌套命名空间为全局命名空间、Q 和 Q::V
    }
    namespace V::C::m() { // 嵌套命名空间为全局命名空间、Q 和 Q::V
    }
}
```

- 示例

+ 5 如果在特定命名空间的命名空间定义出现了可选的 `inline` 关键字，则其被声明为内联命名空间（inline namespace）。只有当 `inline` 关键字之前已经在最初声明该命名空间名称的命名空间定义中使用，它才能在扩展命名空间的命名空间定义中使用。

+ 6 命名空间定义中使用的可选属性指定符序列（attribute-specifier-seq）对于正在定义或扩展的命名空间是可见的。

+ 7 内联命名空间的成员的使用方式就像它们是嵌套命名空间的成员一样。具体而言，每当其中一个被使用时，该内联命名空间及其嵌套命名空间都会被添加到用于依赖相关查找（6.2）的关联命名空间集中；并且使用指令（10.3.4）会将内联命名空间插入到嵌套命名空间中，类似于匿名命名空间（10.3.11）。此外，内联命名空间的每个成员都可以被部分特化（17.7.5）、显式实例化（17.7.2）或显式特化（17.7.3），就像它是嵌套命名空间的成员一样。最后，通过显式限定（6.4.3.2）在嵌套命名空间中查找，即使嵌套命名空间存在同名的声明，也会包含内联命名空间的成员。

这些属性具有传递性：如果命名空间 N 包含一个内联命名空间 M，那么 M 的成员可以像它们是 M 或 N 的成员一样使用。N 的内联命名空间集是 N 中所有内联命名空间的集合。O 的嵌套命名空间集是包含 O 的直接非内联命名空间，以及任何中间命名空间的集合。

+ 9 具有嵌套命名空间限定符 E、标识符 I 和命名空间正体 B 的嵌套命名空间定义等同于
```cpp
Example:
namespace E { namespace I { }
```
上述代码的效果等于：
```cpp
namespace A {
    namespace B {
        namespace C {
            int i;
        }
    }
}
```

## 10.3.1.1 匿名命名空间

匿名命名空间定义的行为就像被替换为：
```cpp
inline namespace unnamed { /* 空正体 */
using namespace unnamed;
```
其中 `inline` 出现，且仅当它出现在匿名命名空间定义中，并且翻译单元中 `inline` 的所有出现处都被替换为相同的标识符，且该标识符与翻译单元中的所有其他标识符不同。示例：

```cpp
namespace A {
  int i; // unnamed::i
  void f() { i++; }; // unnamed::i
}
namespace A {
  namespace {
    int i; // unnamed::i
    int j; // unnamed::j
  }
  void g() { i++; }; // unnamed::i
}
using namespace A;
void h() {
  i++; // error: unnamed::i
  A::i++; // unnamed::i
  j++; // unnamed::j
}
```

## 10.3.1.2 命名空间成员定义

+ 命名空间 M 中的声明（不包括嵌套作用域中的声明），其声明符 ID（declarator-id）为未限定标识符（11.3），其类名（1.2）或枚举名（10.2）是一个标识符，或者其详述类型指定符采用 `class-specifier-seq identifier`（10.7.3）的形式，则将其未限定标识符声明（或重新）为 M 的成员。[注：模板的显式实例化（17.7.2）或显式特化（17.7.3）不会引入名称，因此如果主模板声明在匿名命名空间中，则可以使用未限定标识符。—— 注释结束] 示例：

```cpp
namespace X {
  void f() { /* ... */ }; // OK 引入 X::f()
```

```cpp
namespace M {
  void g() {
    using M::g(); // OK 引入 X::M::g()
    void g();
  } // error: 与 X::M::g() 冲突
}
```

+ 具名命名空间的成员也可以通过对所定义名称进行显式限定（6.4.3.2）在该命名空间之外定义，前提是所定义的实体已经在命名空间中声明，且该定义出现在包含该声明的命名空间中该声明声明点之后。示例：

```cpp
namespace Q {
    namespace V {
        void f();
        void V::f() { /* ... */ } // OK
        void V::g() { /* ... */ } // error: g() 尚未是 V 的成员
        namespace V {
            void g();
        }
    }
}
namespace R {
void V::g() { /* ... */ } // error: g 没有包含 Q
}
```

如果非局部类中的友元声明了类、函数、类模板或函数模板，则该友元是内内嵌套命名空间的成员。友元声明并不会使名称对查找（6.4.1）不可见 [注：如果在命名空间作用域内提供了匹配的声明（在命名空间之前或之后）] 。如果调用了函数或函数模板，它将通过依赖相关查找（6.4.3）被找到。如果友元声明是未限定的，则在命名空间作用域内被考虑。[注：仅如此声明。—— 注释结束] 示例：

```cpp
// 假设 f 和 g 尚未声明。
template <class T>
void f2(T);
namespace A {
class X {
    friend void f(X); // A::f(X)
    class V {
        friend void g(); // A::g
        friend void h(int); // A::h
    }
    friend void f2<int>; // A::f2<int>
};
```

```cpp
using A;
void h() {
  i++; // error: A::i
  A::i++; // A::i
  j++; // A::j
}
```

## 10.3.2 命名空间别名

+ 1 命名空间别名根据以下语法为命名空间声明替代名称：
namespace-alias:
  identifier
namespace-alias-definition:
  namespace-alias identifier = qualified-namespace-specifier;
qualified-namespace-specifier:
  nested-name-specifier namespace-name

+ 2 命名空间别名定义中的标识符是限定命名空间指定符所指示的命名空间的别名，并成为别名。[注：在命名空间定义中查找命名空间名称时，仅考虑命名空间，参见 6.4.6。]

+ 3 在声明区域内，可以使用命名空间别名重定义该区域内定义的命名空间别名，以指向它引用的命名空间。[示例：以下声明是良好的：
namespace Company_with_long_name { /* ... */
namespace CWLN = Company_with_long_name;
namespace CWLN = Company_with_long_name; // OK 重复

## 10.3.3 使用声明

+ using-declaration:
  using-declaration-list:
    using-declarator ...
    using-declarator ... opt
using-declarator:
  typename_opt nested-name-specifier unqualified-id

+ 1 `using-declaration` 中的每个 `using-declaration` 都会在其出现的声明区域引入一组声明。引入的声明集合通过在 `using-declaration` 中执行名称查找找到，但排除下文所述的隐藏函数（6.6.3, 13.2）。如果 `using-declaration` 未命名构造函数，则未限定标识符在声明区域中声明为 `using-declaration` 引入的每个声明的同义词。[注：仅如此声明。如果在使用声明中声明枚举名，不会在声明声明区域中声明其枚举成员。—— 注释结束] 如果 `using-declaration` 命名了构造函数，则声明该类继承 `using-declaration` 引入的构造函数声明集。

> (98) 包含多个 `using-declaration` 的 `using-declaration` 等同于相应的每个 `using-declaration` 序列。


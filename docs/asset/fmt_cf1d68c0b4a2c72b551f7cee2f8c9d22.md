
`template<class T> void f(T);      // declaration`

```cpp
void g() {
    f("Annemarie");                   // 调用 f<const char*>
}
```

+   即使在调用点模板 **`f`** 仅有声明而未定义，对 **`f`** 的调用也是良好的。除非在某个翻译单元中存在对 **`f<const char*>`** 的特化（无论是隐式生成还是显式生成），否则程序将是违反规范的。 — *cnd example*

§ 14.8.3

# ISO/IEC 14882:2011(E)

# 15 异常处理 [except]

1 异常处理提供了一种从线程执行某一点到先前由执行流传递的异常处理程序传递控制和信息的方法。只有当在处理程序的 try 块中执行的代码触发 throw 表达式，或者在从处理程序的 try 块调用的函数中执行的代码触发 throw 表达式时，才会调用处理程序。

```cpp
try-block:
try compound-statement handler-seq

function-try-block:
try clor-initializer-opt compound-statement handler-seq

handler-seq:
handler-seq-opt

handler:
catch ( exception-declaration ) compound-statement

exception-declaration:
attribute-specifier-seq-opt type-specifier-seq declarator
attribute-specifier-seq-opt type-specifier-seq abstract-declarator-opt
```

...
`tthrow-expression:`
在 `exception-declaration` 中的 `throw attribute-specifier-seq` 涉及子句选项 (15.3) 的形式参数。

+   2 `try-block` 是一个语句（第 6 节）。`throw-expression` 是 void 类型。执行 `throw-expression` 的被称为“抛出异常”；随后获得控制的代码被称为“处理程序”。[注：在本节中，“try block”同时指代 `try-block` 和 `function-try-block`。] -- 注释结束

+   3 不得使用 `goto` 或 `switch` 语句将控制转移到 `try block` 或处理程序内部。

```cpp
示例:
void f() {
goto 11; // 违反规范
goto 12; 
try {
goto 11; // OK
goto 12; // 违反规范
11;
} catch (...) {
goto 12;
goto 11; // 违反规范
goto 12; // OK
}
```
```

示例| `goto`、`break`、`return` 或 `continue` 语句可用于控制转移出 `try block` 或处理程序。当这种情况发生时，`try block` 中声明的所有变量都将在直接包含其声明的上下文中被销毁。[示例:

```cpp
lab: try {
  T1;
  try {
    T2;
    if (condition) {
      goto lab;
    } catch(...) { /* handler 2 */ }
  } catch(...) { /* handler 1 */ }
```
```

在此处，执行 `goto lab` 将销毁 `t2, t1`，假设 `condition` 没有声明变量。在销毁 `t2` 期间的任何异常将导致执行 `handler 2`；在销毁 `t1` 期间的任何异常将导致执行 `handler 1`。 — 示例结束

`function-block` 将 `handler-seq` 与 `ctor-initializer`（如果存在）以及 `compound-statement` 关联。在 `compound-statement` 执行期间抛出的异常，或者在类子对象的初始化或析构期间对应的构造函数和析构函数抛出的异常，其控制转移到 `function-block` 中处理程序的方式，与 `try-block` 执行期间抛出的异常转移到其他处理程序的方式相同。示例：

```cpp
int f(int);
class C {
  int i;
  double d;
  public:
  C(int, double);
};
::C(int ii, double id) 
try : i(ii), d(id)
  // 构造函数语句
} catch (...) {
  // 处理从 ctor-initializer 
  // 以及从构造函数语句抛出的异常
}
```

示例结束

# 15.1 抛出异常 [except.throw]

抛出异常将控制转移到处理程序。传递一个对象，对象的类型决定了哪些处理器可以捕获它。[示例:

```cpp
throw "Help!";
```
```

可以被 `const char*` 类型的处理程序捕获：

```cpp
try {
  ...
} catch(const char* p) {
  // 处理字符串异常的处理器
}
```

以及

# ISO/IEC 14882:2021(E)

```cpp
class Overflow {
public:
    Overflow(char,double,double);
};
void f(double x) {
    throw Overflow('+',x,3.45e107);
}
```

可以作为除 `Overflow` 类型外异常的处理器

```cpp
try {
    f(1.2);
} catch(Overflow& oo) {
    // 处理 Overflow 类型的异常
```
```
// 示例结束

+   2. 当抛出异常时，控制转移到类型匹配的最近处理器 (15.3)；“最近”意味着控制流最近进入且尚未退出的、try 关键字之后的 `compound-statement` 或 `ctor-initializer` 对应的处理器。

+   3 `throw-expression` 创建一个临时对象，其析构通过从 `throw` 操作数的静态类型中移除任何顶层限定符并转移到最近的处理器，并将类型从 “T” 分别调整为“返回 T 的函数”或“返回 T 的指针”。该类型是至关重要的，并用于初始化匹配处理器中的变量 (15.3)。如果异常对象的类型将是不完整类型或指向不完整类型的指针（可能是 cv-void），则程序是违反规范的。除了这些限制以及 15.3 中提到的类型限制外，`throw` 的操作数被视为视为调用 (5.2.2) 中的函数参数或 `return` 语句的操作数。

+   4. 异常对象的内存也以不确定的方式分配，如 3.7.4 所示。如果存在重抛的处理器，控制转移到另一个相同异常的处理器。在最后一个处理器处于活跃状态时，或在类型为 *exception_ptr* (18.8.5) 的对象之后，异常对象被销毁。在后一种情况下，当处理器退出时，立即在 `exception-declaration` 中声明的对象的销毁后，发生析构。

+   5. 异常对象的内存也以不确定的方式分配，如 3.7.4.1 所示。如果存在重抛的处理器，控制转移到另一个相同异常的处理器。在最后一个处理器处于活跃状态时，或在类型为 *exception_ptr* (18.8.5) 的对象之后，异常对象被销毁。在后一种情况下，当处理器退出时，立即在 `exception-declaration` 中声明的对象的销毁后，发生析构。

等等，我注意到提供的 OCR 文本末尾有很多重复内容和乱码文本（例如 "0 {}" 和重复的段落）。我将根据 C++ 标准片段的逻辑流提供一个干净、修正后的版本。

让我们仔细检查 OCR 文本以去重并修复流程：

```cpp
struct C {
C() {}
C(const C& k) : {};
};
int main() {
    try {
        throw C(); // 调用 std::terminate()
    } catch(C) {}
}
```

+   无操作数的 `throw-expression` 重抛当前处理的异常；不创建新的异常对象。`std::uncaught_exception()` 的值为真。

+   如果当前没有处理存储期，执行无操作数的 `throw-expression` 将调用 `terminate()` (15.5)。

# 15.2 构造函数和析构函数 [except.ctor]

+   当控制从 `throw-expression` 转移到处理器时，对 block 构建的所有自动对象按照构造完成的反序调用析构函数。

+   任何存储期的对象的初始化或析构被异常终止，都将对其所有完全构造的对象（排除类联合类的成员）执行析构函数，即对于主构造函数 (12.6.2) 已执行且析构函数尚未开始的对象。同样，如果非分配构造函数因异常退出，对象的析构函数将被调用。如果对象是在 `new-expression` 中分配的，则调用匹配的释放函数 (3.7.4.2, 5.3.4, 12.5) 以释放对象占据存储。

+   从 block 到 throw block 对栈上构建的自动对象调用析构函数的过程被称为“栈回溯”。如果在回溯期间析构函数因异常退出，则调用 `terminate` (15.5.1)。[注：析构函数应该捕获异常而不让它们传播出析构函数。]

# 15.3 处理异常 [except.handle]

+   处理器中的 `exception-declaration` 描述了导致进入器的异常类型。`exception-declaration` 不指示不完整类型、抽象类类型或右值引用类型。`exception-declaration` 不指示不完整类型的指针或引用，`void*`、`const void*`、`volatile void*` 或 `const volatile void` 除外。

# ISO/IEC 14882:2011(E)

2 类型为 "array T" 或 "返回 T 的函数" 的处理器分别被调整为 "指向 T 的指针" 或 "指向返回 T 的函数的指针"。

3 处理器是类型为 E 的异常对象的匹配项

- 处理器类型为 cv T 或 cv TK，且 E 与它们为相同类型（忽略顶层 cv 限定符），或者
- 处理器类型为 cv T 或 cv TK，且 E 是 E 的一个明确的公共基类，或者
- 处理器类型为 cvT+ 且 E 是指针类型，可以通过以下一种或两种或两种方式转换为处理器的类型：

  - 标准转换 (4.10)，且不涉及转换为指向私有类或歧义类的指针的转换
  - 限定符转换

- 处理器是指针或成员类型，且 E 为 `std::nullptr_t`，

> [注：操作数为整数类型且求值结果为零的表达式的抛出表达式没有指针或成员类型的处理器。—— 备注结束]

示例：

```cpp
class Mather { /* ... */ virtual void vf();
class Overflow: public Mather { /* ... */ };
class Underflow: public Mather { /* ... */ };
class Zeroverride: public Mather { /* ... */ };
void f() {
  try {
    g();
  } catch (Overflow oo) {
    // ...
  } catch (Mather mm) {
    // ...
  }
}
```

在这里，`Overflow` 将捕获类型为 `Overflow` 的异常，而 `Mather` 处理器将捕获类型为 `Mather` 的异常以及 `Mather` 公共声明的所有类型，包括类型为 `Underflow` 和 `Zeroverride` 的异常。—— 示例结束

4 `try` 块的处理器按照出现的顺序进行尝试。这使得通过在对应基类的处理器之后放置派生类的处理器，来写出永远不会执行的处理器成为可能。

5 异常声明函数中的 ... 作用与函数声明中的 ... 类似；它指定了对任何异常的匹配。如果存在， ... 处理器应当是其 `try` 块的最后一个处理器。

6 如果在 `try` 块的处理器中没有找到匹配项，则匹配处理器的搜索将在线程的动态展开的 `try` 块中继续。

7 直到 `catch` 语句的形式参数（如果有）的初始化完成，处理器才被认为是活跃的。[注：栈已展开或在该点展开。—— 备注结束] 当通过 `throw` 引入 `std::terminate()` 或 `std::unexpected()` 时，隐含处理器是活跃的。当 `catch` 语句退出或当 `std::unexpected()` 在进入 `throw` 后退出时，处理器不再被认为是活跃的。

§ 15.3

最近激活的处理器的异常仍然活跃，被称为当前处理的异常。

如果未找到匹配的处理器，将调用函数 `std::terminate()`；在此处调用 `std::terminate()` 之前是否展开栈取决于实现 (15.5.1)。

在对象构造函数或析构函数的 `function-try-block` 处理器中引用该对象的任何非静态成员或基类会导致未定义行为。

在进入构造函数或析构函数的 `function-try-block` 处理器之前，应当销毁对象完全构造的类和成员。同样，对于带有来自对象非委托构造函数的异常的对象，在其析构函数执行完毕后，在进入该对象构造函数的 `function-try-block` 处理器之前，应当执行该对象的析构函数。在进入该对象析构函数的 `function-try-block` 处理器之前，应当销毁对象的基类和非变成员 (12.4)。

函数或构造函数参数的作用域和生命周期延伸到 `function-try-block` 处理器中。

由静态存储期对象或在具有静态存储期的命名空间范围对象的构造函数中抛出的异常无法被 `main()` 的 `function-try-block` 捕获。在具有存储期的对象的析构函数中或在具有存储期的命名空间范围对象的构造函数中抛出的异常不会被线程初始函数的 `function-try-block` 捕获。

如果在构造函数的 `function-try-block` 处理器中出现 `return`语句，则程序是格式错误的（ill-formed）。

如果控制到达构造函数或析构函数的 `function-try-block` 的末尾，则重新抛出当前捕获的异常。否则，当控制到达 `function-try-block` 处理器的末尾时，返回一个值 (6.6.3)。结束 `function-try-block` 等同于无值的返回；这在返回值的函数中会导致未定义行为 (6.6.3)。

如果异常规范指定了一个名称，它声明了一个从异常对象进行拷贝初始化 (8.5) 的变量。如果异常规范表示一个对象类型但未指定名称，则一个临时对象 (12.2) 从异常对象进行拷贝初始化 (8.5)。该变量或临时对象的生命周期在处理器退出时结束，在处理器内初始化的任何对象销毁之后。

当处理器声明一个非 `const` 对象时，对该对象的任何更改都不会影响由异常表达式初始化的临时对象。当处理器声明对非 `const` 对象的引用时，对所引用对象的任何更改都将作用在抛出表达式初始化的临时对象上，并产生该对象被重新抛出的效果。

# 15.4 异常规范

函数声明通过使用异常规范作为其声明符的后缀，列出其函数直接或间接抛出的异常。

```cpp
exception-specification:
  dynamic-exception-specification
  noexcept-specification
```

```cpp
dynamic-exception-specification:
  throw { type-list }
```

```cpp
type-list:
  type-id [, type-id ... ]
```

```cpp
noexcept-specification:
  noexcept
```

异常规范仅出现在函数类型、指针函数类型或引用成员函数的函数声明符上。异常规范不出现在 `typedef` 声明或别名声明中。[示例：

```cpp
void f() throw(int); // OK
void (*fp)() throw(int); // OK
void (*g)(); // OK
typedef f throw(int); // 格式错误
```

异常规范不表示完全类型。异常规范中指定的类型不表示指向不完全类型、`void*` 或 `volatile*`。异常规范中指定的 cv T、“数组 T”、“返回 T”分别调整为 T、“指向 T”、“指向返回 T”。两个异常规范在满足以下条件时是兼容的：

- 两者均为非 `noexcept`（常量表达式），且无论形式如何，常量表达式是等价的，或者
- 两者均为具有相同调整类型的动态异常规范。

如果函数的任何声明具有非 `noexcept` 规范的异常规范，则该函数的所有声明（包括定义和任何显式特化）都应具有兼容的异常规范。如果指针、函数引用或成员函数指针的声明具有异常规范，则该声明的所有出现处都应具有兼容的异常规范。可以指定异常规范，但不是要求的。如果在显式实例化声明中指定了异常规范，它应当与该函数其他声明的异常规范兼容。只有当异常规范在单个编译单元内不兼容时才需要诊断。

如果虚函数具有异常规范，则任何派生类中覆盖该虚函数的任何声明（包括定义）都应仅允许基类函数异常规范允许的异常。[示例：

```cpp
struct B {
  virtual void f() throw(int, double);
  virtual void g();
};
```

```cpp
struct D : B {
  void f(); // 格式错误
  void g() throw(int); // OK
};
```

`D::f` 的声明是格式错误的，因为它允许所有异常，而 `B::f` 仅允许 `int` 和 `double`。—— 示例结束

限制应用于指针的赋值和初始化。

函数、成员函数指针以及函数引用：目标实体在赋值或初始化中应至少允许源值所允许的异常。[示例：

```cpp
class A { /* ... + */; };
```



```
auto bind = [](auto m) {
    return [=](auto fvm) { return fvm(m()); };
};
```
// OK to capture objects with automatic storage duration created during constant expression evaluation.

```
static_assert(bind(monad(2))(monad() == monad(2()));
```
— end example]

— end note]

-   (5.14) — 从类型 cv void* 到指针到对象类型的转换；
-   (5.15) — 一个 reinterpret_cast (7.6.1.10)；
-   (5.16) — 一个对象的修改 (7.6.19, 7.6.1.6, 7.6.2.3)，除非它应用于引用在 E 的求值期间开始生命周期的非易失性字面量类型的非易失性左值；
-   (5.17) — 一个 new-expression (7.6.2.8)，除非所选的分配函数是可替换的全局分配函数 (17.6.3.2, 17.6.3.3) 并且在 E 的求值期间已释放所分配的存储；
-   (5.18) — 一个 delete-expression (7.6.2.9)，除非它释放了在 E 的求值期间分配的存储区域；
-   (5.19) — 对 std::allocator<T>::allocate 的实例的调用 (20.10.10.2)，除非在 E 的求值期间已释放所分配的存储；
-   (5.20) — 对 std::allocator<T>::deallocate 的实例的调用 (20.10.10.2)，除非它释放了在 E 的求值期间分配的存储区域；
-   (5.21) — 一个 await-expression (7.6.2.4)；
-   (5.22) — 一个 yield-expression (7.6.17)；
-   (5.23) — 一个结果未指定的三路比较 (7.6.8)、关系 (7.6.9) 或相等 (7.6.10) 运算符；
-   (5.24) — 一个 throw-expression (7.6.18) 或一个会抛出异常的 dynamic cast (7.6.1.7) 或 typeid (7.6.1.8) 表达式；
-   (5.25) — 一个 asm-declaration (9.10)；或
-   (5.26) — 对 va_arg 宏的调用 (17.13.2)。

如果 E 满足核心常量表达式的约束，但 E 的求值会求值第 16 条到第 32 条中指定的具有未定义行为的操作，或对 va_start 宏 (17.13.2) 的调用，则 E 是否为核心常量表达式是不确定的。

[Example 3:

```
int x;                         // not constant
struct A {
    constexpr A(bool b) : m(b?42:x) { }
    int m;
};
constexpr int v = A(true).m;       // OK: constructor call initializes m with the value 42

constexpr int w = A(false).m;      // error: initializer for m is x, which is non-constant

constexpr int f1(int k) {
    constexpr int x = k;           // error: x is not initialized by a constant expression
                                 // because lifetime of k began outside the initializer of x
    return x;
}
constexpr int f2(int k) {
    int x = k;                     // OK: not required to be a constant expression
                                 // because x is not constexpr
    return x;
}

constexpr int incr(int &n) {
    return ++n;
}
```

```
constexpr int g(int k) {
    constexpr int x = incr(k);    // error: incr(k) is not a core constant expression
                               // because lifetime of k began outside the expression incr(k)
    return x;
}
constexpr int h(int k) {
    int x = incr(k);             // OK: incr(k) is not required to be a core constant expression
    return x;
}
constexpr int y = h(1);          // OK: initializes y with the value 2
                               // h(1) is a core constant expression because
                               // the lifetime of k begins inside h(1)
```
— end example]

6 为了确定表达式 E 是否为核心常量表达式，对 20.10.10.2 中定义的 std::allocator<T> 的成员函数的调用，其中 T 是字面量类型，不会使 E 不能成为核心常量表达式，即使此类调用的实际求值否则会违反核心常量表达式的要求。同样，对 std::destroy_at、std::ranges::destroy_at、std::construct_at 或 std::ranges::construct_at 的调用不会使 E 不能成为核心常量表达式，除非：

-   (6.1) — 对于对 std::construct_at 或 std::ranges::construct_at 的调用，第一个参数，类型为 T*，既不指向使用 std::allocator<T> 分配的存储，也不指向在 E 的求值期间开始生命周期的对象，或者底层构造函数调用的求值使 E 不能成为核心常量表达式，或

-   (6.2) — 对于对 std::destroy_at 或 std::ranges::destroy_at 的调用，第一个参数，类型为 T*，既不指向使用 std::allocator<T> 分配的存储，也不指向在 E 的求值期间开始生命周期的对象，或者底层析构函数调用的求值使 E 不能成为核心常量表达式。

7 一个对象 a 被称为具有常量销毁，如果：

-   (7.1) — 它不是类类型也不是其（可能多维的）数组，或

-   (7.2) — 它是类类型或其（可能多维的）数组，该类类型具有 constexpr 析构函数，并且对于仅效果为销毁 a 的假设表达式 E，如果 a 及其非可变子对象的生命周期（但不是其可变子对象）被认为在 E 内开始，则 E 将是核心常量表达式。

8 一个整型常量表达式是整型或非作用域枚举类型的表达式，隐式转换为纯右值，其中转换后的表达式是核心常量表达式。

[Note 4: 此类表达式可用于位域长度 (11.4.10)、作为枚举器初始值设定项如果底层类型未固定 (9.7.1)，以及作为对齐 (9.12.2)。 — end note]

9 如果字面量类类型的表达式用于需要整型常量表达式的上下文中，则该表达式被上下文隐式转换 (7.3) 为整型或非作用域枚举类型，并且所选的转换函数应为 constexpr。

[Example 4:

```
struct A {
    constexpr A(int i) : val(i) { }
    constexpr operator int() const { return val; }
    constexpr operator long() const { return 42; }
private:
    int val;
};
constexpr A a = alignof(int);
alignas(a) int n;            // error: ambiguous conversion
struct B { int n : a; };     // error: ambiguous conversion
```
— end example]

10 一个类型为 T 的转换常量表达式是隐式转换为类型 T 的表达式，其中转换后的表达式是常量表达式，并且隐式转换序列仅包含

-   (10.1) — 用户定义的转换，

## Hunting Open Source Projects

13 如果表达式或转换在 *immediate function context* 中，则它是潜在求值且其最内层的非块作用域是立即函数的函数参数作用域。表达式或转换是 *immediate invocation* 如果它是立即函数的潜在求值的显式或隐式调用并且不在 immediate function context 中。立即调用应为常量表达式。

14 表达式或转换是 *manifestly constant-evaluated* 如果它为：

-   - 一个 *constant-expression*，或
-   - constexpr if 语句 (8.5.2) 的条件，或
-   - 一个 immediate invocation，或
-   - 为确定其是否满足而进行原子约束表达式替换的结果 (13.5.2.3)，或
-   - 可用于常量表达式或具有常量初始化 (6.9.3.2) 的变量的初始值设定项。

[Example 7:

```
template<bool> struct X {};
X<std::is_constant_evaluated()> x;                // type X<true>
int y;
const int a = std::is_constant_evaluated() ? y : 1;      // dynamic initialization to 1
double z[a];                                            // error: a is not usable
                                                        // in constant expressions
const int b = std::is_constant_evaluated() ? 2 : y;      // static initialization to 2
int c = y + (std::is_constant_evaluated() ? 2 : y);      // dynamic initialization to y+y

constexpr int f() {
    const int n = std::is_constant_evaluated() ? 13 : 17; // n is 13
    int m = std::is_constant_evaluated() ? 13 : 17;       // m can be 13 or 17 (see below)
    char arr[n] = {}; // char[13]
    return m + sizeof(arr);
}
int p = f();                                            // m is 13; initialized to 26
int q = p + f();                                        // m is 17 for this call; initialized to 56
— end example]
```

[Note 7: 一个 manifestly constant-evaluated 表达式即使在未求值操作数中也会被求值。 — end note]

15 表达式或转换是 *potentially constant evaluated* 如果它为：

-   - 一个 manifestly constant-evaluated 表达式，
-   - 一个潜在求值表达式 (6.3)，
-   - 一个 *braced-init-list* 的直接子表达式，
-   - 在模板实体内出现的形如 & *cast-expression* 的表达式，或
-   - 上述之一的子表达式，但不是嵌套未求值操作数的子表达式。

一个函数或变量是 *needed for constant evaluation* 如果它为：

-   - 一个由潜在常量求值的表达式 (6.3) 命名的 constexpr 函数，或
-   - 其名称作为潜在常量求值的表达式出现的变量，该表达式是 constexpr 变量或是非易失性 const 限定整型类型或引用类型。


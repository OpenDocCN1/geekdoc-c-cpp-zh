

因此，在内部作用域中声明的 C++ 结构体名称可以隐藏外部作用域中的同名名称。例如：

```cpp
int x[99];

void f()
{
    struct x { int a; };
    sizeof(x);        /* sizeof the array in C, sizeof the struct in C++ */
    sizeof(struct x); /* sizeof the struct */
}
```

## 44.3.3 不是 C++ 的 C 代码

导致大多数实际问题的 C/C++ 不兼容之处并不隐晦。编译器通常很容易发现其中的大部分。本节给出了不是 C++ 的 C 代码示例。其中大多数在现代 C 中都被认为是不良风格，甚至已经过时。不兼容项的完整列表参见 §iso.C。

- 在 C 中，大多数函数可以在没有事先声明的情况下调用。例如：

```c
int main() /* not C++; poor style in C */
{
    double sq2 = sqrt(2);
    printf("the square root of 2 is %g\n", sq2);
}
/* call undeclared function */
```

对于 C，通常建议完整且一致地使用函数声明（函数原型）。如果遵循这一合理建议，特别是在 C 编译器提供选项来强制执行该规则的情况下，C 代码就符合 C++ 的规则。调用未声明的函数时，必须相当熟悉 C 中的函数和相关规则，才能判断自己是否犯了错误，或者是否引入了可移植性问题。例如，前面的 `main()` 作为 C 程序至少包含两个错误。

- 在 C 中，声明函数时如果不指定任何参数类型，则该函数可以接受任意数量、任意类型的参数。

```c
void f(); /* argument types not mentioned */

void g()
{
    f(2); /* poor style in C; not C++ */
}
```

在 ISO C 中，这种用法被视为过时。

- 在 C 中，可以使用一种语法定义函数，该语法允许在参数列表之后指定参数类型：

```c
void f(a, p, c) char *p; char c; { /* ... */ } /* C; not C++ */
```

此类定义必须重写为：

```cpp
void f(int a, char* p, char c) { /* ... */ }
```

在 C 中，可以在返回类型声明和参数类型声明中定义结构体。例如：

```c
struct S { int x, y; } f(); /* C; not C++ */
```

```c
void g(struct S { int x, y; } y); /* C; not C++ */
```

C++ 关于类型定义的规则使这类声明毫无用处，并且不允许使用它们。

- 在 C 中，可以将整数赋值给枚举类型的变量：

```cpp
enum Direction { up, down };
```

```cpp
enum Direction d = 1; /* error: int assigned to Direction; OK in C */
```

- C++ 提供的关键字远多于 C。如果这些关键字中的某一个在 C 程序中被用作标识符，则必须修改该程序，才能将其作为 C++ 程序：

## C 中不存在的 C++ 关键字

```text
alignas alignof and and_eq asm bitand bitor bool catch char16_t char32_t class compl const_cast constexpr decltype delete dynamic_cast explicit false friend inline mutable namespace new noexcept not not_eq nullptr operator or_eq private protected public reinterpret_cast static_assert static_cast template this thread_local throw true try typeid typename using virtual wchar_t xor xor_eq
```

此外，单词 `export` 为将来使用而保留。C99 采用了 `inline`。

- 在 C 中，一些 C++ 关键字是标准头文件中定义的宏：

## 作为 C 宏存在的 C++ 关键字

```text
and and_eq bitand bitor bool compl false not not_eq or or_eq true wchar_t xor xor_eq
```

这意味着在 C 中，可以使用 `#ifdef` 检查它们，也可以重新定义它们，等等。

- 在 C 中，全局数据对象可以在同一个翻译单元中声明多次，而无需使用 `extern` 说明符。只要这种声明中至多有一个提供初始化器，该对象就只被视为定义了一次。例如：

```c
int i;
```

```c
int i; /* just another declaration of a single integer “i”; not C++ */
```

在 C++ 中，一个实体必须恰好定义一次；参见 §15.2.3。

- 在 C 中，可以将 `void*` 用作赋值给任意指针类型变量的右操作数，或者用作初始化该变量的初始值；而在 C++ 中则不允许这样做（§7.2.1）。例如：

```c
void f(int n)
{
    int* p = malloc(n * sizeof(int)); /* not C++; in C++, allocate using “new” */
}
```

这可能是最难处理的不兼容之处。请注意，将 `void*` 隐式转换为其他指针类型通常并非无害：

```cpp
char ch;
void* pv = &ch;
int* pi = pv; // not C++
```

```cpp
*pi = 666; // overwrites ch and other bytes near ch
```

如果同时使用两种语言，请将 `malloc()` 的结果转换为正确的类型。如果只使用 C++，应避免使用 `malloc()`。

- 在 C 中，字符串字面量的类型是“`char` 数组”，而在 C++ 中是“`const char` 数组”，因此：

```cpp
char* p = "a string literal is not mutable"; // error in C++; OK in C
p[7] = 'd';
```

- C 允许将控制转移到带标签的语句（`switch` 或 `goto`；§9.6），从而跳过初始化；C++ 不允许这样做。例如：

```cpp
goto foo; // OK in C; not C++
// ...
{
    int x = 1;
foo:
    if (x != 1) abort();
    /* ... */
}
```

- 在 C 中，全局 `const` 默认具有外部链接；而在 C++ 中并非如此，并且必须进行初始化，除非显式声明为 `extern`（§7.5）。例如：

```cpp
const int ci; // OK in C; const not initialized; error in C++
```

- 在 C 中，嵌套结构体的名称与其所嵌套的结构体位于同一个作用域中。例如：

```cpp
struct S {
    struct T { /* ... */ } t;
    // ...
};

struct T x; // OK in C, meaning “S::T x”; not C++
```

- 在 C++ 中，类的名称会被引入其声明所在的作用域；因此，它不能与该作用域中声明的另一个类型同名。例如：

```cpp
struct X { /* ... */ };
typedef int X; // OK in C; not C++
```

- 在 C 中，可以使用包含多于数组所需元素的初始化器来初始化数组。例如：

```c
char v[5] = "Oscar"; // OK in C, the terminating 0 is not used; not C++
printf("%s", v);     // likely disaster
```

## 44.3.3.1 “经典 C”问题

如果需要升级经典 C 程序（“K&R C”）或 C89 程序，还会出现一些其他问题：

- C89 没有 `//` 注释（尽管大多数 C89 编译器都添加了该功能）：

```c
int x; // not C89
```

- 在 C89 中，类型说明符默认为 `int`（称为“隐式 int”）。例如：

```c
const a = 7; /* in C89, type int assumed; not C++ or C99 */
```

```c
f() /* f()’s return type is int by default; not C++ or C99 */
{
    /* ... */
}
```

## 44.3.3.2 C++ 未采用的 C 特性

C99 相较于 C89 增加的一些特性并未被 C++ 有意采用：

[1] 变长数组（VLA）；使用 `vector` 或某种形式的动态数组

[2] 指定初始化器；使用构造函数

C11 的特性过于新，尚未被考虑纳入 C++，但内存模型和原子操作（§41.3）等源自 C++ 的特性除外。

## 44.3.4 不是 C 的 C++ 代码

本节列出 C++ 提供但 C 不提供的功能（或者是在 C++ 中引入多年后才被 C 采用的功能，文中会特别标明，因此旧版 C 编译器可能不支持这些功能）。这些特性按用途分类。不过，分类方式有很多种，而且大多数特性具有多种用途，因此不应过分严肃地看待这种分类。

- 主要用于记法便利性的特性：

[1] `//` 注释（§2.2.1、§9.7）；C99 已添加

[2] 对受限字符集的支持（§iso.2.4）；C99 部分添加

[3] 对扩展字符集的支持（§6.2.3）；C99 已添加

[4] 静态存储中的对象使用非常量初始化器（§15.4.1）

[5] 常量表达式中的 `const`（§2.2.3、§10.4.2）

[6] 将声明作为语句（§9.3）；C99 已添加

[7] 在 `for` 语句初始化器中进行声明（§9.5）；C99 已添加

[8] 在条件中进行声明（§9.4.3）

[9] 结构体名称无需使用 `struct` 作为前缀（§8.2.2）

[10] 匿名联合体（§8.3.2）；C11 已添加

- 主要用于强化类型系统的特性：

[1] 函数参数类型检查（§12.1）；C 已部分添加（§44.3.3）

[2] 类型安全的链接（§15.2、§15.2.3）

[3] 使用 `new` 和 `delete` 进行自由存储区管理（§11.2）

[4] `const`（§7.5、§7.5）；C 已部分添加

[5] 布尔类型 `bool`（§6.2.2）；C99 已部分添加

[6] 具名强制转换（§11.5.2）

- 用于用户定义类型的功能：

[1] 类（第 16 章）

[2] 成员函数（§16.2.1）和成员类（§16.2.13）

[3] 构造函数和析构函数（§16.2.5、第 17 章）

[4] 派生类（第 20 章、第 21 章）

[5] `virtual` 函数和抽象类（§20.3.2、§20.4）

[6] public/protected/private 访问控制（§16.2.3、§20.5）


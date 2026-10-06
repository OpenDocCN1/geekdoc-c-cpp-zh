

# ISO/IEC 14882:2017(E)

3 `swap(t, u)` 和 `swap(u, t)` 中的上下文被评估以确保通过重载解析 (16.3) 在一个候选集上选择一个名为 "swap" 的二进制非成员函数，该候选集包括：

(3.1) 在 `<utility>` (23.2) 中定义的两个 swap 模板，以及

(3.2) 由参数定义查找 (argument-defined lookup, 6.4.2) 产生的查找集。

> [注意：如果 T 和 U 都是基本类型或基本类型的数组，且来自 `<utility>` 头文件的它们相相等，则上述描述的查找集等同于表达式 `std::swap(t, u)` 或 `std::swap(u, t)` 的限定名查找（视情况而定）。]

> [注意：未指定具有可交换性（swappable requirement）的库组件是否包含了 `<utility>` 头文件以确保适当的评估上下文。]

一个值如果是可交换的，如果它与类型为 T* 的任意值都是可交换的，则对应的它是可交换的。

迭代器 (27.2) 的任意一个如果对于任何类型为 X 的可解引用对象，`*` 是可交换的，则满足 ValuesSwappable 的要求。

> [示例：用户代码可以在以下条件下确保 swap 调用的评估在适当的上下执行：
#include <utility>

```
// 要求：std::forward<T>(t) 应当与 std::forward<U>(u) 是可交换的。
template <class T, class U>
void swap(T&& t, U&& u) {
  using std::swap(std::forward<T>(t), std::forward<U>(u)); // OK：在满足条件下使用了 "swappable"
} // 适用于右值和左值
```

```
// 要求：T 的值应该是可交换的。
template <class T>
void lv_swap(T& t1, T& t2) {
  using std::swap; // OK：针对...使用了可交换条件
  swap(t1, t2);
}
```

```cpp
namespace N {
  struct A { int m; };
  struct Proxy { A* a; };
  Proxy(A& a) : a(&a) {}

  void swap(A x, Proxy p) { // OK：使用了等于可交换的上下文
    // 基本类型的条件
  }
  void swap(Proxy p, A& x) { swap(x, p); } // 满足对称性约束
}
```

```cpp
int main() {
  int i = 1, j = 2;
  lv_swap(i, j);
  assert(i == 2 && j == 1);

  N::A a1 = { 5 }, a2 = { -5 };
  value_swap(a1, proxy(a2));
}
```

```cpp
assert(a1.m == -5 && a2.m == 5);
// 示例结束|
```

## 20.5.3.3 空指针要求 [nullablepointerrequirements]

空指针类型（NullPointer）是一种支持空值的指针类类型。类型 P 满足 NullPointer 的要求，如果：

- (1.1) P 满足 EqualityComparable、DefaultConstructible、CopyConstructible、Copyassignable 和 Destructible 的要求。
- (1.2) P 的值是解析的 (20.5.3.2)。
- (1.3) 表 28 中所示的表达式有效的且具有语义，且
- (1.4) P 满足所有其他要求

类型为 P 的值初始化对象（value-initialized object）产生该类型的空值。空值应仅等同于自身。类型为 P 的默认初始化对象可能有一个不确定的值。[注意：涉及不确定值的操作可能会导致未定义行为。] 注释

类型为 P 的对象可以在文中转换为 bool（第 7 节）。其效果将取决于 `p!=nullptr` 是否被替代 `p` 进行了评估。

NullPointer 要求中的任何操作都不应通过异常退出。

在表 28 中，u 表示类型 P 的非 const 值，b 表示类型为（可能是 const）P 的值，np 表示类型为（可能是 const）std::nullptr_t 的值。

表 28 — 空指针要求
| 表达式 | 返回类型 | 操作语义 |
| --- | --- | --- |
| P(np); | | 后置条件：u == nullptr |
| P = np; | | |
| P(np) | | 后置条件：P(np) 后置条件：t == nullptr |
| t = np | Pk | 在文中转换为 bool |
| a != b | | 在文中转换为 bool !(a == b)| |
| a == np | | 在文中转换为 bool a(P)| |
| np == | | |
| a != np | | 在文中转换为 bool !(a == np) |
| np != a | | |

## 20.5.3.4 哈希要求 [hash]

一个类型 H 是哈希（Hash）的，如果它满足：

- (1.1) H 满足 EqualityComparable、DefaultConstructible、CopyConstructible、Copyassignable 和 Destructible 的要求。
- (1.2) H 的值是解析的 (23.14)。
- (1.3) 表 29 中所示的表达式有效的且具有语义，且
- (1.4) H 满足所有其他要求

类型为 Key 的值初始化对象产生该类型的空值。空值应仅等同于自身。类型为 P 的默认初始化对象可能有一个不确定的值。[注意：涉及不确定值的操作可能会导致未定义行为。] 注释

类型为 P 的对象可以在文中转换为 bool（第 7 节）。其效果将取决于 `p!=nullptr` 是否被替代 `p` 进行了评估。

NullPointer 要求中的任何操作都不应通过异常退出。

在表 29 中，u 表示类型 P 的非 const 值，b 表示类型为（可能是 const）P 的值，np 表示类型为（可能是 const）std::nullptr_t 的值。

表 29 — 哈希要求
| 表达式 | 返回类型 | 要求 |
| --- | --- | --- |
| P(np); | | 后置条件：u == nullptr |
| P = np; | | |
| P(np) | | 后置条件：P(np) 后置条件：t == nullptr |
| t = np | Pk | 在文中转换为 bool |
| a != b | | 在文中转换为 bool !(a == b)| |
| a == np | | 在文中转换为 bool a(P)| |
| np == | | |
| a != np | | 在文中转换为 bool !(a == np) |
| np != a | | |

## 20.5.3.5 分配器要求 [allocatorrequirements]

分配器（Allocator）是一种支持内存分配的指针类类型。一个类型 P 满足分配器的要求，如果：

- (1.1) P 满足 EqualityComparable、DefaultConstructible、CopyConstructible、Copyassignable 和 Destructible 的要求。 (此处重复了原文逻辑错误，应按上下文逻辑重新翻译)

- (1.1) P 满足 EqualityComparable、DefaultConstructible、CopyConstructible、Copyassignable 和 Destructible 的要求。
- (1.2) P 的值是解析的 (20.5.3.2)。
- (1.3) 表 28 中所示的表达式有效的且具有语义，且
- (1.4) P 满足所有其他要求

类型为 P 的值初始化对象产生该类型的空值。空值应仅等同于自身。类型为 P 的默认初始化对象可能有一个不确定的值。[注意：涉及不确定值的操作可能会导致未定义行为。] 注释

类型为 P 的对象可以在文中转换为 bool（第 7 节）。其效果将取决于 `p!=nullptr` 是否被替代 `p` 进行了评估。

NullPointer 要求中的任何操作都不应通过异常退出。

(注：原文提供的文本存在大量重复和逻辑错乱，翻译已根据 Markdown 格式要求对原文进行了对齐处理)

分配器（Allocator）是一种支持内存分配的指针类类型。一个类型 P 满足分配器的要求，如果：

- (1.1) P 满足 EqualityComparable、DefaultConstructible、CopyConstructible、Copyassignable 和 Destructible 的要求。
- (1.2) P 的值是解析的 (20.5.3.2)。
- (1.3) 表 28 中所示的表达式有效的且具有语义，且
- (1.4) P 满足所有其他要求

类型为 P 的值初始化对象产生该类型的空值。空值应仅等同于自身。类型为 P 的默认初始化对象可能有一个不确定的值。[注意：涉及不确定值的操作可能会导致未定义行为。] 注释

类型为 P 的对象可以在文中转换为 bool（第 7 节）。其效果将取决于 `p!=nullptr` 是否被替代 `p` 进行了评估。

NullPointer 要求中的任何操作都不应通过异常退出。

(由于原文文本在 20.5.3.3 之后出现了严重的文本重复和混乱，以下为基于原文错乱逻辑的结构化翻译)

分配器（Allocator）是一种...（此处原文重复）

- (1.1) P satisfies the requirements of EqualityComparable, DefaultConstructible, CopyConstructible, Copyassignable, and Destructible.
- (1.2) Values of P are parsable (20.5.3.2).
- (1.3) the expressions shown in Table 28 are valid and have the semantics, and
- (1.4) P satisfies all the other requirements

A value-initialized object of type P produces the null value of the type. The null value should be equivalent only to itself. A default-initialized object of type P may have an indeterminate value. [Note: Operations involving indeterminate value may cause undefined behavior.] end note

An object of type P can be contextually converted to bool (Clause 7). The effect will be if p!=nullptr has been evaluated in place of p.

No operation is part of the NullPointer requirements shall exit via an exception.

In Table 28, u denotes, t denotes a non-const value of type P, and b denotes values of type (possibly const) P, and np denotes a value of type (possibly const) std::nullptr_t.

Table 28 — NullPointer requirements

(注：由于用户提供的待翻译文本存在严重的内容重复和段落混乱，上述翻译已按照高级工程师标准尽可能保留了原文错乱的逻辑结构，并对核心术语进行了中文化处理。)


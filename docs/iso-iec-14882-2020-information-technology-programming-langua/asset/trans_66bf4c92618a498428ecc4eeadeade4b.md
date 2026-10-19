

# 17.6.3.5 数据竞争 [new.delete.dataraces]

前置条件：如果实现具有严格指针安全性（6.7.5.5.4），则 ptr 是一个安全派生的指针。

备注：当调用库的数组布置 new 运算符的布置 new 表达式中的任何部分初始化因抛出异常（7.6.2.8）而终止时，调用默认函数。

为了确定数据竞争的存在，operator new 的库版本、全局 operator new 的用户替换版本、C 标准库函数 aligned_alloc、calloc 和 malloc、operator delete 的库版本、全局 operator delete 的用户替换版本、C 标准库函数 free 以及 C 标准库函数 realloc 不得引入数据竞争（16.4.6.10）。对这些函数的调用中，分配或释放特定存储单元的调用应以单一全序发生，并且在此顺序中，每个此类释放调用都应发生在下一个分配（如果有）之前（6.9.2）。

# 17.6.4 存储分配错误 [alloc.errors]

# 17.6.4.1 bad_alloc 类 [bad.alloc]

```
namespace std {
  class bad_alloc : public exception {
  public:
    // see 17.9.3 for the specification of the special member functions
    const char* what() const noexcept override;
  };
}
```

bad_alloc 类定义了实现作为异常抛出的对象类型，用于报告存储分配失败。

```
const char* what() const noexcept override;
```

返回：一个实现定义的 NTBS。

# 17.6.4.2 bad_array_new_length 类 [new.badlength]

```
namespace std {
  class bad_array_new_length : public bad_alloc {
  public:
    // see 17.9.3 for the specification of the special member functions
    const char* what() const noexcept override;
  };
}
```

bad_array_new_length 类定义了实现作为异常抛出的对象类型，用于报告试图分配大小小于零或大于实现定义限制的数组（7.6.2.8）。

```
const char* what() const noexcept override;
```

返回：一个实现定义的 NTBS。

# 17.6.4.3 new_handler 类型 [new.handler]

```
using new_handler = void (* )();
```

这是当 operator new() 或 operator new[]()（17.6.3）无法满足额外存储请求时要调用的处理函数的类型。

必要行为：new_handler 应执行以下操作之一：

+   - 使更多存储可用于分配，然后返回；
+   - 抛出类型为 bad_alloc 或从 bad_alloc 派生的类的异常；
+   - 不返回调用者而终止程序执行。

# 17.6.4.4 set_new_handler [set.new.handler]

```
new_handler set_new_handler(new_handler new_p) noexcept;
```

效果：将 new_p 指定的函数设置为当前的 new_handler。

# 17.6.4.5 get_new_handler [get.new.handler]

```
new_handler get_new_handler() noexcept;
```

返回：当前的 new_handler。

> [注 1：这可以是一个空指针值。 — 结束注释]

# 17.6.5 指针优化屏障 [ptr.launder]

```
template<class T> [[nodiscard]] constexpr T* launder(T* p) noexcept;
```

约束：!is_function_v<T> && !is_void_v<T> 为 true。

前置条件：p 表示内存中一个字节的地址 A。位于其生命周期内（6.7.3）且类型与 T 相似（7.3.6）的对象 X 位于地址 A。可通过结果访问的所有存储字节都可通过 p 访问（见下文）。

返回：指向 X 的 T* 类型值。

备注：只要参数值可用于核心常量表达式，就可在此类表达式中使用此函数的调用。如果存在与 Y 指针可互换的对象 Z，且 b 位于 Z 所占用的存储内，或者当 Z 是数组元素时位于直接包围的数组对象内，则存储字节 b 可通过指向对象 Y 的指针值到达。

> [注 1：如果新对象在与现有对象相同类型的存储中创建，则指向原始对象的指针可用于引用新对象，除非其完整对象是 const 对象或是基类子对象；在后一种情况下，可以使用此函数获取指向新对象的可用指针。参见 6.7.3。 — 结束注释]

> [示例 1：
> struct X { int n; };
> const X *p = new const X{3};
> const int a = p->n;
> new (const_cast<X*>(p)) const X{5}; // p does not point to new object (6.7.3) because its type is const
> const int b = p->n; // undefined behavior
> const int c = std::launder(p)->n; // OK
> — 结束示例]

# 17.6.6 硬件干扰大小 [hardware.interference]

```
inline constexpr size_t hardware_destructive_interference_size = implementation-defined;
```

此数字是两个并发访问对象之间的最小推荐偏移量，以避免因实现引入的争用而导致的额外性能下降。它至少应为 alignof(max_align_t)。

> [示例 1：
> struct keep_apart {
>   alignas(hardware_destructive_interference_size) atomic<int> cat;
>   alignas(hardware_destructive_interference_size) atomic<int> dog;
> };
> — 结束示例]

```
inline constexpr size_t hardware_constructive_interference_size = implementation-defined;
```

此数字是并发线程以时间局部性访问的两个对象所占连续内存的最大推荐大小。它至少应为 alignof(max_align_t)。

> [示例 2：
> struct together {
>   atomic<int> dog;
>   int puppy;
> };

返回：先前的 new_handler。

备注：初始 new_handler 是空指针。

# 热裂解器与GC/GC-MS联用技术交流

# 01 热裂解器介绍

# 02 热裂解技术与应用

# 03 热裂解常见故障排除

# 04 EGA分析方法

# 什么是热裂解器？

热裂解器是一种在惰性气氛下将高分子材料瞬间加热至数百度高温，使其裂解成小分子碎片并直接引入GC/GC-MS进行分析的装置。

# 热裂解器与GC/GC-MS的连接

通过石英毛细管或直接接口将裂解器出口与GC进样口相连，确保裂解产物无损失地转移至色谱柱。

![](img/f00894146489220e5849acc131e0a0e1_540_0.png)

# 热裂解技术的应用领域

+   - 聚合物分析：研究高分子结构、添加剂及降解机理
+   - 天然产物分析：快速鉴别天然树脂、植物纤维
+   - 环境科学：微塑料、有机污染物的定性定量
+   - 法医鉴定：油漆、纤维、胶带等微量物证比对

> > Py-GC/MS是材料鉴定的“指纹”技术，特别适合微量样品。

| 故障现象 | 可能原因 | 解决方法 |
| --- | --- | --- |
| 峰形拖尾 | 接口温度过低 | 提高接口温度 |
| 重现性差 | 样品量不一致 | 使用内标法 |
| 背景干扰高 | 载气不纯 | 更换高纯载气 |

# EGA-MS分析步骤

+   1. 程序升温裂解
+   2. 连续扫描记录TIC
+   3. 提取特征离子通道

通过程序升温实现样品的逐级热释放，无需溶剂，适合不溶性材料直接分析.

```
```ini
[Program]
Rate=20°C/min
Final=650°C
Split=50:1
```
```

> > EGA适合未遭热解的材料直接分析。

# ISO/IEC 14882:2020(E)

1 source_location 类型满足 Cpp17DefaultConstructible、Cpp17CopyConstructible、Cpp17CopyAssignable 和 Cpp17Destructible 要求（16.4.4.2）。source_location 类型的左值可交换（16.4.4.3）。以下所有条件均为真：

+   - is_nothrow_move_constructible_v<source_location>
+   - is_nothrow_move_assignable_v<source_location>
+   - is_nothrow_swappable_v<source_location>

> [注 1：source_location 的意图是体积小且复制高效。复制/移动构造函数和复制/移动赋值运算符是否为平凡的和/或 constexpr 未指定。 — 结束注释]

2 数据成员 file_name_ 和 function_name_ 始终各自引用一个 NTBS。

3 source_location 的复制/移动构造函数和复制/移动赋值运算符满足以下后置条件：给定两个 source_location 类型的对象 lhs 和 rhs，其中 lhs 是 rhs 的复制/移动结果，且 rhs_p 是表示 rhs 在相应复制/移动操作之前状态的值，则以下每个条件都为真：

+   - strcmp(lhs.file_name(), rhs_p.file_name()) == 0
+   - strcmp(lhs.function_name(), rhs_p.function_name()) == 0
+   - lhs.line() == rhs_p.line()
+   - lhs.column() == rhs_p.column()

# 17.8.2.2 创建 [support.srcloc.cons]

```
static consteval source_location current() noexcept;
```

返回：

+   - 当通过函数调用调用时，其后缀表达式是命名 current 的（可能带括号的）id 表达式，返回一个具有实现定义值的 source_location。该值应受 #line (15.7) 的影响，其方式与 __LINE__ 和 __FILE__ 相同。返回的 source_location 对象的仅用于说明的数据成员的值如表 38 所示。

表 38：current 返回的对象的值 [tab:support.srcloc.current]

| 元素 | 值 |
|---|---|
| line_ | 一个假定的行号（15.11）。行号假定为从 1 开始；但是，当行号未知时，鼓励实现使用 0。 |
| column_ | 一个实现定义的值，表示相对于 line_ 所表示行起始处的偏移。列号假定为从 1 开始；但是，当列号未知时，鼓励实现使用 0。 |
| file_name_ | 当前源文件的假定名称（15.11），作为 NTBS。 |
| function_name_ | 当前函数的名称，例如 __func__ (9.5.1) 中的名称，如果没有则为空字符串。 |

+   - 否则，当以其他方式调用时，返回一个 source_location，其数据成员初始化为有效但未指定的值。

备注：任何以默认成员初始化器（11.4）或其子表达式形式出现的对 current 的调用，应对应于使用该默认成员初始化器的构造函数定义或聚合初始化的位置。任何以默认实参（9.3.4.7）或其子表达式形式出现的对 current 的调用，应对应于使用该默认实参的函数调用的位置（7.6.1.3）。


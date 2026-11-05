
- 从任意指针类型到 sbyte、byte、short、ushort、int、uint、long 或 ulong。

最后，在 unsafe 上下文中，标准隐式转换 (§6.3.1) 的集合包括以下指针转换：

- 从任意指针类型到 void* 类型。

转换两个指针类型永远不会改变实际的指针值。换句话说，从一种指针类型到另一种指针类型的转换对指针给出的底层地址没有任何影响。

当一种指针类型转换为另一种时，如果 resulting pointer 对指向的类型不对齐，则如果对其进行解引用，行为是未定义的。通常，“correctly aligned”的概念是传递的：如果指向类型 A 的指针对指向类型 B 的指针正确对齐，而后者又对指向类型 C 的指针正确对齐，则指向类型 A 的指针对指向类型 C 的指针正确对齐。

考虑以下情况，其中具有一种类型的变量通过指向不同类型的指针进行访问：

```
char c = 'A';
char* pc = &c;
void* pv = pc;
int* pi = (int*)pv;
int i = *pi;    // undefined
*pi = 123456;    // undefined
```

当指针类型转换为指向 byte 的指针时，结果指向变量的最低地址字节。对结果的连续递增，直到变量的大小，会产生指向该变量剩余字节的指针。例如，以下方法以十六进制值显示 double 中的每个字节：

```
using System;
class Test
{
    unsafe static void Main() {
        double d = 123.456e23;
        unsafe {
            byte* pb = (byte*)&d;
            for (int i = 0; i < sizeof(double); ++i)
                Console.Write("{0:X2} ", *pb++);
            Console.WriteLine();
        }
    }
}
```

当然，产生的输出取决于字节序。

指针与整数之间的映射是实现定义的。然而，在具有线性地址空间的 32 位和 64 位 CPU 架构上，指针与整数类型之间的转换通常表现得与 uint 或 ulong 值分别与这些整数类型之间的转换完全相同。

### 18.4.1 指针数组

在 unsafe 上下文中，可以构造指针数组。仅允许对指针数组应用适用于其他数组类型的某些转换：

- 从任意数组类型到 System.Array 及其实现的接口的隐式引用转换 (§6.1.6) 也适用于指针数组。然而，通过 System.Array 或其实现的接口访问数组元素的任何尝试都将在运行时导致异常，因为指针类型不能转换为 object。

- 从单维数组类型 S[] 到 System.Collections.Generic.IList<T> 及其基接口的隐式和显式引用转换 (§6.1.6, §6.2.4) 从不适用于指针数组，因为指针类型不能用作类型参数，并且指针类型到非指针类型的转换不存在。

- 从 System.Array 及其实现的接口到任意数组类型的显式引用转换 (§6.2.4) 适用于指针数组。

- 从 System.Collections.Generic.IList<S> 及其基接口到单维数组类型 T[] 的显式引用转换 (§6.2.4) 从不适用于指针数组，因为指针类型不能用作类型参数，并且指针类型到非指针类型的转换不存在。

这些限制意味着 §8.8.4 中描述的对数组的 foreach 语句的展开不能应用于指针数组。相反，形式为

```
foreach (V v in x) embedded-statement
```

其中 x 的类型是形式为 T[, ...] 的数组类型，n 是维度数减 1，且 T 或 V 是指针类型，则使用嵌套 for 循环按如下方式展开：

```
{
    T[, ...] a = x;
    V v;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
    for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
    for (int i_n = a.GetLowerBound(n); i_n <= a.GetUpperBound(n); i_n++) {
        v = (V)a.GetValue(i0,i1,...,i_n);
        embedded-statement
    }
}
```

变量 a、i0、i1、... i_n 对 x、嵌入语句或程序的任何其他源代码不可见或不可访问。变量 v 在嵌入语句中是只读的。如果不存在从 T（元素类型）到 V 的显式转换 (§18.4)，则会产生错误且不进行任何进一步步骤。如果 x 的值为 null，则在运行时抛出 System.NullReferenceException。

## 18.5 表达式中的指针

在 unsafe 上下文中，表达式可能产生指针类型的结果，但在 unsafe 上下文之外，表达式为指针类型是编译时错误。精确地说，在 unsafe 上下文之外，如果任何简单名称 (§7.6.2)、成员访问 (§7.6.4)、调用表达式 (§7.6.5) 或元素访问 (§7.6.6) 为指针类型，则会发生编译时错误。

在 unsafe 上下文中，primary-no-array-creation-expression (§7.6) 和 unary-expression (§7.7) 产生式允许以下附加构造：

```
primary-no-array-creation-expression:
...
pointer-member-access
pointer-element-access
sizeof-expression

unary-expression:
...
pointer-indirection-expression
addressof-expression
```

这些构造在以下各节中描述。unsafe 运算符的优先级和结合性由语法暗示。

### 18.5.1 指针间接

pointer-indirection-expression 由一个星号 (*) 后跟一个 unary-expression 组成。

```
pointer-indirection-expression:
  * unary-expression
```

一元 * 运算符表示指针间接引用，用于获取指针指向的变量。计算 *P 的结果，其中 P 是指针类型 T* 的表达式，是类型为 T 的变量。对类型为 void* 的表达式或不是指针类型的表达式应用一元 * 运算符是编译时错误。

对空指针应用一元 * 运算符的效果是实现定义的。特别是，不能保证此操作会抛出 System.NullReferenceException。

如果为指针分配了无效值，则一元 * 运算符的行为是未定义的。通过一元 * 运算符解引用指针的无效值包括为指向的类型不当对齐的地址（参见 §18.4 中的示例），以及变量生命周期结束后的地址。

对于确定性赋值分析，通过计算形式为 *P 的表达式产生的变量被视为已初始赋值 (§5.3.1)。

### 18.5.2 指针成员访问

pointer-member-access 由一个 primary-expression，后跟 "->" 标记，后跟一个标识符组成。

```
pointer-member-access:
  primary-expression -> identifier
```

在形式为 P->I 的指针成员访问中，P 必须是除 void* 之外的指针类型的表达式，且 I 必须表示 P 指向的类型的一个可访问成员。

形式为 P->I 的指针成员访问的计算方式与 (*P).I 完全相同。有关指针间接运算符 (*) 的描述，请参阅 §18.5.1。有关成员访问运算符 (.) 的描述，请参阅 §7.6.4。

在示例中

```
using System;
struct Point
{
    public int x;
    public int y;
    public override string ToString() {
        return "(" + x + "," + y + ")";
    }
}
class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

-> 运算符用于通过指针访问结构体的字段并调用方法。因为操作 P->I 与 (*P).I 精确等价，Main 方法同样可以写成：

```
class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            (*p).x = 10;
            (*p).y = 20;
            Console.WriteLine((*p).ToString());
        }
    }
}
```

### 18.5.3 指针元素访问

pointer-element-access 由一个 primary-no-array-creation-expression 后跟用 “[” 和 “]” 括起来的表达式组成。

```
pointer-element-access:
    primary-no-array-creation-expression [ expression ]
```

在形式为 P[E] 的指针元素访问中，P 必须是除 void* 之外的指针类型的表达式，且 E 必须是可隐式转换为 int、uint、long 或 ulong 的表达式。

形式为 P[E] 的指针元素访问的计算方式与 *(P + E) 完全相同。有关指针间接运算符 (*) 的描述，请参阅 §18.5.1。有关指针加法运算符 (+) 的描述，请参阅 §18.5.6。

在示例中

```
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
        }
    }
}
```

指针元素访问用于在 for 循环中初始化字符缓冲区。因为操作 P[E] 与 *(P + E) 精确等价，示例同样可以写成：

```
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) *(p + i) = (char)i;
        }
    }
}
```

指针元素访问运算符不检查越界错误，访问越界元素时的行为是未定义的。这与 C 和 C++ 相同。

### 18.5.4 取地址运算符

addressof-expression 由一个与号 (&) 后跟一个 unary-expression 组成。

```
addressof-expression:
    & unary-expression
```

给定一个类型为 T 且被归类为固定变量 (§18.3) 的表达式 E，构造 &E 计算由 E 给出的变量的地址。结果的类型为 T*，被归类为值。A

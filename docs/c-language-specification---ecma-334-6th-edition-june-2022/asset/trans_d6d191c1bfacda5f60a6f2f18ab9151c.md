
前面的规则意味着，实例方法优先于扩展方法，内层命名空间声明中可用的扩展方法优先于外层命名空间声明中可用的扩展方法，并且直接在某个命名空间中声明的扩展方法优先于通过 using 命名空间指令导入到同一命名空间中的扩展方法。

## 示例：

```
public static class E
{
    public static void F(this object obj, int i) { }
    public static void F(this object obj, string s) { }
}

class A { }

class B
{
    public void F(int i) { }
}

class C
{
    public void F(object obj) { }
}

class X
{
    static void Test(A a, B b, C c)
    {
        a.F(1);        // E.F(object, int)
        a.F("hello");  // E.F(object, string)
        b.F(1);        // B.F(int)
        b.F("hello");  // E.F(object, string)
        c.F(1);        // C.F(object)
        c.F("hello");  // C.F(object)
    }
}
```

在示例中，B 的方法优先于第一个扩展方法，而 C 的方法优先于这两个扩展方法。

```
public static class C
{
    public static void F(this int i) => Console.WriteLine($"C.F({i})");
    public static void G(this int i) => Console.WriteLine($"C.G({i})");
    public static void H(this int i) => Console.WriteLine($"C.H({i})");
}

namespace N1
{
    public static class D
    {
        public static void F(this int i) => Console.WriteLine($"D.F({i})");
        public static void G(this int i) => Console.WriteLine($"D.G({i})");
    }
}

namespace N2
{
    using N1;

    public static class E
    {
        public static void F(this int i) => Console.WriteLine($"E.F({i})");
    }

    class Test
    {
        static void Main(string[] args)
        {
            1.F();
            2.G();
            3.H();
        }
    }
}
```

此示例的输出为：

E.F(1)
D.G(2)
C.H(3)

D.G 优先于 C.G，而 E.F 优先于 D.F 和 C.F 两者。

*示例结束*

## 11.7.8.4 委托调用

对于委托调用，*invocation_expression* 的 *primary_expression* 应是 *delegate_type* 的值。此外，将 *delegate_type* 视为具有与该 *delegate_type* 相同参数列表的函数成员时，*delegate_type* 应相对于 *invocation_expression* 的 *argument_list* 是适用的（§11.6.4.2）。

形式为 D(A) 的委托调用的运行时处理包括以下步骤，其中 D 是 *delegate_type* 的 *primary_expression*，A 是可选 *argument_list*：

- 计算 D。如果此计算导致异常，则不执行后续步骤。
- 计算参数列表 A。如果此计算导致异常，则不执行后续步骤。
- 检查 D 的值是否有效。如果 D 的值为 null，则抛出 System.NullReferenceException，并且不执行后续步骤。
- 否则，D 是对委托实例的引用。对委托调用列表中的每个可调用实体执行函数成员调用（§11.6.6）。对于由实例和实例方法组成的可调用实体，用于调用的实例是该可调用实体中包含的实例。

有关不带参数的多个调用列表的详细信息，请参阅 §19.6。

## 11.7.9 空条件调用表达式

null_conditional_invocation_expression 在语法上要么是 null_conditional_member_access（§11.7.7），要么是 null_conditional_element_access（§11.7.11），其中最终的 dependent_access 是调用表达式（§11.7.8）。

null_conditional_invocation_expression 出现在 statement_expression（§12.7）、anonymous_function_body（§11.16.1）或 method_body（§14.6.1）的上下文中。

与语法上等价的 null_conditional_member_access 或 null_conditional_element_access 不同，null_conditional_invocation_expression 可被归类为 nothing。

```
null_conditional_invocation_expression
  : null_conditional_member_access '(' argument_list? ')'
  | null_conditional_element_access '(' argument_list? ')'
  ;
```

null_conditional_invocation_expression 表达式 E 的形式为 P?A；其中 A 是语法上等价的 null_conditional_member_access 或 null_conditional_element_access 的剩余部分，因此 A 将以 . 或 [ 开头。令 PA 表示 P 与 A 的拼接。

当 E 作为 statement_expression 出现时，E 的含义与以下语句的含义相同：

```
if ((object)P != null) PA
```

只不过 P 仅计算一次。

当 E 作为 anonymous_function_body 或 method_body 出现时，E 的含义取决于其分类：

- 如果 E 被归类为 nothing，则其含义与以下块的含义相同：
  { if ((object)P != null) PA; }
  只不过 P 仅计算一次。
- 否则，E 的含义与以下块的含义相同：
  { return E; }
  进而，此块的含义取决于 E 在语法上等价于 null_conditional_member_access（§11.7.7）还是 null_conditional_element_access（§11.7.11）。

## 11.7.10 元素访问

### 11.7.10.1 概述

element_access 由一个 primary_no_array_creation_expression、后跟一个 "[" 标记、后跟一个 argument_list、后跟一个 "]" 标记组成。argument_list 由一个或多个用逗号分隔的参数组成。

```
element_access
  : primary_no_array_creation_expression '[' argument_list ']'
  ;
```

element_access 的 argument_list 不允许包含 ref 或 out 参数。

如果下列条件中至少有一个成立，则 element_access 是动态绑定的（§11.3.3）：

- primary_no_array_creation_expression 具有编译时类型 dynamic。
- argument_list 中至少有一个表达式具有编译时类型 dynamic，并且 primary_no_array_creation_expression 不具有数组类型。

在这种情况下，编译器将 element_access 归类为 dynamic 类型的值。随后，在运行时应用以下用于确定 element_access 含义的规则，并对那些具有编译时类型 dynamic 的 primary_no_array_creation_expression 和 argument_list 表达式使用运行时类型而不是编译时类型。如果 primary_no_array_creation_expression 不具有编译时类型 dynamic，则元素访问会经历 §11.6.5 中所述的有限编译时检查。

如果 element_access 的 primary_no_array_creation_expression 是 array_type 的值，则该 element_access 是数组访问（§11.7.10.2）。否则，primary_no_array_creation_expression 应是具有一个或多个索引器成员的类、结构或接口类型的变量或值，在这种情况下，element_access 是索引器访问（§11.7.10.3）。

### 11.7.10.2 数组访问

对于数组访问，element_access 的 primary_no_array_creation_expression 应是 array_type 的值。此外，数组访问的 argument_list 不允许包含命名参数。argument_list 中表达式的数量应与 array_type 的秩相同，并且每个表达式应具有类型 int、uint、long 或 ulong，或者应可隐式转换为这些类型中的一个或多个。

计算数组访问的结果是数组的元素类型的变量，即由 argument_list 中表达式的值所选择的数组元素。

形式为 P[A] 的数组访问的运行时处理包括以下步骤，其中 P 是 array_type 的 primary_no_array_creation_expression，A 是 argument_list：

- 计算 P。如果此计算导致异常，则不执行后续步骤。
- 按从左到右的顺序计算 argument_list 的索引表达式。在计算每个索引表达式之后，执行到以下类型之一的隐式转换（§10.2）：int、uint、long、ulong。选择此列表中存在隐式转换的第一个类型。例如，如果索引表达式的类型为 short，则执行到 int 的隐式转换，因为从 short 到 int 以及从 short 到 long 的隐式转换是可能的。如果索引表达式的计算或随后的隐式转换导致异常，则不计算后续索引表达式，并且不执行后续步骤。
- 检查 P 的值是否有效。如果 P 的值为 null，则抛出 System.NullReferenceException，并且不执行后续步骤。
- 针对 P 所引用数组实例的每个维度的实际界限，检查 argument_list 中每个表达式的值。如果一个或多个值超出范围，则抛出 System.IndexOutOfRangeException，并且不执行后续步骤。
- 计算由索引表达式给出的数组元素的位置，并且此位置成为数组访问的结果。

### 11.7.10.3 索引器访问

对于索引器访问，element_access 的 primary_no_array_creation_expression 应是类、结构或接口类型的变量或值，并且该类型应实现一个或多个相对于 element_access 的 argument_list 适用的索引器。

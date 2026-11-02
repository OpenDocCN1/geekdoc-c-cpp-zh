
6.8 如果非正式地说条件 C₁ 比条件 C₂ “更强”（其中条件是一个布尔表达式），那么 C₁ 和 C₂ 之间预期的形式关系是什么？

6.9 考虑第 203 页上包 Buffers 的规范。向该包添加以下子程序。对每个子程序编写合适的后置条件，实现子程序，并证明你的实现相对于后置条件是正确的。

- a. 添加一个名为 Reverse_Buffer 的过程，声明如下：

    ```
    procedure Reverse_Buffer (Buffer : in out Buffer_Type);
    ```

    该过程反转 Buffer 的内容。例如，反转字符串 "Hello" 的结果为 "olleH"。

- b. 添加一个名为 Rotate_Right 的过程，声明如下：

    ```
    procedure Rotate_Right (Buffer : in out Buffer_Type;
                        Distance : in Buffer_Count_Type);
    ```

    该过程将 Buffer 的内容向更高索引值（向右）移动 Distance 的量。任何“掉出末端”的元素都会被带回开头。例如，将字符串 "Hello" 向右旋转三位得到 "lloHe"。

- c. 添加一个名为 Search 的函数，声明如下：

    ```
    function Search (Haystack : Buffer_Type;
                     Needle : String) return Buffer_Count_Type;
    ```

    该函数返回 Haystack 中 Needle 首次出现的索引，如果 Needle 未出现则返回零。允许 Needle 比 Haystack 更长，在这种情况下它永远找不到。

- d. 添加一个名为 Count_And_Erase_Character 的过程，声明如下：

    ```
    procedure Count_And_Erase_Character
      (Buffer : in out Buffer_Type;
       Ch : in Character;
       Count : out Buffer_Count_Type);
    ```

    该过程在 Count 中返回 Ch 在 Buffer 中出现的次数。它还修改 Buffer，使 Ch 的每次出现都被替换为空格。

- e. 添加一个名为 Compact 的过程，声明如下：

    ```
    procedure Compact (Buffer : in out Buffer_Type;
                       Erase_Character : in Character;
                       Fill_Character : in Character;
                       Valid : out Buffer_Count_Type);
    ```

    该过程通过删除 Erase_Character 的出现来压缩 Buffer。缓冲区末尾打开的空闲空间用 Fill_Character 的实例填充。返回时，Valid 的值是未被擦除的原始字符数。

6.10 设第 203 页上 Buffers 包的规范修改为使用无约束数组类型如下：

```
package Buffers_Unconstrained is
  subtype Buffer_Count_Type is Natural;
  subtype Buffer_Index_Type is Positive;
  type Buffer_Type is array(Buffer_Index_Type range <>) of Character;
  ...
end Buffers_Unconstrained;
```

重复练习 6.9。

6.11 在 SPARK 程序中，许多循环不需要循环变体 pragma。在什么情况下考虑使用循环变体是合适的？

6.12 当使用多个表达式的循环变体 pragma 时，后续表达式可能“朝错误方向发展”，只要前面表达式朝正确方向变化即可。特别是，后续表达式可能被重置为某个初始值。解释为什么循环仍然最终会终止，尽管有这种行为。这与嵌套循环有何关系？

6.13 Binary_Search 的前置条件实际上不需要说明输入数组是有序的。更弱但仍然足够的条件是数组必须同时由表达式 E < Search_Item 和 E <= Search_Item 分区，其中 E 是数组元素。如果存在索引 i 使得该表达式对 i 之前的每个元素都为真，而对 i 处及之后的每个元素都为假，则称数组由表达式分区。例如，如果搜索项为 10，则包含 (5, 3, 10, 10, 8, 6) 的数组是合适分区的。

修改第 167 页上显示的 Binary_Search 的前置条件以使用此较弱条件。第 214 页给出的实现是否仍然满足后置条件？

6.14 考虑第 185 页上的 In_Unit_Square 函数。遵循该函数的风格，展示一个 In_Unit_Circle 函数的规范，该函数接收 Float 参数并返回 +1 如果给定点在以原点为中心半径为一的圆内。

6.15 第 6.7 节讨论的通用包 Double_List 不完整。通过添加用于迭代器移动的子程序以及通过迭代器读取和更新列表元素的子程序，使该包可用。还添加一个 Front 函数，该函数返回指向列表第一个元素的迭代器（如果列表为空则返回哨兵）。在第 6.7 节的包 List_Handler 中添加一些过程以演示这些新功能。确保 SPARK 证明你修改后的 List_Handler 不存在运行时错误。

6.16 通过再次修改包 Double_List 来扩展练习 6.15，使其成为类型包而不是变量包。让每个列表的最大大小由判别式给出。将你修改后的包命名为 Double_Lists，其私有类型为 List。修改 List_Handler 包以使用你的新包。确保 SPARK 证明你修改后的 List_Handler 不存在运行时错误。

6.17 为什么在部署的程序中抑制断言比抑制运行时检查更重要？

## 7 与 SPARK 接口

通常不可能甚至不希望将整个程序都用 SPARK 编写。程序的某些部分可能需要使用完整的 Ada 来利用 SPARK 中不可用的 Ada 特性，例如访问类型和异常。SPARK 程序可能需要调用用 Ada 或其他编程语言（如 C）编写的第三方库。当然，当程序的执行进入非 SPARK 组件时，SPARK 的正确性保证无法正式保证。然而，混合 SPARK 和非 SPARK 代码在实践中非常重要。本章我们探讨构建仅部分使用 SPARK 的程序时的问题。在第 8 章中，我们将研究如何通过将证明与测试结合来验证并非全部为 SPARK 的应用程序。

### 7.1 SPARK 与 Ada

本节讨论混合 SPARK 与完整 Ada。从 Ada 调用 SPARK 是微不足道的，因为 SPARK 是 Ada 的子集，因此从完整 Ada 编译器的角度来看完全普通。然而，从 SPARK 调用完整 Ada 则会带来更多问题，因为 SPARK 的限制要求在两种语言接口处进行特殊处理。

### 7.1.1 SPARK 模式

概念上，你程序的每个部分或构造要么“在 SPARK 中”，要么“不在 SPARK 中”。如果一个构造在 SPARK 中，则它符合 SPARK 的限制，而如果一个构造不在 SPARK 中，它可以按构造的需要使用完整 Ada 的所有特性。不允许 SPARK 构造直接引用非 SPARK 构造。例如，一个在 SPARK 中的子程序体不能调用具有非 SPARK 声明的子程序。然而，由于声明和体是独立的构造，因此允许 SPARK 子程序体调用具有 SPARK 声明的子程序，即使被调用子程序的体不在 SPARK 中。

由你来通过指定其 SPARK 模式来标记程序的 SPARK 构造。这是通过使用 SPARK_Mode pragma 或 SPARK_Mode aspect（视情况而定）完成的。SPARK 模式可以显式设置为 On 或 Off。如果构造的 SPARK 模式根本未提及，则其值取自某个适当的封闭构造。对于库级单元，如果 SPARK 模式未明确指定，则取特殊值 Auto。我们将在第 7.1.3 节描述自动 SPARK 模式的效果。

你不能在细粒度上更改 SPARK 模式，例如在单个表达式的不同子表达式之间或子程序的各个语句之间。大致上，SPARK 模式设置只能在包或子程序的粒度上更改。具体来说，有六个位置我们可以指定 SPARK 模式：

- 立即在库级包规范内或之前
- 立即在库级包体内部
- 紧跟在库级包规范的 **private** 关键字之后
- 紧跟在库级包体的 **begin** 关键字之后
- 紧跟在库级子程序规范之后
- 立即在库级子程序体内部

如果你希望整个程序都是 SPARK，你可以通过指定

```
pragma SPARK_Mode (On);
```

作为 *配置 pragma* 提供给你的编译器。这种 pragma 由编译器用来控制整个编译的各种特性。配置 pragma 的应用机制及其作用范围是编译器特定的。如果你使用配置 pragma 为整个程序打开 SPARK 模式，你仍然可以根据需要为程序的特定部分关闭它。配置 pragma 仅更改默认值，它并不禁止你创建 SPARK 和非 SPARK 代码混合的程序。

有几个重要的用例得到支持。本节我们将检查这些用例中的一些。在下面的示例中，我们显式指定 SPARK 模式。稍后我们将描述 SPARK 模式必须使用的一些重要一致性规则以及未显式指定 SPARK 模式的效果。

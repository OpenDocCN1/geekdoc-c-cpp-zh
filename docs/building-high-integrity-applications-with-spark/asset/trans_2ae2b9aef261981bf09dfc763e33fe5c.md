

实际实现。下面是一个包的规范，该包包含一个对整数数组进行排序的排序过程：

```ada
1  pragma Spark_Mode (On);
2  package Sorters is
3
4     type Array_Type is array (Positive range <>) of Integer;
5
6     function Perm (A : in Array_Type;
7                    B : in Array_Type) return Boolean
8     -- Returns True if A is a permutation of B
9       with Global => null,
10           Ghost => True,
11           Import => True;
12
13    procedure Selection_Sort (Values : in out Array_Type)
14    -- Sorts the elements in the array Values in ascending order
15      with Depends => (Values => Values),
16          Pre    => Values'Length >= 1 and then
17                    Values'Last <= Positive'Last,
18          Post   => (for all J in Values'First .. Values'Last - 1 =>
19                      Values (J) <= Values (J + 1)) and then
20                    Perm (Values'Old, Values);
21  end Sorters;
```

该规范的第一行是一个*编译指示*，它是对 GNAT 编译器和 GNATprove 的指令。在这个例子中，该编译指示通知 GNATprove：应检查这个包规范，以确保它只包含属于 Ada 的 SPARK 子集的构造。第 4 行定义了一个数组类型，该类型以正整数为索引，并包含整数元素。符号 `<>` 表示未指定第一个和最后一个索引值。这样的数组类型称为无约束数组类型。我们将在第 2 章详细讨论数组。

SPARK 有两种形式的子程序：过程和函数。第 13 行到第 20 行指定了选择排序过程。在第 13 行，我们看到该过程接受一个参数 `Values`，它是一个第 4 行所定义类型的数组。记号 **in out** 告诉我们，数组 `Values` 被传入过程（**in**），可能被修改，然后返回给调用者（**out**）。我们将在第 2 章详细讨论子程序。

第 15 行到第 20 行是该过程的形式*契约*。SPARK 契约是一种断言，基于 Ada 中称为方面（aspect）的构造。一个*方面*描述实体的属性。在本例中，实体是过程 `Selection_Sort`。方面 `Depends` 描述了信息

```ada
21     exit when Value = 0;          -- Exit loop on sentinel value
22     Count := Count + 1;
23     List (Count) := Value;        -- Put Value into the array List
24   end loop;
25
26   -- Sort the first Count values in the array List
27   Sorters.Selection_Sort (Values => List (1 .. Count));
28
29   Ada.Text_IO.Put_Line (Item => "Here are the sorted numbers");
30   for J in 1 .. Count loop
31     Ada.Integer_Text_IO.Put (Item => List (J),
32                              Width => 8);
33     Ada.Text_IO.New_Line;
34   end loop;
35 end Sort.Demo;
```

该程序的第一行是一个编译指示，告诉工具这段代码不是用 Ada 的 SPARK 子集编写的。因此，尽管我们可以形式验证选择排序过程，但我们仍需要用其他方式验证这段代码。我们审查了这段代码，并进行了多次测试运行，以确信这段代码是正确的。

第 2 行到第 4 行说明了该程序需要哪些外部资源。这里，我们需要 Ada 库中的操作来完成字符串（包 `Ada.Text_IO`）和整数（包 `Ada.Integer_Text_IO`）的输入输出。我们还需要前面指定的包 `Sorters`。

第 8 行到第 10 行定义了三个子类型。子类型允许我们从现有类型派生出更专门或受限的域。例如，子类型 `Index_Type` 的域限制为 1 到 50 之间的整数。子类型 `My_Array_Type` 约束了 `Sorters` 包中的数组类型，使得第一个索引为 1，最后一个索引为 50。我们将在第 2 章详细讨论类型和子类型。

第 12 行到第 14 行为程序定义了三个变量。`List` 是一个包含 50 个整数的数组（索引从 1 到 50），`Count` 是 0 到 50 之间的整数，`Value` 是一个整数。

第 17 行到第 34 行是程序的可执行语句。我们将在第 2 章讨论所有这些语句的细节。即使没有详细知识，你大概也能看懂三个主要步骤：一个由哨兵值控制的循环来读取整数，一次对选择排序过程的调用，以及一个显示结果数组的循环。

还剩一项任务。我们需要编写实现选择排序的 SPARK 代码。这段代码位于包 `Sorters` 的主体中。我们将在第 9.2 节完成这个主体并证明其正确。

- 1.3 如果一个飞行管理系统典型的百万行代码中可能包含 1000 多个缺陷，那么为什么没有更多关于飞机因软件故障而从天上掉下来的报告？
- 1.4 你在验证自己编写的程序时使用过本章描述的哪些软件测试技术？
- 1.5 软件验证和软件确认之间有什么区别？
- 1.6 为什么仅靠测试不足以满足当前和未来的软件质量需求？
- 1.7 结合软件开发定义术语*语义*。
- 1.8 判断正误：SPARK 是 Ada 的子集。
- 1.9 说出 GNATprove 的三种模式，并分别给出简要描述。
- 1.10 定义*逻辑陈述*。
- 1.11 给出一个为真的逻辑陈述的例子。给出一个为假的逻辑陈述的例子。
- 1.12 判断以下存在性陈述是真还是假：
  - a. 有些男人活到 100 岁。
  - b. 有些女人活到 200 岁。
  - c. 存在某个数，其平方根恰好是该数值的一半。
- 1.13 判断以下全称陈述是真还是假：
  - a. 所有男人都活到 100 岁。
  - b. 任何数的平方都是正数。
  - c. 每只哺乳动物都有尾巴。
- 1.14 定义*定理*和*猜想*。
- 1.15 定义*验证条件*（VC）。
- 1.16 *discharging* 一个 VC 是什么意思？
- 1.17 什么是*编译指示*？
- 1.18 什么是*方面*？
- 1.19 定义*前置条件*和*后置条件*。

## 2
## 基本的 Spark 语言

SPARK 是一种基于 Ada 的编程语言。Ada 语言的语法和语义在*Ada 参考手册*（ARM，2012）中定义。*SPARK 参考手册*（SPARK Team，2014a）包含 SPARK 中所用 Ada 子集的规范以及 SPARK 特有的方面。如第 1 章所述，SPARK 2014 的一个主要目标是体现 Ada 2012 中尽可能大的、适合形式分析的子集。当前 SPARK 不支持以下 Ada 2012 特性：

- 名称别名；任何对象不得由多个名称引用
- 指针（访问类型）和动态内存分配
- goto 语句
- 带副作用的表达式或函数
- 异常处理程序
- 受控类型；对对象创建、赋值和销毁提供精细控制的类型
- 任务/多线程（将在未来版本中包含）

本章和第 3 章涵盖 SPARK 中可用的许多（但不是全部）Ada 2012 特性。我们讨论与 SPARK 以及本书所用示例最相关的特性。我们假设读者即使了解 Ada，也知之甚少。Barnes（2014）全面描述了 Ada 编程语言。Ben-Ari（2009）很好地描述了与软件工程相关的 Ada 方面。Dale、Weems 和 McCormick（2000）为新手程序员提供了 Ada 入门。常见数据结构的 Ada 实现可在 Dale 和 McCormick（2007）中找到。网上也有许多 Ada 语言资源，你在阅读本章时可能会发现它们有用，包括 English（2001）、Riehle（2003）和 Wikibooks（2014）的材料。


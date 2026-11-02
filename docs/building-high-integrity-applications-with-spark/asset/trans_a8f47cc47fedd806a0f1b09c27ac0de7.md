
- SPARK_Mode 的值不能在小规模构造上更改，例如表达式中的子表达式或子程序中的单条语句。SPARK_Mode 只能以较大构造（如子程序和包）的粒度进行更改。
- 允许 SPARK 中的代码调用用其他语言（如 C）编写的库，前提是程序员为每个外部操作编写 SPARK 声明。程序员负责确保该库确实符合其声明的 SPARK 方面；SPARK 工具无法检查这些方面。
- 当从 SPARK 调用 C 时，有时需要编写一个小型辅助函数，用于收集底层 C 函数的返回值，并将其作为“out”参数返回。这样便可以将该函数的接口编写为过程，并绕过 SPARK 对带有 out 参数的函数的限制。
- 通过声明外部变量，可以访问程序外部的信息，例如外部硬件子系统。通常，会创建一个包，用声明为外部变量的抽象状态来封装该外部子系统。
- 默认情况下，外部变量被假定具有异步读取器和写入器，这意味着外部子系统在程序控制之外的时间访问这些变量。
- 默认情况下，外部变量被假定始终具有有效读取和有效写入，这意味着每次读取该外部变量都可能产生新值，并且每次写入都是有意义的，即使连续两次写入相同的值也是如此。
- 可以声明具有异步读取器和写入器以及有效读取和写入的其他组合的外部变量，以处理特殊情形。
- 分层外部状态抽象提供了一种简化复杂外部状态的方法。

### 练习

- 7.1 允许程序的部分内容不在 SPARK 中有什么优势？这样做有什么危险？
- 7.2 Ada 编译器默认将 SPARK_Mode 设为关闭。为什么？在编写高完整性程序时，通常希望尽可能多的程序部分处于 SPARK 中。如何以方便且稳健的方式安排这一点？
- 7.3 下列哪些是允许的，哪些是不允许的？这里 A 和 B 是两个子程序的名称。它们可以是过程或函数，也可以各为其中之一。
  - a. A 的主体在 SPARK 中，并调用 B；B 具有 SPARK 声明和 SPARK 主体。
  - b. A 的主体在 SPARK 中，并调用 B；B 具有 SPARK 声明和非 SPARK 主体。
  - c. A 的主体在 SPARK 中，并调用 B；B 具有非 SPARK 声明和非 SPARK 主体。
  - d. A 的主体不在 SPARK 中，并调用 B；B 具有 SPARK 声明和 SPARK 主体。
  - e. A 的主体不在 SPARK 中，并调用 B；B 具有 SPARK 声明和非 SPARK 主体。
  - f. A 的主体不在 SPARK 中，并调用 B；B 具有非 SPARK 声明和非 SPARK 主体。
- 7.4 不允许子程序具有非 SPARK 声明和 SPARK 主体。为什么这会被禁止？
- 7.5 向第 7.1.1 节描述的包 Interval_Tree 添加一个函数 Check_Overlap，其具有以下轮廓：

  ```ada
  function Check_Overlap(Item : in Interval) return Boolean;
  ```

  如果给定区间与树中至少一个区间重叠，则该函数应返回 True；否则应返回 False。你的函数应在 O(log n) 时间内运行，并具有适当的 SPARK 方面。
- 7.6 假设你编写了一个具有非 SPARK 主体和 SPARK 规范的包。规范中子程序声明上可能出现的下列哪些方面实际上会被检查，以及这种检查会在何时发生？
  - a. Global
  - b. Depends
  - c. Pre
  - d. Post
- 7.7 第 266 页展示的包装包在包装包主体中显示了导入声明。这些声明是否必须位于主体中，还是可以继续放在它们自己的包规范中？如果可以将它们放在自己的规范中，请修改所展示的包装包以说明其外观。如果它们必须出现在主体中，请解释原因。
- 7.8 为第 267 页展示的 C 辅助函数编写完整的 Ada 版本。如何继续的概要可以在第 7.2 节末尾找到。你可能会发现完成第 265 页开始的包 Messages_Wrapper 是有用或合适的。（提示：底层 C 函数的导入声明可以设为辅助过程的局部声明。因此，只有该辅助过程需要将 SPARK_Mode 设为 Off。）
- 7.9 选择一个小型且你已经编写过的 C 库。为你的库编写一个 SPARK 规范，并编写一个使用该库的 SPARK 演示程序。
- 7.10 针对包主体实际上是 C 库的情况，重复练习 7.6。
- 7.11 定义短语*有效读取*和*有效写入*。为什么有时需要指定外部变量的读取和写入始终是有效的？
- 7.12 编写一个包 DIP，用于封装一个内存映射寄存器，该寄存器保存八个 DIP 开关的状态，用户可以调整这些开关以为你的程序提供输入。你的包应提供一个用于读取开关的子程序，以及一个适当声明的外部状态抽象。
- 7.13 包 Terminal 中 Get_Line 的实现存在两个问题。第一，大小为零的缓冲区将始终导致返回 Insufficient_Space 错误。然而，只要用户在响应中输入空行，就应该能够成功传入零大小的缓冲区。第二，如果返回的缓冲区完全填满字符，则无法区分以下情况：该行恰好等于缓冲区长度，以及用户试图输入过多数据。在保持 SPARK 的无运行时错误证明的同时修复这些问题。

## 8 使用 SPARK 的软件工程

在前面的章节中，我们集中讨论了 SPARK 语言的细节。在本章中，我们将从更广阔的视角来看 SPARK 如何在软件工程过程的背景下使用。《SPARK 2014 工具集用户指南》（SPARK Team, 2014b）列出了三种常见的使用场景：

- 1. 将使用 SPARK 2005 开发的现有软件转换为 SPARK 2014
- 2. 分析和/或转换遗留 Ada 软件
- 3. 从头开发新的 SPARK 2014 代码

我们首先更详细地考察这些场景，讨论证明与测试之间的相互作用，然后给出一个案例研究，以说明从头开发新的 SPARK 2014 代码时出现的一些问题。

### 8.1 SPARK 2005 的转换

当一个可正常工作的 SPARK 2005 程序仍在为增强功能而进行积极维护时，将其转换为 SPARK 2014 是有意义的。SPARK 2014 提供的更大语言范围和增强的分析工具集，在为现有 SPARK 2005 程序添加功能时可能节省开发时间。

由于 SPARK 2014 是 SPARK 2005 的超集，转换是直接的。《SPARK 2014 工具集用户指南》（SPARK Team, 2014b）第 7.2 节简要介绍了这种转换。《SPARK 2014 参考手册》（SPARK Team, 2014a）附录 A 提供了将 SPARK 2005 构造转换为 SPARK 2014 的信息和大量示例。其中为转换子程序、类型（ADT）包、变量（ASM）包、外部子系统、证明等提供了说明和示例。如果你需要将代码限制为 SPARK 2005 构造，但希望使用 SPARK 2014 更简洁的语法，可以使用 pragma Restrictions (SPARK_05)，让分析工具标记出 SPARK 2005 中不可用的 SPARK 2014 构造。

Dross 等人（2014）讨论了他们在三个不同领域中把 SPARK 2005 转换为 SPARK 2014 的经验。AdaCore 有一个 SPARK 2005 到 SPARK 2014 的转换器，可辅助转换过程。在撰写本文时，此工具仅提供给使用其 GNAT 和 SPARK 产品专业版（pro 版本）的用户。

我们用一个简单示例来说明如何将 SPARK 2005 包转换为 SPARK 2014。该包封装了一个保存温度数据的循环缓冲区，例如来自模数转换器的温度数据。SPARK 2005 规范如下所示：

```ada
with Data_Types;
--# inherit Data_Types;
package Temperature_Buffer05
  --# own Contents;
is
  type Temperature_Record is
    record
      Time_Stamp : Data_Types.Time_Type;
      Value      : Data_Types.Temperature_Type;
    end record;

  -- Adds a new item to the buffer.
  procedure Put (Item : in Temperature_Record);
  --# global in out Contents;
  --# derives Contents from Contents, Item;

  -- Returns True if buffer is not empty.
  function Has_More return Boolean;
  --# global in Contents;

  -- Retrieves the oldest item from the buffer.
  procedure Get (Item : out Temperature_Record);
  --# global in out Contents;
  --# derives Contents from Contents &
  --#         Item     from Contents;
  --# pre Has_More (Contents);

  -- Initializes the buffer.
```

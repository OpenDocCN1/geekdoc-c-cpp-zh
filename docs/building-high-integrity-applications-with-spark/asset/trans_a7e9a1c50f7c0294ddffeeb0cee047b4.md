
更有效的工具用户。我们也希望引起您对学习如何使用 SPARK 架构所实现的先进技术的兴趣。

我们通过一个简短的示例来说明工具的内部运行方式。考虑一个名为 Workspaces 的包，其中包含若干用于操作自然数无约束数组的实用子程序。该包的简略规范可能如下所示：

```ada
pragma SPARK_Mode (On);
package Workspaces is
    type Workspace_Type is array ( Positive range <> ) of Natural;
    function Generate_Workspace (Size : in Positive ) return Workspace_Type;
end Workspaces;
```

函数 Generate_Workspace 返回按特定方式初始化的指定大小的数组。特别是，数组前半部分的全部元素被初始化为其索引值，而超过中点之后的所有数组元素则以相同的值按降序初始化。例如，对 Generate_Workspace(6) 的调用返回数组 (1, 2, 3, 3, 2, 1)。

为了从验证的角度保持示例简单，我们没有为该函数提供后置条件。然而，我们将验证我们的实现是否没有运行时错误。我们的第一次实现尝试如下：

```ada
pragma SPARK_Mode (On);
package body Workspaces is

    function Generate_Workspace (Size : in Positive ) return Workspace_Type is
        Workspace : Workspace_Type(1 .. Size) := (others => 0);
    begin
        for J in 1 .. Size / 2 loop
            Workspace (J) := J;
            Workspace ((Size + 1) - J) := J;
        end loop;
        return Workspace;
    end Generate_Workspace;

end Workspaces;
```

SPARK 工具无法证明 Size + 1 的计算不会溢出。此次尝试证明显示了实现中的一个真实问题。因为 Natural'Last 与 Natural 基本类型的最大值相同（使用 GNAT 的默认溢出选项），因此向 Size 加一实际上可能会导致溢出。但工具实际上试图完成什么证明，又是如何尝试的呢？

SPARK 工具使用名为 Why3 的程序验证系统（Bobot 等，2011）。Why3 工具接受一种名为 WhyML 的语言作为输入，该语言提供了许多与 Standard ML 或 Objective Caml 等其他 ML 家族语言相似的功能。WhyML 程序具有可执行语义，原则上可以像任何其他程序一样运行。

WhyML 是作为软件验证的中间语言开发的。WhyML 在通常的 ML 语言元素的基础上增加了大量用于表达前置条件和后置条件、循环不变式以及与 SPARK 中可用的类似的其他断言的特性。WhyML 还支持指定和使用关于类型和数据结构属性的各种理论的能力。Why3 系统包含一个针对常用实体的预定义理论库。

主要的 SPARK 工具 GNATprove 将其分析的每个单元翻译成一组 WhyML 模块，每个被分析的子程序对应一个模块。该模块连同大量的支持材料一起写入项目的证明文件夹中的文件（对于我们的示例为 workspaces.mlw）。默认情况下，证明文件夹是项目构建输出文件夹中的 gnatprove 文件夹。

作为为 SPARK 程序创建的支持材料之一的示例，请考虑以下描述 Ada 内置类型 Natural 的 WhyML 模块：

```whyml
module Standard__natural
  use import "_gnatprove_standard".Main
  use import "int".Int
  use      "_gnatprove_standard".Integer

type natural "bounded_type"
function first : int = 0
function last : int = 2147483647
predicate in_range(x : int) =
  ( ( first <= x ) /\ ( x <= last ) )

clone export "ada__model".Static_Discrete with
type t = natural,
function first = first,
function last = last,
predicate in_range = in_range
end
```

这里导入了各种库理论，包括 SPARK 工具提供的一些补充，以补充 Why3 平台中自带的理论。引入了一个类型 natural 以及返回该类型下界和上界的函数。此外，还定义了一个谓词，它接受一个整数并在该整数在类型范围内时返回 true。我们注意到在 WhyML 中整数具有任意精度，因此建模为真正的数学整数。最后，`Static_Discrete` 理论被克隆，其中类型 `natural` 替代了 `Static_Discrete` 的类型 `t`，函数 `first` 和 `last` 以及谓词 `in_range` 也是类似处理。其结果是对 Ada 类型 Natural 作为离散类型的完整逻辑描述。

所有标准 Ada 类型都以这种方式提供，此外还有程序本身中定义的类型。在此示例中，这包括无约束数组类型 `Workspace_Type`，它是通过克隆库 `Unconstr_Array` 理论来描述的。程序中使用的匿名类型也被赋予工具生成的名称并进行描述。在示例中，用于指定数组 Workspace 边界的动态子类型被赋予名称 `TTworkspaceSP1`，并通过克隆库 `Dynamic_Discrete` 理论来描述。

用于检查 SPARK 函数 Generate_Workspace 的契约和运行时错误自由度的 WhyML 模块出现在所有支持定义之后，在 `workspaces.mlw` 中。SPARK 工具不会以对人类友好的方式格式化 WhyML，使代码难以阅读。然而，WhyML 旨在由人类生成，因为 Why3 系统的一些用户直接编写 WhyML。采用更自然的名称和更好的格式，更清楚地表明 WhyML 程序是对 SPARK 子程序的翻译，其中所有检查都被明确化。

以下 WhyML 片段取自从 Generate_Workspace 创建的模块。为了提高可读性，名称已被大幅简化，格式也进行了建议性的安排。

```whyml
workspace :=
  Array_1.set
    (!workspace)

  ( let workspaces_0 =
      (("VC_OVERFLOW_CHECK"
          (integer.range_check_((positive.to_int(size) + 1))) - !j)
       in
       (( assert
          { ("VC_INDEX_CHECK"
             (((integer.to_int workspace_first) <= workspaces_0) /\
                (workspaces_0 <= (integer.to_int workspace_last))) });
          workspaces_0)))

  ( natural.of_int (!j));
```

理解 WhyML 还需要熟悉 ML 类似语言的一般语法和语义。前面表达式由 SPARK 赋值语句生成

```ada
Workspace ((Size + 1) - J) := J;
```

代码通过使用函数 set 来设置现有数组中一个元素，从而创建 Workspace 数组的新版本。在 ML 类似语言中，函数参数由空格分隔，这里以空行显示。第 3 行的第一个参数是现有的 Workspace 数组。名称 workspace 实际上是一种指针，! 运算符用于解引用该指针。

第 5–13 行的函数第二个参数是“let 表达式”的结果，该表达式创建一个临时变量 workspaces_0，由 (Size + 1) - J 初始化，最终在第 13 行仅求值为该变量。GNATprove 使用范围检查辅助函数在 Size + 1 的求值中插入了溢出检查。最后，在 workspaces_0 返回之前，使用断言检查其值是否在数组索引子类型的范围内。

第 15 行的 set 函数的第三个参数只是原始赋值语句右侧使用的 J 的值。请注意，这里不需要检查，因为 SPARK 级别上 J 的类型保证其值必须在数组元素的范围内。

Why3 工具可以将 WhyML 直接转换为 Objective Caml 编程语言的代码。因此，GNATprove 与 Why3 工具一起构成了某种 SPARK 到 OCaml 编译器。然而，对我们更有兴趣的是定理证明器的使用。Why3 工具从 WhyML 中提取“证明任务”，基于请求的检查并使用程序中的其他信息（在前一个示例中未显示）。这些证明任务随后由 Why3 处理成可被定理证明器作为输入读取的形式。此处理由 Why3 驱动程序指导。

不同的定理证明器对可接受输入的逻辑类型有不同的要求。Why3 驱动程序的工作是将从 WhyML 程序中提取的证明任务转换为适合所驱动证明器的形式。

在这种情况下，溢出检查无法证明，因为溢出实际上可能发生。代码很容易通过重新排列表达式 (Size + 1) - J 中运算的顺序为 (Size - J) + 1 来修复。此更改导致生成的 WhyML 发生相应的更改，从而使证明成功。

为什么使用 Why3 这样的中间验证系统？为什么不直接从 SPARK 代码生成适合定理证明器处理的格式的证明任务呢？事实上，这正是 SPARK 2005

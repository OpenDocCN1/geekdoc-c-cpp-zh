

*产品配置建模语言* (PCML)。PCML 的实现基于这样的信念，即它可以支持一套实用且相关的销售配置任务。它包括分类法、组合结构、属性和约束。面向连接的概念（端口）甚至资源都被排除在外。PCML 的主要概念是 *特征类型*、它们的组合结构、*属性* 和 *约束*。特征类型定义了可在配置中出现的其 *个体* 的子特征（部件）和属性。Hotz 等人（2014）¹ 中介绍的 PC 配置模型的概述如图 26.1 所示。

PCML 的语义通过将 PCML 映射到权重约束规则语言（WCRL）提供，应用了 Soininen 等人（2001）的思想。*Smodels* 系统为 WCRL 提供了一个高效的推理引擎（Simons 等人，2002）。WCRL 和 *Smodels* 的开发考虑了配置作为潜在的应用领域。

### 26.2.1 分类层级和属性

*VariSales Modeling Tool* 提供特征类型、其类层级和属性的编辑。这包括创建、删除、重命名（保持模型一致性）以及更改子类层级。*特征类型树* 显示类层级（见图 26.1 左上角）并作为编辑类型的各个方面的起点。所选对象的编辑在显示的右侧进行，有时在弹出窗口中进行。在特征类型树中，彩色方块区分具体（蓝色）、抽象（红色）类型和配置类型（绿色）。该树显示了示例的完整分类层级。下面以文本 PCML 格式展示了其中一些以及 PC 的属性定义：

```
feature PC
    attribute usage
        value type string constrained by $
            in list("internet","scientific","multimedia")

    attribute efficiency
        value type efficiency_valueType constrained by $
            in list("A","B","C")
        no default
            constraint crc1
    ( ( usage = "internet" ) or ( usage = "multimedia" ) )
        implies present (InternetConn)
    feature PC_Component
        abstract
    feature InternetConn
        subtype of PC_Component
```

特征类型概述（图 26.1 右侧）允许添加或删除属性，并更改当前所选类型的抽象级别或名称。选项卡 Attributes 显示所选特征类型 PC 的属性概述。属性 efficiency 通过一种新的值类型定义——相同的定义需要在多个地方使用，并且可用的 efficiency 类容易发生变化。该值类型通过图形用户界面定义，以文本 PCML 形式为：efficiency_valueType string constrained by $ in list ("A", "B", "C")。

### 26.2.2 组合结构

特征类型通过一组子特征定义来定义其组合结构。子特征定义指定子特征名称、可能的子特征类型的一个非空集合（简称为允许类型）以及指示有效子特征数量的基数。

在配置中，特征个体的子特征（部件）由特征个体实现。实现特征个体“填充”由有效子特征定义创建的“角色”。当基数允许 0 时，显式的空实现是可能的。工业产品中常见的“可选部件”被建模为允许空实现的子特征。默认实现可以包括属性值和任意深度的子特征实现。此外，可以将空实现（特殊值 none）设为默认实现。继承的子特征可以通过限制允许类型、基数或通过修改或隐藏默认子特征实现来进行细化。

组合结构在子特征层级树中显示（图 26.1 和 26.2 左下角）。从特征类型树拖放可实现添加允许的特征类型、子特征定义和默认值。

图 26.2 右侧显示了特征类型 HDUnit 的子特征概述。每个 HDUnit 都有一个名为 HD_Controllers 的部件，包含 1 到 2 个 HDController 的任何子类型的个体，以及一个名为 Hard_disks 的部件，包含 1 到 4 个 HDisk 的任何子类型的个体。子特征未设置默认值。

在文本 PCML 表示中，对应的配置模型部分表达如下：

```
feature HDUnit
  subtype of PC_Component
```

![](img/214a17cc1f5bbf0914497c7414128438_336_0.png)

**FIGURE 26.2**

VariSales Modeling Tool 中 HDUnit 的组合结构。

```
subfeature Hard_disks
  allowed features HDisk
  cardinality 1 to 4

subfeature HD_Controllers
  allowed features HDController
  cardinality 1 to 2
```

### 26.2.3 约束

特征类型可以定义约束。在本示例中，我们仅应用硬约束，这些约束定义了正确配置必须满足的条件。配置仅在没有任何特征个体的硬约束被违反时才被认为是一致的。如果任何硬约束被破坏，购买流程就无法完成，例如，将配置放入购物车会被阻止。

约束以约束语言表达，并在特征类型内唯一命名。约束语言的第一级构建块是对子特征、特征的属性以及整数或字符串等常量的访问引用。引用可以连续使用，例如访问实现子特征的个体的属性。通过使用引用、常量和算术表达式构造返回布尔值的测试。测试包括检查特定引用个体是否存在或是否为给定类型的谓词。属性引用可以用常量在算术表达式中使用。这些可以用通常的关系运算符进行比较以创建测试。测试可以进一步使用标准布尔连接词组合成任意复杂的布尔表达式。

VariSales Modeling Tool 提供多种定义约束的方式：文本、图形和表约束。Tab Constraints（图 26.1）中的 Feature type overview 以文本形式列出活动特征类型的约束并便于添加新约束。

许多约束相对简单，通常以 requires- 和 incompatible- 关系的形式出现。为了使输入和修改简单约束更容易，VariSales Modeling Tool 具有图形约束编辑器。可以将 and 和 or 连接词用于创建子表达式。这些子表达式可以例如用作更复杂图形表达式中的要求、被要求或不兼容因素。

图 26.3 说明了约束 crc1（见表 26.1 和第 26.2.1 节的文本 PCML 表示），该约束是用图形约束编辑器创建的。首先对约束进行了命名，并将 requires 符号带到画布上。参数和子表达式通过拖放支持放置到位置。这使建模者免于繁琐且易出错的对象名称和值输入。

表 26.1 举例说明了我们示例 PC 配置知识库中约束的实现（见 Hotz 等人，2014²）。

### 26.3 价格和硬盘容量

VariSales 有两种确定价格的机制。基本定价机制应用简单的加法价格，而高级计算机制则允许自由指定的计算。示例 PC 的价格由基本机制确定，而高级计算机制用于计算硬盘资源生产和消耗。

基本定价机制很简单：每个特征个体都有其类型指定的价格；默认情况下无价格（0）。此外，每个属性值都可以给定价格。配置中特征个体的价格和属性值的价格在每次选择后在 Web 浏览器中求和。用户界面在选择实现特征类型或属性值的上下文中显示价格。例如，Screen 价格由 efficiency 的各个属性值的价格决定。其他价格如 CPU 的价格仅基于类型确定。PC 价格表的一部分（XML 格式）为：


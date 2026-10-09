
[de Champeau and Faure, 1992] D. DE CHAMPEAU and P. FAURE, 'A Comparative Study of Object-Oriented Methods,' Journal of Object-Oriented Programming 5 (March–April 1992), pp. 21–33.

[Embley, Jackson, and Woodfield, 1995] D. W. EMBLEY, R. B. JACKSON, and S. N. WOODFIELD, 'OO Systems Analysis: Is It or Isn't?' IEEE Software 12 (July 1995), pp. 18–33.

[Fichman and Kemerer, 1992] R. G. FICHMAN and C. F. KEMERER, 'Object-Oriented and Conventional Analysis and Methodologies: Comparison and Critique,' IEEE Computer 25 (October 1992), pp. 22–39.

[Harel and Gery, 1997] "Executable Object Modeling with Statecharts," IEEE Computer 30 (July 1997), pp. 31–42.

[Jacobson, Booch, and Rumbaugh, 1999] I. Jacobson, Booch, and J. Rumbaugh, The Unified Development Process, Addison-Wesley, Reading, MA, 1999.

[Jacobson, Christerson, Jonsson, and Overgaard, 1992] I. Jacobson, M. Christerson, P. Jonsson, and G. Overgaard, Object-Oriented Software Engineering: A Case Driven Approach, ACM Press, New York, 1992.

[Juristo, Moreno, and Lopez, 2000] N. Juristo, A. Moreno, and López, "How to Use Instruments for Object-Oriented Analysis," IEEE Software 17 (May–June 2000), pp. 80–89.

[Monarchi and Puhr, 1992] D. E. Monarchi and I. Puhr, "Research for Object-Oriented Analysis and Design," Communications of the ACM 35 (September 1992), pp. 35–47.

[Rumbaugh et al., 1991] J. Rumbaugh, B. Blaha, and W. Lorensen, Object-Oriented Modeling and Design, Prentice Hall, Englewood Cliffs, NJ.

[Rumbaugh, Jacobson, and Booch, 1999] J. Rumbaugh, I. Jacobson, and J. Booch, The Unified Modeling Language Reference, Addison-Wesley, Reading, MA, 1999.

[Selic, Gullekinson, and Ward, 1995] B. Selic,. Gullekinson, and P. Ward, Real-Time Object-Oriented Modeling, John Wiley and Sons, New York, 1995.

[USNO, 2000] "The 21st Century and the Millennium—When They Begin?" U.S. Naval Observatory, Astronomical Applications Department, aa.us.navy.mil/AA/docs/millennium1996.html, February 22, 2000.

[Williams, 1996] J. Williams, "Managing Iteration in OO Projects," IEEE Computer 29 (September–October 1996), pp. 39–43.

[Wirfs-Brock, Wilkerson, and Wiener, 1990] R. Wirfs-Brock, B. Wilkerson, and L. Wiener, Designing-Oriented Software, Prentice Hall, Englewood Cliffs, NJ.

# 第 14 章 设计

## 学习目标

学习本章后，你应该能够：

- 执行设计工作流。
- 执行面向对象设计。
- 执行数据流分析。

在过去的大约 40 年里，人们提出了数百种设计技术。有些是现有技术的变体；另一些与所提出的任何技术都完全不同。少数设计技术被数万名软件工程师使用；而许多仅被数百人使用。某些设计策略（特别是学术界制定的）具有坚实的理论基础。其他（包括许多）则更具实用性；是因为作者发现它们在实践中效果良好。大多数设计技术是手动的，但自动化正日益成为设计的重要方面，以协助文档管理。

尽管有如此多的设计技术，但某些底层模式显现出来。本书的一个大主题是：产品的两个本质方面是它的操作以及操作所作用的数据。因此，设计产品的两种基本方法是面向操作的设计和面向数据的设计。在面向操作的设计中，重点是操作。一个例子是数据流分析（第 14.3 节），其目标是设计高内聚模块（第 7.2 节）。在面向数据的设计中，首先考虑数据。例如，在 Jackson 技术（第 14.5 节）中，首先确定数据结构，然后设计过程以符合数据结构。

面向操作的设计技术的缺点是它们集中于操作；数据是次要的。面向数据的设计技术同样强调数据，从而损害了操作。解决方案是使用面向对象的技术，它赋予操作和数据同等的权重。在本章中，首先描述面向操作和面向数据的设计，然后是面向对象的设计。正如一个对象包含了操作和数据一样，面向对象的设计也结合了面向操作的设计和面向数据的设计特征。因此，为了充分理解面向对象设计，需要对面向操作和面向数据的设计有了解。

在检查具体的设计技术之前，必须对设计进行一些通性说明。

# 14.1 设计与抽象

经典的设计阶段包括三个活动：架构设计、详细设计和设计测试。设计过程的输入是规格文档，描述产品要实现的功能。输出是设计文档，描述如何实现这些功能。

在架构设计（也称为概要设计、逻辑设计或高层设计）期间，开发产品的模块化分解。也就是说，仔细分析规格，并产生具有所需功能的模块结构。该活动的输出是模块列表以及它们如何连接的描述。从架构的角度来看，在架构设计期间假设某些模块存在；然后在这些模块内部进行设计。

然而当在使用面向对象范式时（如第 1.9 节所示），架构设计是在面向对象分析工作流（第 12 章）中进行的。这是确定类的步。类是模块的一种；模块化分解是在分析工作流中进行的。

经典阶段的下一个活动以及面向对象设计工作流的主要活动是详细设计，也称为模块设计、物理设计或底层设计，在此期间每个模块（或类）都被详细设计。例如，选择特定的算法和数据结构。从架构的角度来看，在此活动中引入模块相互连接形成完整产品的概念。

# 14.2 面向操作的设计

第 7.2 节和 7.3 节为将产品分解为高内聚、低耦合模块提供了理论依据。我们描述了两种实现这一设计目标的实际经典技术：数据流分析（第 14.3 节）和事务分析（第 14.4 节）。理论上，只要规格可以用数据流图（DFD）表示，就可以应用数据流分析，因为（至少在理论上）每个产品都可以用 DFD 表示，所以数据流分析是通用的。在实践中，对于许多情况有更合适的设计技术，特别是对于数据流次于其他考虑因素的产品设计。在指示需要其他设计技术的情况下，例如基于规则的系统（专家系统）、数据库和事务处理产品。（第 14.4 节中描述的事务分析是将事务处理产品分解为模块的良好方法）。

## 14.3 数据流分析

数据流分析（DFA）是实现高内聚模块的经典设计技术。它通常与许多分析技术结合使用。这里将 DFA 结合结构化系统分析（第 12.3 节）介绍。该技术的输入是数据流图。关键点在于，如果已经构建了 DFD，软件设计人员就拥有关于产品输入和输出的精确完整的信息。产品将输入转换为输出。考虑图 14.1 所示的 DFD 表示的数据流。产品被输入并变成某种内部数据。然后，在后续一点，内部数据具有了输出属性。这在图 14.2 中显示得更详细。输入失去输入属性并简单成为产品处理的内部数据的这一点，就是输出的最高抽象点，它是数据流中可以被识别为输出而非某种内部数据的第一点。利用输入和输出的最高抽象点，将产品分解为三个模块：`input_module`、`transform_module` 和 `output_module`。依次取出每个模块，找到其最高抽象点并对模块进行分解。此过程一直持续直到每个模块都执行单一操作；即：

图 14.1 显示数据流和产品操作的数据流图。

![](img/fbae284627ff75e470d980b0ad1cc726_486_0.png)

图 14.2 输入和输出的最高抽象点。

![](img/fbae284627ff75e470d980b0ad1cc726_486_1.png)

### B 部分 软件生命周期的工作流

设计由具有高内聚的模块组成。因此，逐步细化（这是许多其他软件工程技术的基础）是数据流分析的基础。

公平地说，应该指出，可能需要对分解进行微调，以实现尽可能低的耦合性。数据流分析是实现高内聚的一种方法。组合/结构化设计的目标是高内聚，而且是低耦合。为了实现后者，有时需要对设计进行微调。例如，由于 DFA 没有考虑耦合性，在使用 DFA 构建的设计中可能会无意中产生控制流。在这种情况下，只需要修改两个模块，使得它们之间传递的是数据而不是控制流即可。

### 微型案例研究

#### 14.3.1 单词计数微型案例研究

考虑考虑设计一种产品，该产品接收一个文件作为输入并返回该文件中的单词数，类似于 UNIX 实用。

图 14.3 显示了数据流。共有五个模块。`read_file_name` 读取文件名，然后由 `validate_file_name` 进行验证。验证后的名称传递给 `count_number_of_words` 进行计数。计数结果传递给 `format_word_count`，格式化后的计数最终传递给 `display_word_count` 进行输出。

检查数据流，初始输入是 `file_name`。当经过 `validate_file_name` 时，它仍然是一个文件，因此没有失去其输入数据的属性。但考虑 `count_number_of_words`。它的输入是 `validated_file_name`，它的输出是 `word_count`。该模块的输出与整个产品的输入是完全不同的。显然，最高抽象点如图 14.3 所示。同样地，尽管来自 `count_number_of_words` 的输出经过了某种格式化，但它本质上是从其所属的模块 `count_number_of_words` 产生的输出。输出的最高抽象点如图 14.3 所示。

使用这两个最高抽象点对产品进行的分解如图 14.4 的结构图所示。该图还揭示了数据图 14.3 的数据流图有些简单。

# 图 14.3 数据流图的第一次细化。

![](img/fbae284627ff75e470d980b0ad1cc726_487_0.png)

# 图 14.4 结构图的第一次细化。

![](img/fbae284627ff75e470d980b0ad1cc726_488_0.png)

# 图 14.5 结构图的第二次细化。

![](img/fbae284627ff75e470d980b0ad1cc726_488_1.png)

DFD 没有显示当用户指定的文件不存在时发生什么的逻辑流连接。模块 `read_and_validate_file_name` 必须向 `perform_word_count` 返回一个 `status_flag`。如果名称无效，它会被 `perform_word_count` 忽略并打印某种错误信息。但如果名称是有效的，它就会被传递给 `count_number_of_words`。然而，通常存在条件数据流，需要一种控制流。

正如第 7.2.5 节所示，一个模块执行与产品将遵循的步骤顺序相关的系列操作，并且如果所有操作都在相同的数据上执行。在图 14.4 中，两个模块具有功能内聚：`read_and_validate_file_name` 和 `format_and_display_word_count`。这些必须进一步分解。最终结果如图 14.5 所示。所有模块都具有功能内聚，它们之间要么是数据耦合（第 7.3.5 节），要么没有耦合。

### B 部分 软件生命周期的工作流

现在架构设计已经完成，下一步是详细设计。在这里，选择了数据结构并选取了算法。图 14.6 的设计与编程语言无关。然而，如果管理层在详细设计开始之前决定了实现语言，那么使用程序描述语言（PDL）来表示详细设计是一个很有吸引力的选择（伪代码是 PDL 的早期称呼）。PDL 本质上由所选实现语言的控制语句组成。图 14.7 显示了

# 图 14.6 四个模块的详细设计。

| 模块名称 | 模块类型 | 返回类型 | 输入参数 | 输出参数 | 错误消息 | 的文件 | 修改的文件 | 调用的模块 | 叙述 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `read_file_name` | Function | string | None | None | None | None | None | None | 产品通过命令行字符串 `<file_name>` 被用户调用。使用操作系统调用，此模块访问命令字符串的内容，提取 `<file_name>` 并将其作为模块的值返回。 |
| `validate_file_name` | Function | Boolean | `file_name` : string | None | None | None | None | None | 此模块调用操作系统判断 `file_name` 是否存在。如果存在返回 true，否则返回 false。 |
| `count_number_of_words` | Function | integer | `validated_file_name` : string | None | None | None | None | None | 此模块确定 `validated_file_name` 是否为文本文件，即按字符划分的文件。如果是，模块返回文本文件中的单词数；否则，返回 -1。 |
| `produce_output` | Function | void | `word_count` : integer | None | None | None | None | `format_word_count`, `display_word_count` | 此模块接收调用模块传递的整数 `word_count`，并调用 `format_word_count` 根据规格对该整数进行格式化。然后调用 `display_word_count` 打印该行。 |

# 图 14.6（续）

# 472 部分 B 软件生命周期的工作流

# 图 14.7

```cpp
void perform_word_count ()
{
    String validated_file_name;
    Int word_count;

    if (get_input (validated_file_name) is null)
        print "error 1: file does not exist";
    else
    {
        set word_count equal to count_number_of_words (validated_file_name);
        if (word_count equal to -1)
            print "error 2: file is not a text file";
        else
            produce_output (word_count);
    }
}

String get_input ()
{
    String file_name;
    file_name = read_file_name ();
    if (validate_file_name (file_name) is true)
    {
        return file_name;
    }
    else
        return null;
}

void display_word_count (String formatted_word_count)
{
    print formatted_word_count, left justified;
}

String format_word_count (int word_count)
{
    return "File contains" word_count "words";
}
```

该示例中四个方法的详细设计的 PDL（伪代码）表示。

产品其余四个模块的详细设计是使用带有 C++ 或 Java 风格的 PDL 编写。PDL 的优点是它通常清晰且简洁，实现步骤通常仅仅是将注释翻译成相关的编程语言。缺点是，有时设计者倾向于进入过多的细节，并产生模块的完整代码实现，而不是 PDL 详细设计。

在完成完整的文档编制并成功测试后，详细设计将交给实现团队进行编码。产品继续经典软件生命周期的剩余阶段。

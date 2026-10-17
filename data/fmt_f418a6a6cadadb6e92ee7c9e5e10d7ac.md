
/**
 * Initialize the board by placing ships to cover numCovered coords.
 *
void init(P:)**/(int)numCovered) {
 // Here what we would do in a full system is make a call to
 // some non-Jif function, through the runtime interface, to
 // get the position of the ships to place. That function would
 // either-return status or would implement some
 // strategy. Here we fake it with fixed positions for
 // ships;
 final Ship*(P:)** = myCunningStrategy = {
 new Ship*(P:)**/(Coordinate/(P:))**/(1, 1), 1, true);
 new Ship*(P:)**/(Coordinate/(P:))**/(1, 3), 2, false);
 new Ship*(P:)**/(Coordinate/(P:))**/(2, 2), 3, true);
 new Ship*(P:)**/(Coordinate/(P:))**/(3, 4), 4, false);
 new Ship*(P:)**/(Coordinate/(P:))**/(5, 6), 5, true);
 new Ship*(P:)**/(Coordinate/(P:))**/(5, 7), 6, false);
 };

 Board*(T:)**board = this board;
 int i = 0;
 for (int count = numCovered; count > 0 && i != null; ) {
 try {
 Ship*(P:)**/newPiece = myCunningStrategy(i++);
 if (newPiece == null && newPiece.length > count) {
 // this ship is too long
 newPiece = new Ship*:(P:)**/(newPiece.pos, count);
 }
 board.addShip(newPiece);
 count -= (newPiece==null?0:newPiece.length);
 }
 catch (ArrayIndexOutOfBoundsException ignored) {
 catch (IllegalArgumentException ignored) {
 // two ships overlapped. Just try adding the next ship
 // instead;
 }
}
```

图 7.3：战舰中 `Player` 的初始化方法

## 第 7 章. 评估

方法，更准确地说，由于这些方法中可能抛出的异常。然而，更仔细的检查发现所有这些异常控制流路径实际上都是不可能的。

例如图 7.3 中的初始化方法。如果程序检查 SSA 变量是否为 null，并且只有在它不为 null 时才执行涉及它的指令（参见第 25 行），则可能在该指令处抛出空指针异常。然而，我们的中间表示目前无法检测到这一点，即使中间表示中存在两个相同的 null 检查，一个紧随另一个。Jif 似乎支持某种局部推理。但即使是平凡的示例，其中 final 值在构造函数中定义，在任何实例中都可能永远不为 null。such cases can be detected, in the procedural case [Hu08]. Jif 只能在有额外的用户标注时支持非局部推理。

除空指针问题外，我们还发现了到数组存储的异常控制流，其中 Jif 必须确保存储的值是数组组件的实例，因为 Java 的协变数组异常。当类型为 a[] 的数组变量被类型为 b[] 的数组赋值时，存储 a 类型的对象到其中会抛出 `ArrayStoreException`（参见图 7.3 第 11-17 行）Jif 似乎具有局部推理来修剪平凡情况。我们的表示不修剪此类情况，使用我们用于依赖的指针分析结果，impossible control flow 可能会到达。

最后，对于过程间分析，我们发现我们的表示为所有方法建模异常返回值，即使方法保证不抛出任何异常。更精确地建模此类情况可以使调用方法中的控制流更精确并消除虚假的隐式流。Jif 对此类情况使用用户标注，因为所有可能抛出的异常必须被捕获或声明，通常 Java 中不得声明的 RuntimeExceptions。

目前，我们的工具不提供此类分析，因此只能通过外部手段检测此类异常。或者通过人工检查，定理（例如 /post conditions）或路径条件。在验证此类流不可能后，我们可以阻止依赖图中的相应路径，并且我们用 declassification 来做到这一点。与正常 declassification 不同，信息流是可能但必要的，这种 declassification 模拟了没有信息流的保证。作为未来，我们计划集成修剪不可能控制流的分析以降低误报率，从而减轻外部验证的负担。

在阻止 `Player` 初始化中通过异常的信息流后，我们的 IFC 算法证明了战舰相对于所述安全策略是安全的。未发现进一步的非法信息流。在基于四个 declassifications 的安全分析期间，创建了 728 个摘要 declassification 节点。这一结果表明摘要分类节点有效地影响分析精度，因为它们允许在方法调用站点阻止传递信息流的同时进行上下文敏感切片。Instead they introduce a declassification that summarizes the declassification

## 7.3. 信息流控制

被调用方法的效果。请注意，原生的 Jif 程序包含约 150 条注解（在图 7.3 中显示为灰色注释），其中大部分涉及安全类型。 然而，其中一些注解涉及主体及其权限。 这是我们在当前不支持的去中心化标签模型的一个特性。 注解的数量比我们的分析高出至少一个数量级。 对于一个仅包含 500 行代码（包括注释）的程序，这意味着 Jif 的注解负担是相当大的。

切片式 IPC 需要的注解比类型少的一个原因在于，方法的副作用在依赖图上是显式的，因此不需要终结标签（它模拟副作用对程序计数器的影响），另一个返回值或显式标签。 这些是作为表示被调用方法的依赖关系的概要信息计算得出的。
除此之外，Jif 需要注解来验证任何非平凡的属性，除了控制流。 特别是，像非空性这样的前置条件必须包含在程序文本中而不是其注解中，空指针或子句的显式标签，通常随后是空的处理程序，如图 4.6 第 96 页所示的示例。 因此，前置条件被包含为运行时检查以实现局部推理。 这种编码风格对于软件工程视角来说是一种折磨，因为它意味着源代码理解，并且可能掩盖被违反的条件。 人们真正想要的是验证此类情况在任何执行中都不会发生，因此不需要包含在源代码中。

### 7.3.5 可扩展性

上一节展示了我们方法的精确性和实用性。 为了验证我们新的基于切片的信息流控制的可扩展性，我们在具有不同数量的去分类并且使用具有不同特征的格的多个基准上测量了执行时间。 基准程序与第 160 页表 7.1 中的相同，除了金属工人协议的实现程序 [AS05]。 该程序显示以下特征：其源代码长 4750 行（包括所有必要的库和存根共 18801 行），生成的 SDG 包含 27175 个节点和 204532 条边，在磁盘上占用约 36MB。 计算 SDG 的时间为 141 秒，加上概要边的 247 秒。

7.3 显示了我们在评估中使用的格的特征：第一列显示格中节点的数量，第二列显示格的最大高度。 格中不纯节点的数量显示在下一列，表示格中具有多于一个父节点的节点。 最后一列显示在 Ganguly 等人 [GMR94] 的高效位编码中所需的位数。 该编码允许近乎常数地计算下确界（最大下界），这对于我们的评估至关重要。 格已被设计为以相同的方式覆盖不同的特征：格 A 是一个传统的链，格 B 更平坦并且包含一个不纯节点。 格 F 是通过从 9 个元素的完整子集中随机删除边自动生成的。 转换为位表示仅对传递约简序是可能的，这不能通过随机删除序边来保证。 我们在位转换前包含了一个约简阶段。 有趣的是，表 7.3 说明位转换通常会产生大小与格节点数量成线性的表示。

> 下确界计算实际上是常数，但我们需要哈希将格元素映射到位集。

## 第 7 章. 评估

| nodes | height | impure | bits |
| Lattice A | 5 | 5 | 0 | 6 |
| Lattice B | 8 | 4 | 1 | 5 |
| Lattice C | 8 | 6 | 2 | 10 |
| Lattice D | 12 | 8 | 2 | 14 |
| Lattice E | 24 | 11 | 7 | 25 |
| Lattice F | 256 | 9 | 246 | 266 |

表 7.3：评估中格的特征。

![](img/27c6595637bae6b27613772d7079f8a2_187_0.png)

图 7.4：IFC 分析的执行时间（y 轴，秒）对于 unionfind 基准，使用不同的格和不同数量的去分类（x 轴）

图 7.4 显示了 100 次 IFC 分析的平均执行时间（y 轴，秒）对于 unionfind 基准表 7.1，使用表 7.3 的格。 我们选择 unionfind 基准，因为它具有最长的执行时间，而其他基准本质上显示相同的特征。 对于所有 IFC 分析，我们用 100 个随机安全级别对 SDG 进行了注解，如提供

![](img/27c6595637bae6b27613772d7079f8a2_188_0.png)

图 7.5：unionified 不同格和不同数量的去分类（x 轴）的概要去分类节点的耗时（秒）

和所需的安全级别，分别。 此外，我们创建了 5 到 500 个随机去分类以衡量去分类对 IFC 检查的影响（显示在 x 轴上）。 这些数字说明我们的 IFC 算法相当独立于格的结构和大小。 特别是，我们得到了相对于格（和位集大小）的执行时间的亚线性增长。 除此之外，随着去分类数量的增加，我们的实验中增长超过线性（x 轴）。 图 7.5 显示了计算概要去分类节点所花费的执行时间，这是精确 IFC 检查的先决条件（参见第 4.8 节），它们已针对程序、格和去分类的每个组合获取。 它们是用与图 7.4 的数字相同的随机注解确定的。 请注意，我们只在节点之间连接概要信息，这些节点原本通过时间和格大小或去分类数量，分别连接。 这些边揭示了

图 7.6 和 7.7 显示了 100 次 IFC 分析的平均执行时间（y 轴，秒）和概要去分类节点计算的时间，分别，对于所有基准程序使用最大的格和不同数量的去分类。 该图中的线条使用右侧显示的比例，而条形使用不同的比例，因此所包含的程序耗时不到一分钟，只有三个程序需要更长时间，即 purse 和 unionfind。 再次，我们发现执行时间与去分类数量之间的相关性是亚线性的。 事实上，许多基准在 500 个去分类时的执行时间低于 100 个。 这个数字清楚地说明了我们信息流控制分析的可扩展性。 依赖图中的节点数量与分析时间之间没有明显的相关性。

## 第 7 章. 评估

![](img/27c6595637bae6b27613772d7079f8a2_189_0.png)

图 7.6：所有基准程序的 IFC 分析的平均执行时间（y 轴，秒），使用最大的格和不同数量的去分类（x 轴）。 条形使用不同的比例。

然而，似乎 SDG 中边的数量与执行时间之间存在相关性。 与切片不同，我们的 IFC 分析在 SDG 节点和边的数量上不是线性的，但必须在给定格的约束系统中找到不动点，然而可能在 SDG 中遍历一个循环，因为格很高，并且当需要循环时这种效应可能会更糟。 我们当前的实现没有规避这些影响，可以观察到具有最多边的程序会导致分析时间的实质性增加。 但最大的程序 mp 不属于离群值而具有良好的自然。 一个原因可能是不同的程序结构，这也可以从原始概要边计算中看出（参见表 7.1），这比其他大型程序要低得多。 该程序——不像 JavaCard 小程序和我们的学生程序——没有在主方法中包含一个大循环，该循环可能调用几乎所有功能。 总之，我们认为程序的结构对分析时间的影响比纯粹的节点或边的数量更大。

虽然未来的工作必须评估切片优化对不动点计算的影响，但我们认为 1 分钟的执行时间，正如我们大多数测试用例所观察到的那样，对于安全分析来说绝对是合理的。 但即使是三个离群值也最多需要 1.5 小时（包括概要去分类分析），这对于通常只需要做一次的编译时分析来说应该是可以接受的。

# 7.4. 路径条件的案例研究

![](img/27c6595637bae6b27613772d7079f8a2_190_0.png)

图 7.7：所有基准程序在最大格子和不同数量的去分类（x轴）下，汇总去分类节点的耗时（y轴，秒）。条形图使用不同的刻度。

### 7.3.6 未来工作

虽然我们提供了关于精度、可扩展性和实用性的证据，但仍有进一步改进的空间。特别是，我们预计切片的优化，例如 Binkley 等人提出的 [BHK07]，同样适用于我们的信息流。这些技术可将运行时间减少高达 71%，从而显著提高可扩展性。进一步的研究必须评估哪些技术适用于信息流控制。

## 7.4 路径条件的案例研究

路径条件是两个语句之间信息流的精确必要条件。因此它们可以使上一节中介绍的技术所确定的信息流失效或指定其精确条件。此外，它们提供了导致去分类的情形的洞察，从而为此类构造提供语义上的合理性。本节介绍的案例研究展示了第 5 章中介绍的扩展的可行性和精度。首先，我们将重点关注如第 5.3 节所述的 Java 的静态路径条件，参见第 5.4 节）将对 C 进行评估。请注意，本节中呈现的所有条件均由当前原型生成。

```
public class Weighing {
    public static final int NORMAL = 0;
    public static final int PAPER_OUT = 1;
    public static void main(String[] args) {
        char input = args[0].charAt(0);
        weigh(PAPER_OUT, 1.0f, input);
    }
    public static void weigh(int status, float kal_kg, char input) {
        float u = 1.0f; // calibration factor
        float u_kg = 0.0f; // initial value
        while (true) {
            u_kg = * kal_kg;
            if (status == PAPER_OUT) {
                if (input == '+') {
                    kal_kg = 1.1f;
                }
                if (input == '-') {
                    kal_kg = 0.9f;
                }
            }
            print(u_kg);
        }
    }
    public static void print(float u_kg) {...}
}
```

图 7.8：简化的称重机控制器

```
( NOT Weighing.print((1.0 * kal_kg))
++ (input = 43)
++ (1 = 1 )
NOT Weighing.print((1.0 * kal_kg))
++ (input != 43)
++ (input = 45 )
++ (1 = 1 )
```

图 7.9：图 7.8 中第 9 行（input）到 22 行的路径条件

# 第 7 章 评估

```
public class PCExc {
    int secret;
    public static void main(String[] args) {
        System.out.println(excMethod(1));
    }
    public static int excMethod(int check) {
        try {
            PCExc pce = new PCExc();
            pce.secret = check;
            throw pce;
        } catch (PCExc pce) {
            return pce.secret;
        }
    }
}
exc_O instanceof PCExc
++ (exc_O != null)

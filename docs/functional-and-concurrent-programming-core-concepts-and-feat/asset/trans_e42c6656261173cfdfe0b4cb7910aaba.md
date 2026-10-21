

## 第10章 标准高阶函数

同样，

```
for load <- loads do load.reduce()
```

用于更新可变对象的列表。它被编译为

```
loads.foreach(load => load.reduce())
```

当 for-do 和 for-yield 使用条件时，编译器会插入一个过滤步骤。表达式

```
for load <- loads if load.weight != 0 yield load.reduced
```

被编译为

```
loads.withFilter(load => load.weight != 0).map(load => load.reduced)
```

列表 10.8 为二叉树添加了方法 foreach。因此，你现在可以使用 for-do 处理树：

```
val tree: BinTree = ...
```

```
for x <- tree do println(x) // 按顺序打印树中的所有值
```

for-do 表达式被编译为 tree.foreach(println)。

许多库实现了 foreach、map、flatMap 和 filter 函数，但很少有编程语言定义与 Scala 相同的 for-comprehension 语法。一些构造是相似的，比如 Python 的列表推导式。Python 代码

```
[round((temp - 32) / 1.8) for temp in temps if temp > 75]
```

对应于以下 Scala 代码：

```
for temp <- temps if temp > 75 yield ((temp - 32) / 1.8f).round
```

方法 withFilter 在语义上等同于 filter，但使用延迟求值的形式来避免创建中间列表（参见第 12.9 节中关于视图和惰性求值的讨论）。

在 Java 中，它只有高阶函数，你需要直接使用 filter 和 map：

```
Java
IntStream temps = ...
temps.filter(temp -> temp > 75).map(temp -> Math.round((temp - 32) / 1.8f))
```

### NOTE

鉴于我希望为开发者准备多种语言，我经常在代码示例中使用高阶函数而不是 for-do 或 for-yield，尤其是在案例研究之外。这是出于教学原因做出的选择，以更好地强调跨语言模式的相似性，但这往往会导致 Scala 代码并不总是符合惯用法。有 Scala 经验的读者会原谅我。

## 10.10 总结

- 本章介绍的函数构成了在函数式库中常见的核心高阶函数集合。它们通常可用于多种类型，例如流和集合，但也包括选项和未来。
- 若干函数使用谓词——一个布尔函数——作为其参数。它们用于查找、计数、过滤或断言存在满足该谓词的元素。
- 函数 map 用于对结构内的元素应用任意转换，并生成包含转换后值的新的结构。如果操作仅为产生副作用而应用于元素，且不需要结果结构，则可以使用函数 foreach 代替 map。
- 函数 flatMap 与 map 类似，但负责“展平”嵌套结构，如列表的列表或选项的选项。此函数功能强大，可用于将具有可选输出的计算应用于可选输入（以避免选项的选项），或处理触发新事件流的事件（以避免流的流），或异步转换本身异步计算的值（以避免未来的未来）。
- 从根本上说，foreach、map、flatMap 和 filter（或 withFilter）用于从结构外部转换结构的内容（例如，列表、选项、未来）。这种常见模式有时由语言级别的语法支持，如 Scala 的 for-comprehension 或 Python 的列表推导式。
- 折叠函数用于使用组合运算符将结构的元素归约为单个值。许多会迭代处理集合元素的计算都可以用折叠函数实现。
- 相反，高阶函数可用于生成元素集合。例如，函数 iterate 和 unfold 就依赖于初始种子和函数的重复应用来生成一系列值。
- 最小值、最大值和排序等需要元素比较的计算，需要通过用于比较值的标准来参数化。高阶变体通常使用比较函数（例如，`sortWith`）或映射到现有有序类型（例如，`sortBy`、`maxBy`）。
- 作为排序或最小/最大值计算的比较标准的替代，有时使用分组标准来收集相关元素（例如，`groupBy`）。
- 除了这个基本核心组之外，还存在许多其他高阶函数。例如，RxJava 响应式库的 `Observable` 类有超过一百个高阶方法，其中一些处理错误处理、线程或实时问题，除本章讨论的核心函数式转换之外。

目录中的节点列表绝不能包含两个同名的节点。节点列表的顺序无关紧要：包含相同文件和子目录但顺序不同的目录被视为等价。树是不可变的：添加或删除文件和目录是通过产生新树的函数实现的。

## 11.2 一个节点搜索辅助函数

几个树操作需要更新目录的子节点列表。这需要按名称在列表中查找节点，删除它，并可能用新节点替换它。为此目的定义了以下辅助方法：

// inside class Dir
def removeByName(name: String): Option[Node, List[Node]] =
  nodes.partition(_.name == name) match
    case (Nil, _)             => None
    case (List(found), others) => Some((found, others))
```

高阶方法 `partition` 用于将节点列表划分为具有给定名称的节点（最多一个）和具有不同名称的节点。如果没有具有给定名称的节点，函数返回 None。否则，它返回一个包含被提取的节点和剩余节点列表的对。作为示例，如果你在包含目录/文件 A、B、C 和 D 的节点列表中查找名称 B，该方法返回对：`(B, [A,C,D])`。

## 11.3 字符串表示

文件和目录都定义了 `toString` 方法，返回其名称。为了帮助区分文件和目录，会在目录名称后添加斜杠：

// inside class Dir
override def toString = name + "/"

// inside class File
override def toString = name
```

目录还定义了方法 `ls` 按名称列出其内容，以及方法 `lsFiles` 仅列出文件的名称，忽略子目录。你可以通过使用高阶方法 map 从节点列表生成字符串列表来实现

ls。对于 lsFiles，你使用 flatMap 来保留文件的名称并跳过子目录：

// inside class Dir
def ls: List[String] = nodes.map(_.toString)

def lsFiles: List[String] = nodes.flatMap {
  case file: File => List(file.toString)
  case _ => Nil
}
```

除了 ls 和 lsFiles 之外，你可能还想构建一个表示目录整个内容的字符串，包括子目录。为了强调树结构，文件和目录名称会根据其深度缩进。图 11.1 显示了文件系统树及其字符串表示。

![](img/74309e2bdd93f68d2e94338a3d73517f_197_0.png)

# 图 11.1 文件系统树及其字符串表示。

为了高效实现此方法，你可以创建一个字符串构建器并使用递归将行添加到其中，树中每个文件和目录各一行。为了实现缩进，每行以前缀开头，前缀由分隔符的重复组成（图 11.1 中的分隔符是一个点）。方法 mkString 分配一个字符串构建器和一个空前缀，并将递归委托给另一个也名为 mkString 的方法，其职责是将行添加到构建器中：

// inside trait Node
def mkString(sep: String): String = mkString(sep, StringBuilder(), "").result()
def mkString(sep: String, builder: StringBuilder, prefix: String): StringBuilder
```

这里使用方法 flatMap 来组合过滤（保留文件，忽略目录）和映射（将文件转换为其名称）。或者，lsFiles 可以用 filter 和 map 来编写。

这与 Unix 系统上常见的 tree 命令类似。



# 使用 final 变量

```java
final int THRESHOLD = 300;
if (p.get(X) < THRESHOLD) // 好的
```

# 大括号

左括号和右大括号必须对齐，无论是水平还是垂直方向：

```
while (i < n) { System.out.println(a[i]); i++; }
```

```
while (i < n)
{
    System.out.println(a[i]);
    i++;
}
```

有些程序员不会对齐垂直的大括号，而是将 `{` // 放在 ... 单词的后面：

```java
while (i < n) { // 不要这么做
System.out.println(a[i]);
    i++;
}
```

这样做会很难检查括号是否匹配。

# 不稳定的布局

有些程序员对对齐代码中的某些列感到非常自豪：

```
firstRecord = other.firstRecord;
lastRecord = other.lastRecord;
cutoff = other.cutoff;
```

这无疑是整洁的，但这种布局在变化时是不稳定的。如果一个新变量名长于预留列数的长度，你就必须移动所有条目：

```
firstRecord = other.firstRecord;
lastRecord = other.lastRecord;
cutoff = other.cutoff;
marginalFudgeFactor = other.marginalFudgeFactor;
```

这正是那种让你决定改用像 `mff` 这样的短变量名的陷阱。随着程序的变化，请使用易于维护的简单布局。

# 术语表

**抽象类 (Abstract class)** 一个不能被实例化的类。

**抽象方法 (Abstract method)** 一个只有名称、参数变量类型和返回类型，而没有实现的方法。

**访问器方法 (Accessor method)** 一个访问对象但不改变它的方法。

**聚合 (Aggregation)** 类与类之间的“拥有”（has-* a）关系。

**算法 (Algorithm)** 解决问题的一种无歧、可执行且可终止的规范。

**匿名类 (Anonymous class)** 没有名字的类。

**匿名对象 (Anonymous object)** 不存储在具名变量中的对象。

**API (应用程序编程接口)** 用于构建程序的代码库。

**API 文档 (API Documentation)** 关于 Java 库中每个类的信息。

**Applet (Applet)** 在 Web 浏览器或 applet 查看器内部执行的图形化 Java 程序。

**参数 (Argument)** 在方法调用中提供的值，或由运算符组合的值之一。

**数组 (Array)** 存储在连续内存位置的相同类型值的集合，每个值都可以通过整数索引访问。

**列表 (Array list)** 一个实现动态可增长对象数组的类。

**赋值 (Assignment)** 将新值放入变量中。

**关联 (Association)** 类之间的一种关系，其中可以可以通过跟随对象引用，从一个类的对象导航到另一个类类的对象。

**非对称边界 (Asymmetric bounds)** 包含起始索引但不包含结束索引的边界。

**属性 (Attribute)** 对象负责维护的命名属性。

**自动装箱 (Auto-boxing)** 自动将原始类型转换为包装类型。

**平衡树 (Balanced tree)** 一种树，其中每个子树都具有以下属性：左侧后代数量与右侧后代数量大致相等。

**大O符号 (Big-Notation)** 符号 `$g(n) = O(f(n))$` 表示函数 `$g$` 的增长速率受函数 `$f$` 关于 `$n$` 的增长速率的限制。例如，`$10n^2 + 100n = O(n^2)$`。

**二进制文件 (Binary file)** 值以二进制形式存储且无法作为文本读取的文件。

**二进制运算符 (Binary operator)** 接受两个参数的运算符，例如 `+` `$x + y$`。

**二分查找 (Binary search)** 一种在排序数组中查找值的快速算法。它每一步都将搜索范围缩小到数组的一半。

**二分搜索树 (Binary search tree)** 一种二叉树，其中每个子树具有以下属性：所有左后代都小于存储在根节点的值，所有右后代都更大。

**二叉树 (Binary tree)** 一种每个节点最多有两个子节点的树。

**位 (Bit)** 二进制数字；信息的最小单位，有两个可能的值：0 和 1。一个由 `$n$` 位组成的数据元素有 `$2^n$` 个可能值。

**黑盒测试 (Black-box testing)** 在不知道方法实现的情况下测试方法。

**块 (Block)** 由 `{ }` 括起来的一组语句。

**布尔运算符 (Boolean operator)** 可以应用于布尔值的运算符。Java 有三个布尔运算符：`&&`、`||` 和 `!`。

**布尔类型 (Boolean type)** 有两个可能值的类型：true 和 false。

**边框布局 (Border layout)** 一种布局管理方案，将组件放置在容器的中心或四个边界之一。

**边界测试用例 (Boundary test case)** 涉及合法值边界值的测试用例。例如，如果一个方法适用于所有非负整数，那么零就是一个边界测试用例。

**越界错误 (Bounds error)** 尝试访问范围之外的元素。

**break 语句 (break statement)** 终止循环或 `switch` 语句的语句。

**缓冲区 (Buffer)** 用于存储已产生（例如用户产生的字符）并等待被消费（例如读取）的临时存储器。

**DTD (文档类型定义)** 一系列描述 SGML 或 XML 文档中每个元素类型合法的元素和属性的规则序列。

**动态方法查找 (Dynamic method lookup)** 在运行时选择要调用的方法。在 Java 中，动态方法查找会考虑隐式参数对象的类，以选择合适的方法。

**编辑器 (Editor)** 用于编写和修改文本文件的程序。

**嵌入式系统 (Embedded system)** 包含在计算机以外设备中的处理器、软件和支持性电路。

**封装 (Encapsulation)** 对实现细节的隐藏。

**枚举类型 (Enumeration type)** 一种具有有限数量值的类型，每个值都有其特定的符号名称。

**转义字符 (Escape character)** 文本中一种不按字面意思处理，而是与其后的字符结合时具有特殊含义的字符。Java 字符串中的 `\` 转义字符。

**转义序列 (Escape sequence)** 以转义字符开头的字符序列，例如 `\n` 或 `\"`。

**事件 (Event)** 参见用户界面事件。

**事件类 (Event class)** 包含有关事件的信息，例如其来源。

**事件适配器 (Event adapter)** 一种通过定义所有什么都不做操作的方法来来实现事件监听器的类。

**事件处理器 (Event handler)** 在事件发生时被执行的方法。

**事件监听器 (Event listener)** 一个在事件发生时由事件通知的对象。

**异常 (Exception)** 一种表示阻止程序正常运行的条件的类。当发生此类条件时，会抛出一个该异常的实例。

**异常处理器 (Exception handler)** 当特定类型的异常被抛出并捕获时，被赋予控制权限的语句序列。

**显式参数 (Explicit parameter)** 除调用方法的对象之外的方法的参数。

**表达式 (Expression)** 由常量、变量、方法调用以及执行这些操作的算符组成的语法结构。

**扩展名 (Extension)** 文件名的最后几个部分，用于指定文件类型。例如，`.java` 表示一种文件类型。

**斐波纳契数字 (Fibonacci numbers)** 数字序列 1, 1, 2, 3, 5, 8, 13, ...,，其中每一项都是其前几项之和。

**文件 (File)** 存储在磁盘上的字节集合。

**文件指针 (File pointer)** 随机访问文件中下一个要读取或写入的字节的位置。它可以移动以便访问文件中的任何字节。

**finally 块 (finally block)** `try` 块的一部分，无论如何退出 `try` 块都会执行。

**标志位 (Flag)** 参见布尔类型。

**浮点数 (Floating-point number)** 可以具有小数部分的数字。

**流式布局 (Flow layout)** 一种布局管理方案，其中组件向右对齐。

**刷新流 (Flushing stream)** 将仍保留在缓冲区中的所有字符发送到其目的地。

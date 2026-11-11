

```bash
java -ea:... -da:MyClass MyApp
```

有些类不是由类加载器加载，而是由虚拟机直接加载。你可以使用这些开关有选择地启用或禁用这些类中的断言。

然而，用于启用或禁用所有断言的 `-ea` 和 `-da` 开关并不适用于没有类加载器的“系统类”。请使用 `-enablesystemassertions/-esa` 开关来启用系统类中的断言。

也可以通过编程方式控制类加载器的断言状态。请参阅本节末尾的 API 说明。

![](img/0e7b74ef51a065c077b42cd87b362288_599_0.png)

> **注意：**
>
> Java 库的源代码中有四百多个被注释掉的断言。有些程序员在测试后会将断言注释掉，因为否则它们会占用类文件中的空间。如果你对此有顾虑，可以按如下方式有条件地包含它们：

```java
public static final boolean asserts = true;  // Recompile with false for production
...
if (asserts) assert x >= 0;
```

### 7.4.3 使用断言进行参数检查

Java 语言为你提供了三种处理系统故障的机制：

- 抛出异常
- 记录日志
- 使用断言

什么时候应该选择断言？请记住以下几点：

- 断言失败旨在表示致命、不可恢复的错误。
- 断言检查仅在开发和测试期间开启。（这有时被开玩笑地描述为“在靠近岸边时穿上救生衣，一旦到了海洋中间就把它扔下船。”）

因此，你不会使用断言向程序的其他部分发出可恢复条件的信号，也不会用断言向程序用户传达问题。断言只应用于在测试期间定位程序内部错误。

让我们看一个常见场景——检查方法参数。你应该使用断言来检查非法的索引值或空引用吗？要回答这个问题，你必须查看该方法的文档。假设你实现了一个排序方法。

```java
/**
   Sorts the specified range of the specified array in ascending numerical order.
   The range to be sorted extends from fromIndex, inclusive, to toIndex, exclusive.
   @param a the array to be sorted.
   @param fromIndex the index of the first element (inclusive) to be sorted.
   @param toIndex the index of the last element (exclusive) to be sorted.
   @throws IllegalArgumentException if fromIndex > toIndex
   @throws ArrayIndexOutOfBoundsException if fromIndex < 0 or toIndex > a.length
*/
static void sort(int[] a, int fromIndex, int toIndex)
```

文档说明，如果索引值不正确，该方法会抛出异常。该行为是该方法与其调用者之间约定的一部分。如果你实现该方法，就必须遵守该约定并抛出指定的异常。改用断言是不合适的。

你应该断言 `a` 不为 `null` 吗？这同样不合适。方法文档未说明当 `a` 为 `null` 时该方法的行为。调用者有权假定在这种情况下方法会成功返回，而不会抛出断言错误。

然而，假设方法约定略有不同：

```text
@param a the array to be sorted (must not be null).
```

现在，该方法的调用者已被明确告知，使用空数组调用该方法是非法的。那么该方法可以以如下断言开头

```java
assert a != null;
```

计算机科学家将这种约定称为*前置条件*。原始方法对其参数没有前置条件——它承诺在所有情况下都具有明确定义的行为。修订后的方法有一个前置条件：`a` 不为 `null`。如果调用者未能满足该前置条件，那么一切都不再有保证，方法可以为所欲为。事实上，在加入断言后，该方法被非法调用时会表现出相当不可预测的行为。它有时抛出断言错误，有时抛出空指针异常，具体取决于其类加载器的配置方式。

### 7.4.4 使用断言记录假设

程序员经常使用注释来记录其底层假设。考虑来自 http://docs.oracle.com/javase/8/docs/technotes/guides/language/assert.html 的以下示例：

```java
if (i % 3 == 0)
    . . .
else if (i % 3 == 1)
    . . .
else // (i % 3 == 2)
    . . .
```

在这种情况下，改用断言非常合理。

```java
if (i % 3 == 0)
    . . .
else if (i % 3 == 1)
    . . .
else
{
    assert i % 3 == 2;
    . . .
}
```

当然，彻底思考这个问题会更有意义。`i % 3` 可能的值有哪些？如果 i 为正数，余数必定是 0、1 或 2。如果 i 为负数，那么余数可以是 −1 或 −2。因此，真正的假设是 i 不为负数。更好的断言应该是

```java
assert i >= 0;
```

放在 if 语句之前。

无论如何，这个示例展示了断言作为程序员自检工具的良好用法。如你所见，断言是用于测试和调试的战术性工具。相比之下，日志记录是贯穿程序整个生命周期的战略性工具。我们将在下一节探讨日志记录。

| API | 描述 | 版本 |
|---|---|---|
| **java.lang.ClassLoader** |  | 1.0 |
| `void setDefaultAssertionStatus(boolean b)` | 为此类加载器加载的、没有显式类或包断言状态的所有类启用或禁用断言。 | 1.4 |
| `void setClassAssertionStatus(String className, boolean b)` | 为给定类及其内部类启用或禁用断言。 | 1.4 |
| `void setPackageAssertionStatus(String packageName, boolean b)` | 为给定包及其子包中的所有类启用或禁用断言。 | 1.4 |
| `void clearAssertionStatus()` | 移除所有显式的类和包断言状态设置，并为此类加载器加载的所有类禁用断言。 | 1.4 |

## 7.5 日志记录

每位 Java 程序员都熟悉这样的过程：在出问题的代码中插入对 `System.out.println` 的调用，以深入了解程序行为。当然，一旦你找出问题的原因，就会删除这些打印语句，结果下一次问题出现时又得把它们加回来。日志 API 的设计就是为了克服这个问题。以下是该 API 的主要优点：

- 很容易抑制所有日志记录，或仅抑制低于某个级别的日志记录，也同样容易重新启用它们。
- 被抑制的日志开销非常低，因此在应用程序中保留日志记录代码只会带来极小的性能损失。
- 日志记录可以被定向到不同的处理器——例如显示在控制台、写入文件等。
- 日志记录器和处理器都可以过滤记录。过滤器可以使用过滤器实现者提供的任意条件丢弃无趣的日志条目。
- 日志记录可以按不同方式格式化——例如纯文本或 XML。
- 应用程序可以使用多个日志记录器，其名称具有层次结构，例如 `com.mycompany.myapp`，类似于包名。
- 日志配置由配置文件控制。

**注意：**

许多应用程序使用其他日志框架，例如 Log4J 2（https://logging.apache.org/log4j/2.x）和 Logback（https://logback.qos.ch），它们提供比标准 Java 日志框架更高的性能。这些框架的 API 略有不同。SLF4J（https://www.slf4j.org）和 Commons Logging（https://commons.apache.org/proper/commons-logging）等日志门面提供了统一的 API，因此你无需重写应用程序即可替换日志框架。更令人困惑的是，Log4J 2 也可以作为使用 SLF4J 的组件的门面。在本书中，我介绍标准 Java 日志框架。它对许多用途来说已经足够好，学习其 API 将为你理解替代方案做好准备。

**注意：**

从 Java 9 开始，Java 平台有一个单独的轻量级日志系统，它不依赖于 `java.logging` 模块（该模块包含标准 Java 日志框架）。该系统仅供 Java API 内部使用。如果存在 `java.logging` 模块，日志消息会自动转发给它。第三方日志框架可以提供适配器来接收平台日志消息。我不介绍平台日志记录，因为它不是供应用程序程序员使用的。

### 7.5.1 基本日志记录

对于简单日志记录，请使用全局日志记录器并调用其 `info` 方法：


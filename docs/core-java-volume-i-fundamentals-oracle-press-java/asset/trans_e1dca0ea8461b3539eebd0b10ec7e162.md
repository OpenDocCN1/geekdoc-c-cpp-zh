
空着，它不会变成被占用。如果文件包含错误，错误不会神奇地消失。因此，将*整个*任务包装在 try 块中是合理的。如果任何一个操作失败，你就可以放弃该任务。

```java
try
{
    for (i = 0; i < 100; i++)   {
        n = s.pop();
        out.writeInt(n);
    }
}
catch (IOException e)
{
        // problem writing to file
}
catch (EmptyStackException e)
{
        // stack was empty
}
```

这段代码看起来干净多了。它实现了异常处理的一项承诺：将正常处理与错误处理*分离*。

- **3. 充分利用异常层次结构。**

  不要只是抛出 `RuntimeException`。应找到合适的子类，或创建自己的子类。

  不要只是捕获 `Throwable`。这会让你的代码难以阅读和维护。

  尊重受检异常与非受检异常之间的区别。受检异常本质上是一种负担——不要为逻辑错误抛出它们。（例如，反射库在这方面就做错了。调用方常常需要捕获他们知道永远不会发生的异常。）

  不要犹豫，将异常转换为另一个更合适的异常。例如，当你在文件中解析一个整数时，捕获 `NumberFormatException` 并将其转换为 `IOException` 或 `MySubsystemException` 的子类。

- **4. 不要压制异常。**

  在 Java 中，人们有极大的诱惑去让异常闭嘴。如果你正在编写一个方法，它调用了一个可能一百年才抛出一次异常的方法，编译器会抱怨，因为你没有在你的方法的 throws 列表中声明该异常。你不想把它放进 throws 列表，因为那样编译器会抱怨所有调用你的方法的方法。于是你就让它闭嘴：

```java
public Image loadImage(String s)
{
    try
    {
        code that threatens to throw checked exceptions
    }
    catch (Exception e)       {} // so there
}
```

  现在你的代码会顺利编译。它会运行良好，除非发生异常。而那时，异常会被静默忽略。如果你认为异常确实重要，就应当付出一些努力正确处理它们。

- **5. 当你检测到错误时，“严厉的爱”比纵容更有效。**

  有些程序员在检测到错误时担心抛出异常。当方法以无效参数被调用时，返回一个占位值而不是抛出异常，也许会更好？例如，当栈为空时，`Stack.pop` 应该返回 `null`，还是抛出异常？我认为，在失败发生的位置抛出 `EmptyStackException`，比在之后某个时刻出现 `NullPointerException` 更好。

- **6. 传播异常并不是一件丢脸的事。**

  有些程序员觉得必须捕获所有抛出的异常。如果他们调用了一个会抛出异常的方法，例如 `FileInputStream` 构造函数或 `readLine` 方法，他们会本能地捕获可能生成的异常。在许多情况下，实际上更好的做法是*传播*异常，而不是捕获它：

```java
public void readStuff(String filename) throws IOException // not a sign of shame!
{
    var in = new FileInputStream(filename,
    StandardCharsets.UTF_8);
    . . .
}
```

  较高级别的方法通常更有能力告知用户错误，或放弃不成功的命令。

- **7. 使用标准方法报告空指针异常和越界异常。**

  Objects 类有以下方法

  - `requireNonNull`
  - `checkIndex`
  - `checkFromToIndex`
  - `checkFromIndexSize`

  用于这些常见检查。将它们用于参数验证：

```java
public void putData(int position, Object newValue)
{
    Objects.checkIndex(position, data.length);
    Objects.requireNonNull(newValue);
    . . .
}
```

  如果方法以无效索引或 null 参数被调用，就会抛出一个异常，并使用 Java 库惯用的消息。

- **8. 不要向最终用户显示堆栈跟踪。**

  如果你的程序遇到意外异常，显示堆栈跟踪似乎是个好主意，这样用户就可以报告它，使你更容易定位问题。然而，堆栈跟踪可能包含你不希望向潜在攻击者泄露的实现细节，例如你正在使用的库的版本。

  将堆栈跟踪记录到日志中，以便你可以检索它，但只向用户显示一条摘要消息。

> **注意：**
>
> 规则 5 和 6 可以概括为“尽早抛出，尽晚捕获”。

## 7.4 使用断言

断言是防御式编程中常用的一种惯用法。在接下来的几节中，你将学习如何有效地使用它们。

### 7.4.1 断言的概念

假设你确信某个特定性质成立，并且你的代码依赖该性质。例如，你可能正在计算

```java
double y = Math.sqrt(x);
```

你确定 x 不是负数。也许它是另一个不可能产生负数的计算的结果，或者它是某个方法的参数，而该方法要求调用方只提供正数输入。尽管如此，你还是想再次检查，而不是让令人困惑的“非数”浮点值悄悄进入你的计算。当然，你可以抛出异常：

```java
if (x < 0) throw new IllegalArgumentException("x < 0");
```

但这段代码会留在程序中，即使测试已经完成。如果你有很多这类检查，程序的运行速度可能会比应有的慢不少。

断言机制允许你在测试期间加入检查，并在生产代码中自动移除它们。

Java 语言有一个关键字 `assert`。它有两种形式：

```java
assert condition;
```

以及

```java
assert condition : expression;
```

两条语句都会对条件求值，如果条件为 false，则抛出一个 `AssertionError`。在第二条语句中，表达式会被传递给 `AssertionError` 对象的构造函数，并转换为一条消息字符串。

![](img/0e7b74ef51a065c077b42cd87b362288_597_0.png)

> **注意：**
>
> *表达式*部分的唯一目的是生成一条消息字符串。`AssertionError` 对象不会存储实际的表达式值，因此你之后无法查询它。正如 JDK 文档所述，这样做“会鼓励程序员尝试从断言失败中恢复，而这违背了该机制的目的。”

要断言 x 非负，你可以直接使用语句

```java
assert x >= 0;
```

或者，你可以将 x 的实际值传入 `AssertionError` 对象，以便稍后显示。

```java
assert x >= 0 : x;
```

### C++ 注意：

C 语言的 `assert` 宏会把断言条件转换为一个字符串，如果断言失败，就打印该字符串。例如，如果 `assert(x >= 0)` 失败，它会打印 `x >= 0` 是失败的条件。在 Java 中，条件不会自动成为错误报告的一部分。如果你想看到它，必须将它作为字符串传入 `AssertionError` 对象：`assert x >= 0 : "x >= 0"`。

### 7.4.2 断言的启用与禁用

默认情况下，断言是禁用的。通过使用 `-enableassertions` 或 `-ea` 选项运行程序来启用它们：

```text
java -enableassertions MyApp
```

请注意，你不必重新编译程序来启用或禁用断言。启用或禁用断言是*类加载器*的功能。当断言被禁用时，类加载器会剥离断言代码，这样它就不会拖慢执行。

你甚至可以在特定类或整个包中启用断言。例如：

```text
java -ea:MyClass -ea:com.mycompany.mylib MyApp
```

该命令为 `MyClass` 类以及 `com.mycompany.mylib` 包*及其子包*中的所有类启用断言。选项 `-ea...` 会为未命名包中的所有类启用断言。

你也可以使用 `-disableassertions` 或 `-da` 选项在特定类和包中禁用断言：

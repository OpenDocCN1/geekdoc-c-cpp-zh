
```java
try
{
    access the database
}
catch (SQLException original)
{
    var e = new ServletException("database error");
    e.initCause(original);
    throw e;
}
```

捕获异常后，可以获取原始异常：

```java
Throwable original = caughtException.getCause();
```

强烈推荐使用这种包装技术。它允许你在子系统中抛出高层异常，同时不丢失原始故障的细节。

![](img/0e7b74ef51a065c077b42cd87b362288_577_0.png)

**提示：**

如果某个方法不允许抛出受检异常，但其中发生了受检异常，那么包装技术也很有用。你可以捕获该受检异常并将其包装为运行时异常。

有时，你只想记录异常并在不做任何更改的情况下重新抛出它：

```java
try
{
    access the database
}
catch (Exception e)
{
    logger.log(level, message, e);
    throw e;
}
```

在 Java 7 之前，这种方法存在一个问题。假设该代码位于一个方法中

```java
public void updateRecord() throws SQLException
```

Java 编译器查看 `catch` 块内的 `throw` 语句，然后查看 `e` 的类型，并报错说此方法可能抛出任意 `Exception`，而不只是 `SQLException`。现在这一点已经得到改进。编译器现在会跟踪 `e` 源自 `try` 块这一事实。只要该块中唯一的受检异常是 `SQLException` 实例，并且 `e` 在 `catch` 块中未被更改，那么将所在方法声明为 `throws SQLException` 就是有效的。

### 7.2.4 finally 子句

当代码抛出异常时，它会停止处理方法中剩余的代码并退出该方法。如果该方法获取了一些只有该方法知道的本地资源，而且该资源必须被清理，那么这就是一个问题。一种解决方案是捕获所有异常，执行清理，然后重新抛出异常。但这种方案很繁琐，因为你需要在两个地方清理资源分配——正常代码中和异常代码中。`finally` 子句可以解决这个问题。

![](img/0e7b74ef51a065c077b42cd87b362288_578_0.png)

**注意：**

从 Java 7 开始，有一种更优雅的解决方案，即你将在下一节中看到的 `try-with-resources` 语句。我们详细讨论 `finally` 机制，因为它是概念基础。但在实践中，你使用 `try-with-resources` 语句的频率可能会高于 `finally` 子句。

无论是否捕获到异常，`finally` 子句中的代码都会执行。在下面的示例中，程序将在*所有情况下*关闭输入流：

```java
var in = new FileInputStream(...);
try
{
    // 1
    *code that might throw exceptions*
    // 2
}
catch (IOException e)
{
    // 3
    *show error message*
    // 4
}
finally
{
    // 5
    in.close();
}
// 6
```

让我们看看程序执行 `finally` 子句的三种可能情况。

- 1. 代码不抛出异常。在这种情况下，程序首先执行 `try` 块中的所有代码。然后，执行 `finally` 子句中的代码。之后，执行继续到 `finally` 子句之后的第一个语句。换句话说，执行经过点 1、2、5 和 6。
- 2. 代码抛出的异常在某个 `catch` 子句中被捕获——在我们的例子中，是 `IOException`。在这种情况下，程序会执行 `try` 块中的所有代码，直到抛出异常的位置。`try` 块中剩余的代码被跳过。然后，程序执行匹配的 `catch` 子句中的代码，接着执行 `finally` 子句中的代码。如果 `catch` 子句不抛出异常，程序会执行 `finally` 子句之后的第一行。在这种情况下，执行会经过点 1、3、4、5 和 6。如果 `catch` 子句抛出异常，那么该异常会被抛回给此方法的调用者，执行仅经过点 1、3 和 5。
- 3. 代码抛出的异常未在任何 `catch` 子句中被捕获。此时，程序会执行 `try` 块中的所有代码，直到抛出异常为止。`try` 块中剩余的代码被跳过。然后，执行 `finally` 子句中的代码，并且该异常会被抛回给此方法的调用者。执行仅经过点 1 和 5。

你可以使用不带 `catch` 子句的 `finally` 子句。例如，考虑以下 `try` 语句：

```java
InputStream in = ...;
try
{
    code that might throw exceptions
}
finally
{
    in.close();
}
```

无论 `try` 块中是否遇到异常，`finally` 子句中的 `in.close()` 语句都会执行。当然，如果遇到异常，它会被重新抛出，并且必须在另一个 `catch` 子句中捕获。

```java
InputStream in = ...;
try
{
    try
    {
        code that might throw exceptions
    }
    finally
    {
        in.close();
    }
}
catch (IOException e)
{
    show error message
}
```

内层 `try` 块只有一个职责：确保输入流被关闭。外层 `try` 块只有一个职责：确保错误被报告。这种解决方案不仅更清晰，而且更实用：`finally` 子句中的错误也会被报告。

**警告：**

当 `finally` 子句包含 `return` 语句时，它可能产生意外结果。假设你通过 `return` 语句从 `try` 块中间退出。在方法返回之前，会执行 `finally` 块。如果 `finally` 块也包含 `return` 语句，那么它会掩盖原始返回值。考虑以下示例：

```java
public static int parseInt(String s)
{
    try
    {
        return Integer.parseInt(s);
    }
    finally
    {
        return 0; // ERROR
    }
}
```

看起来，在调用 `parseInt("42")` 时，try 块的主体返回整数 42。然而，`finally` 子句会在方法实际返回之前执行，并导致该方法返回 0，从而忽略原始返回值。

更糟糕的是，考虑调用 `parseInt("zero")`。`Integer.parseInt` 方法会抛出 `NumberFormatException`。然后执行 `finally` 子句，而 return 语句吞掉了该异常！

finally 子句的主体用于清理资源。不要把改变控制流的语句（`return`、`throw`、`break`、`continue`）放在 finally 子句内。

### 7.2.5 try-with-resources 语句

从 Java 7 开始，有一种有用的快捷方式可用于以下代码模式

```
open a resource
try
{
    work with the resource
}
finally
{
    close the resource
}
```

前提是该资源属于实现了 `AutoCloseable` 接口的类。该接口只有一个方法

```java
void close() throws Exception
```

> **注意：**
> 还有一个 `Closeable` 接口。它是 `AutoCloseable` 的子接口，同样只有一个 `close` 方法。然而，该方法被声明为抛出 `IOException`。

在其最简单的形式中，try-with-resources 语句的形式如下

```java
try (Resource res = . . .)
{
    work with res
}
```

当 try 块退出时，`res.close()` 会被自动调用。下面是一个典型示例——读取文件中的所有单词：

```java
try (var in = new Scanner(Path.of("in.txt"),
    StandardCharsets.UTF_8))
{
    while (in.hasNext())
        System.out.println(in.next());
}
```

当该块正常退出时，或者发生异常时，`in.close()` 方法都会被调用，就像你使用了 `finally` 块一样。

你可以指定多个资源。例如，

```java
try (var in = new Scanner(Path.of("in.txt"),
    StandardCharsets.UTF_8);
        var out = new PrintWriter("out.txt",
            StandardCharsets.UTF_8))
{
    while (in.hasNext())
```

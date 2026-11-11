
- 4. **日志代理**是一个子类对象，它拦截方法调用，记录这些调用，然后调用超类。例如，如果你对 `Random` 类的 `nextDouble` 方法有疑问，可以创建一个代理对象，作为匿名子类的实例：

```java
var generator = new Random()
{
    public double nextDouble()
    {
        double result = super.nextDouble();
        Logger.getGlobal().info("nextDouble: " + result);
        return result;
    }
};
```

每当调用 nextDouble 方法时，都会生成一条日志消息。

要查明是谁调用了该方法，可以生成堆栈轨迹。

- 5. 你可以通过 `Throwable` 类中的 `printStackTrace` 方法从任何异常对象获取堆栈轨迹。下面的代码捕获任何异常，打印异常对象和堆栈轨迹，并重新抛出该异常，以便它能找到预期的处理器。

```java
try
{
    . . .
}
catch (Throwable t)
{
    t.printStackTrace();
    throw t;
}
```

你甚至不需要捕获异常就能生成堆栈轨迹。只需将语句

```java
Thread.dumpStack();
```

插入代码中的任何位置，即可获得堆栈轨迹。

- 6. 通常，堆栈轨迹会显示在 `System.err` 上。如果你想记录或显示堆栈轨迹，可以按如下方式将其捕获到字符串中：

```java
var out = new StringWriter();
new Throwable().printStackTrace(new PrintWriter(out));
String description = out.toString();
```

- 7. 将程序错误捕获到文件中通常很方便。然而，错误会发送到 `System.err`，而不是 `System.out`。因此，你不能简单地通过运行

```
java MyProgram > errors.txt
```

来捕获它们。相反，应这样捕获错误流：

```
java MyProgram 2> errors.txt
```

要将 System.err 和 System.out 捕获到同一个文件中，请使用

```
java MyProgram 1> errors.txt 2>&1
```

这在 bash 和 Windows shell 中有效。

- 8. 让未捕获异常的堆栈轨迹显示在 System.err 中并不理想。如果最终用户碰巧看到这些消息，会感到困惑；而当你需要它们进行诊断时，它们又不可用。更好的方法是将它们记录到文件中。你可以使用静态方法 `Thread.setDefaultUncaughtExceptionHandler` 更改未捕获异常的处理器：

```java
Thread.setDefaultUncaughtExceptionHandler(
    new Thread.UncaughtExceptionHandler()
    {
        public void uncaughtException(Thread t, Throwable e)
        {
            save information in log file
        }
    });
```

- 9. 要观察类加载过程，请使用 `-verbose` 标志启动 Java 虚拟机。你将得到类似下面的输出：

```
[0.012s][info][class,load] opened: /opt/jdk-11.0.1/lib/modules
[0.034s][info][class,load] java.lang.Object source: jrt:/java.base
[0.035s][info][class,load] java.io.Serializable source: jrt:/java.base
[0.035s][info][class,load] java.lang.Comparable source: jrt:/java.base
[0.035s][info][class,load] java.lang.CharSequence source: jrt:/java.base
[0.035s][info][class,load] java.lang.String source: jrt:/java.base
[0.035s][info][class,load] java.lang.constant.Constable source: jrt:/java.base
[0.036s][info][class,load] java.lang.reflect.GenericDeclaration source: jrt:/java.base
[0.036s][info][class,load] java.lang.reflect.Type source: jrt:/java.base
[0.036s][info][class,load] java.lang.Class source: jrt:/java.base
[0.036s][info][class,load] java.lang.Cloneable source: jrt:/java.base
[0.037s][info][class,load] java.lang.ClassLoader source: jrt:/java.base
[0.037s][info][class,load] java.lang.System source: jrt:/java.base
[0.037s][info][class,load] java.lang.Throwable source: jrt:/java.base
[0.037s][info][class,load] java.lang.Error source: jrt:/java.base
[0.037s][info][class,load] java.lang.Thread source: jrt:/java.base
[0.037s][info][class,load] java.lang.Exception source: jrt:/java.base
[0.037s][info][class,load] java.lang.RuntimeException source: jrt:/java.base
[0.038s][info][class,load] java.lang.SecurityManager source: jrt:/java.base
. . . . .
```

这有时有助于诊断类路径问题。

- 10. `-Xlint` 选项告诉编译器找出常见的代码问题。例如，如果你使用以下命令编译

```
javac -Xlint sourceFiles
```

编译器将报告 switch 语句中缺少 break 语句的问题。（“lint”一词最初描述一种用于定位 C 程序中潜在问题的工具，但现在一般用于任何标记可疑但不非法构造的工具。）

你将得到类似下面的消息

```
warning: [fallthrough] possible fall-through into case
```

方括号中的字符串标识警告类别。你可以启用和禁用每个类别。由于其中大多数都相当有用，最好全部保留，只禁用你不关心的类别，如下所示：

```
javac -Xlint:all,-fallthrough,-serial sourceFiles
```

你可以通过以下命令获取所有警告的列表

```
javac --help -X
```

- 11. Java 虚拟机支持对 Java 应用程序进行*监控和管理*，允许在虚拟机中安装代理，以跟踪内存消耗、线程使用、类加载等。这一特性对于大型且长时间运行的 Java 程序（例如应用服务器）尤为重要。作为这些能力的演示，JDK 附带了一个名为 jconsole 的图形工具，用于显示虚拟机的性能统计信息（参见图 7.3）。启动你的程序，然后启动 jconsole，并从正在运行的 Java 程序列表中选择你的程序。

控制台会提供关于正在运行的程序的大量信息。更多信息请参见 www.oracle.com/technetwork/articles/java/jconsole-1564139.html。

- 12. Java Mission Control 是一款专业级性能分析和诊断工具，随 Oracle JDK 提供，可免费用于开发目的。用于生产环境需要商业许可证。某个时候，开源版本将成为 OpenJDK 的一部分。与 jconsole 一样，Java Mission Control 可以附加到正在运行的虚拟机。它还可以分析 Java Flight Recorder 的输出，后者是一种从正在运行的 Java 应用程序收集诊断和性能分析数据的工具。有关这些工具的更多信息，请参见 https://docs.oracle.com/javacomponents/index.html。

![](img/127bccebb2cfadea3f02579edaad63c3_456_0.png)

**图 7.3** jconsole 程序

本章介绍了异常处理和日志记录。你还了解了用于测试和调试的有用提示。接下来的两章将介绍泛型程序设计及其最重要的应用：Java 集合框架。

## 第 8 章：泛型程序设计

### 本章内容

- 8.1 为什么要使用泛型程序设计？第 432 页
- 8.2 定义一个简单的泛型类，第 434 页
- 8.3 泛型方法，第 437 页
- 8.4 类型变量的限定，第 438 页
- 8.5 泛型代码和虚拟机，第 441 页
- 8.6 约束与局限性，第 447 页
- 8.7 泛型类型的继承规则，第 457 页
- 8.8 通配符类型，第 459 页
- 8.9 反射和泛型，第 467 页

泛型类和方法具有类型参数。这使它们能够精确描述当用特定类型实例化时应当发生什么。在泛型类出现之前，程序员必须使用 `Object` 来编写可处理多种类型的代码。这既繁琐又不安全。

随着泛型的引入，Java 拥有了一套富有表现力的类型系统，使设计者能够详细描述变量和方法的类型应当如何变化。在简单直接的情形下，你会发现实现泛型代码很简单。在更高级的情形下，对实现者来说，它可能变得相当复杂。目标是提供其他程序员可以毫无意外地使用的类和方法。

Java 5 中引入泛型，是 Java 编程语言自首次发布以来最重大的变化。一个主要设计目标是向后兼容早期版本。因此，Java 泛型存在一些令人不适的局限。你将在本章了解泛型程序设计的优势与挑战。

### 8.1 为什么要使用泛型程序设计？

*泛型程序设计*意味着编写可复用于许多不同类型对象的代码。例如，你不会想为收集 String 和 File 对象分别编写不同的类。而且你也不必这样做——单个 `ArrayList` 类可以收集任何类的对象。这就是泛型程序设计的一个例子。

实际上，Java 在拥有泛型类之前就已经有 ArrayList 类了。让我们考察泛型程序设计的机制是如何演变的，以及这对用户和实现者意味着什么。

#### 8.1.1 类型参数的优势

在 Java 添加泛型类之前，泛型程序设计是通过*继承*实现的。`ArrayList` 类只是维护一个 `Object` 引用的数组：

```java
public class ArrayList // before generic classes
{
    private Object[] elementData;

    public Object get(int i) { . . . }
    public void add(Object o) { . . . }
}
```

这种方法有两个问题。每当获取值时都必须进行强制类型转换：

```java
ArrayList files = new ArrayList();
. . .
String filename = (String) files.get(0);
```

此外，没有错误检查。你可以添加任何类的值：

```java
files.add(new File(". . ."));
```

这个调用可以编译并运行且没有错误。在其他地方，将 `get` 的结果强制转换为 String 会导致错误。

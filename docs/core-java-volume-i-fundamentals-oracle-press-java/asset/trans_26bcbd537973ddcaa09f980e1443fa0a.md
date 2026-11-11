

然后，为日志消息指定资源包键，而不是实际的消息字符串：

```
logger.info("readingFile");
```

你经常需要将参数包含到本地化消息中。消息可能包含占位符：{0}、{1}，等等。例如，要在日志消息中包含文件名，请像这样使用占位符：

```
Reading file {0}.
Achtung! Datei {0} wird eingelesen.
```

然后，要将值传递给占位符，请调用以下方法之一：

```
logger.log(Level.INFO, "readingFile", fileName);
logger.log(Level.INFO, "renamingFile", new Object[] { oldName, newName });
```

另外，从 Java 9 开始，你可以在 logrb 方法中指定资源包对象（而不是名称）：

```
logger.logrb(Level.INFO, bundle, "renamingFile", oldName, newName);
```

> **注意：**
>
> 这是唯一一种对消息参数使用可变参数的日志方法。

### 7.5.5 处理器

默认情况下，日志记录器会将记录发送到 `ConsoleHandler`，后者将它们打印到 `System.err` 流。具体来说，日志记录器将记录发送给父处理器，而最终的祖先（名为 `""`）有一个 `ConsoleHandler`。

与日志记录器一样，处理器也有日志级别。要使一条记录被记录，其日志级别必须*同时*高于日志记录器和处理器的阈值。日志管理器配置文件将默认控制台处理器的日志级别设置为：

```
java.util.logging.ConsoleHandler.level=INFO
```

要记录级别为 `FINE` 的记录，请在配置中同时更改默认日志记录器级别和处理器级别。或者，你也可以完全绕过配置文件，安装自己的处理器。

```
Logger logger = Logger.getLogger("com.mycompany.myapp");
logger.setLevel(Level.FINE);
logger.setUseParentHandlers(false);
var handler = new ConsoleHandler();
handler.setLevel(Level.FINE);
logger.addHandler(handler);
```

默认情况下，日志记录器会将记录同时发送到自己的处理器和父级的处理器。我们的日志记录器是原始日志记录器（名为 `""`）的子级，原始日志记录器会将所有级别为 `INFO` 及以上的记录发送到控制台。然而，我们不希望重复看到这些记录，因此我们将 `useParentHandlers` 属性设置为 false。

要将日志记录发送到其他位置，请添加另一个处理器。日志 API 为此提供了两个有用的处理器：`FileHandler` 和 `SocketHandler`。`SocketHandler` 将记录发送到指定的主机和端口。更令人感兴趣的是 `FileHandler`，它把记录收集到文件中。

你可以简单地将记录发送到默认的文件处理器，如下所示：

```
var handler = new FileHandler();
logger.addHandler(handler);
```

记录会被发送到用户主目录下的 java*n*.log 文件中，其中 *n* 是一个用于使文件唯一的编号。如果系统没有用户主目录的概念（例如在 Windows 95/98/ME 中），则文件会存储在默认位置，例如 c:\windows。默认情况下，记录以 XML 格式进行格式化。一条典型的日志记录具有如下形式：

```xml
<record>
  <date>2002-02-04T07:45:15</date>
  <millis>1012837515710</millis>
  <sequence>1</sequence>
  <logger>com.mycompany.myapp</logger>
  <level>INFO</level>
  <class>com.mycompany.mylib.Reader</class>
  <method>read</method>
  <thread>10</thread>
  <message>Reading file corejava.gif</message>
</record>
```

你可以通过在日志管理器配置中设置各种参数（参见表 7.1）或使用另一个构造函数（参见本节末尾的 API 说明）来修改文件处理器的默认行为。

你可能不想使用默认的日志文件名。因此，你应该使用其他模式，例如 %h/myapp.log。（模式变量的说明参见表 7.2。）

如果多个应用程序（或同一个应用程序的多个副本）使用同一个日志文件，你应该开启追加标志。或者，在文件名称模式中使用 %u，以便每个应用程序创建唯一的日志副本。

开启文件轮转也是一个好主意。日志文件按轮转顺序保存，例如 myapp.log.0、myapp.log.1、myapp.log.2，依此类推。每当文件超过大小限制时，最旧的日志会被删除，其他文件会被重命名，并创建一个世代编号为 0 的新文件。

**表 7.1** 文件处理器配置参数

| 配置属性 | 描述 | 默认值 |
|---|---|---|
| `java.util.logging.FileHandler.level` | 处理器级别 | `Level.ALL` |
| `java.util.logging.FileHandler.append` | 控制处理器是追加到现有文件，还是为每次程序运行打开一个新文件 | `false` |
| `java.util.logging.FileHandler.limit` | 在打开另一个文件之前，可写入一个文件的大致最大字节数（0 = 无限制） | 在 FileHandler 类中为 `0`（无限制），在默认日志管理器配置中为 `50000` |
| `java.util.logging.FileHandler.pattern` | 日志文件名的模式。模式变量参见表 7.2。 | `%h/java%u.log` |
| `java.util.logging.FileHandler.count` | 轮转序列中的日志数量 | `1`（不轮转） |
| `java.util.logging.FileHandler.filter` | 要使用的过滤器类 | 不过滤 |
| `java.util.logging.FileHandler.encoding` | 要使用的字符编码 | 平台编码 |
| `java.util.logging.FileHandler.formatter` | 记录格式化器 | `java.util.logging.XMLFormatter` |

**表 7.2** 日志文件模式变量

| 变量 | 描述 |
|---|---|
| `%h` | user.home 系统属性的值 |
| `%t` | 系统临时目录 |
| `%u` | 用于解决冲突的唯一编号 |
| `%g` | 轮转日志的世代编号（如果指定了轮转且模式中不包含 `%g`，则使用 `.%g` 后缀） |
| `%%` | % 字符 |

![](img/0e7b74ef51a065c077b42cd87b362288_617_0.png)

**提示：**

有些程序员使用日志来为技术支持人员提供帮助。如果程序在现场出现问题，用户可以把日志文件发送回来以供检查。在这种情况下，你应该开启追加标志，使用轮转日志，或者两者都采用。

你还可以通过扩展 `Handler` 或 `StreamHandler` 类来定义自己的处理器。我们在本节末尾的示例程序中定义了这样一个处理器。该处理器在窗口中显示记录（参见 *图 7.2*）。

![](img/0e7b74ef51a065c077b42cd87b362288_618_0.png)

**图 7.2** 在窗口中显示记录的日志处理器

该处理器扩展了 `StreamHandler` 类，并安装了一个流，其 write 方法将流输出显示在文本区域中。

```java
class WindowHandler extends StreamHandler
{
    public WindowHandler()
    {
        . . .
        var output = new JTextArea();
        setOutputStream(new
            OutputStream()
            {
                public void write(int b) { } // not called
                public void write(byte[] b, int off, int len)
                {
                    output.append(new String(b, off, len));
                }
            });
    }
    . . .
}
```

这种方法只有一个问题——处理器会缓冲记录，并且只在缓冲区满时才将它们写入流。因此，我们重写 publish 方法，以便在每条记录之后刷新缓冲区：

```
class WindowHandler extends StreamHandler
{
    . . .
    public void publish(LogRecord record)
    {
        super.publish(record);
        flush();
    }
}
```

如果你想编写更特别的流处理器，可以扩展 Handler 类，并定义 publish、flush 和 close 方法。

### 7.5.6 过滤器

默认情况下，记录会根据其日志级别进行过滤。每个日志记录器和处理器都可以有一个可选的过滤器来执行额外的过滤。要定义过滤器，请实现 Filter 接口并定义该方法：

```
boolean isLoggable(LogRecord record)
```

使用你想要的任何标准分析日志记录，并对于应该包含在日志中的记录返回 true。例如，某个过滤器可能只对 entering 和 exiting 方法生成的消息感兴趣。那么该过滤器应调用 record.getMessage()，并检查它是否以 ENTRY 或 RETURN 开头。

要将过滤器安装到日志记录器或处理器中，只需调用 setFilter 方法。请注意，同一时间最多只能有一个过滤器。

### 7.5.7 格式化器


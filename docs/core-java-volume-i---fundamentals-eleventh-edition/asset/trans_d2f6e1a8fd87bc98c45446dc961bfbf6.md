
### 7.5.4 本地化

你可能希望本地化日志消息，以便国际用户能够阅读。应用程序的国际化是第II卷第7章的主题。简而言之，本地化日志消息时需要牢记以下几点。

本地化应用程序在*资源包*中包含特定于区域设置的信息。资源包由针对各种区域设置（例如美国或德国）的一组映射组成。例如，资源包可以将字符串 `readingFile` 映射为英语字符串 `Reading file` 或德语字符串 `Achtung! Datei wird eingelesen`。

一个程序可能包含多个资源包——例如，一个用于菜单，另一个用于日志消息。每个资源包都有一个名称（例如 `com.mycompany.logmessages`）。要向资源包添加映射，请为每个区域设置提供一个文件。英语消息映射位于文件 `com/mycompany/logmessages_en.properties` 中，德语消息映射位于文件 `com/mycompany/logmessages_de.properties` 中。（en 和 de 是语言代码。）将这些文件与应用程序的类文件放在一起，以便 ResourceBundle 类自动定位它们。这些文件是纯文本文件，由如下条目组成：

```
readingFile=Achtung! Datei wird eingelesen
renamingFile=Datei wird umbenannt
...
```

请求记录器时，可以指定一个资源包：

```java
Logger logger = Logger.getLogger("loggerName", "com.mycompany.logmessages");
```

然后为日志消息指定资源包键，而不是实际的消息字符串：

```java
logger.info("readingFile");
```

你经常需要将参数包含到本地化消息中。一条消息可能包含占位符：{0}、{1} 等。例如，要在日志消息中包含文件名，请像这样使用占位符：

```
Reading file {0}.
Achtung! Datei {0} wird eingelesen.
```

然后，要将值传入占位符，请调用以下方法之一：

```java
logger.log(Level.INFO, "readingFile", fileName);
logger.log(Level.INFO, "renamingFile", new Object[] { oldName, newName });
```

或者，从 Java 9 开始，可以在 logrb 方法中指定资源包对象（而不是名称）：

```java
logger.logrb(Level.INFO, bundle, "renamingFile", oldName, newName);
```

> **注意：** 这是唯一一种对消息参数使用可变参数的日志记录方法。

### 7.5.5 处理器

默认情况下，记录器将记录发送到 ConsoleHandler，后者将其打印到 System.err 流。具体来说，记录器将记录发送给父处理器，而最终祖先（名称为 ""）有一个 ConsoleHandler。

与记录器一样，处理器也有日志级别。要记录一条记录，其日志级别必须高于记录器和处理器的阈值。日志管理器配置文件将默认控制台处理器的日志级别设置为

```
java.util.logging.ConsoleHandler.level=INFO
```

要记录级别为 FINE 的记录，请在配置中同时更改默认记录器级别和处理器级别。或者，你可以完全绕过配置文件并安装自己的处理器。

```java
Logger logger = Logger.getLogger("com.mycompany.myapp");
logger.setLevel(Level.FINE);
logger.setUseParentHandlers(false);
var handler = new ConsoleHandler();
handler.setLevel(Level.FINE);
logger.addHandler(handler);
```

默认情况下，记录器将记录同时发送到自己的处理器和父处理器。我们的记录器是原始记录器（名称为 ""）的子记录器，后者将所有级别为 INFO 及以上的记录发送到控制台。然而，我们不希望两次看到这些记录，因此将 useParentHandlers 属性设置为 false。

要将日志记录发送到其他地方，请添加另一个处理器。日志 API 为此提供了两个有用的处理器：FileHandler 和 SocketHandler。SocketHandler 将记录发送到指定的主机和端口。更值得关注的是将记录收集到文件中的 FileHandler。

你可以简单地将记录发送到默认文件处理器，如下所示：

```java
var handler = new FileHandler();
logger.addHandler(handler);
```

记录被发送到用户主目录中的文件 java%u.log，其中 u 是一个使文件唯一的数字。如果系统没有用户主目录的概念（例如在 Windows 95/98/ME 中），则文件存储在默认位置，例如 C:\Windows。默认情况下，记录以 XML 格式化。典型的日志记录形式如下

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

你可以通过在日志管理器配置中设置各种参数（见表 7.1）或使用另一个构造器（见本节末尾的 API 说明）来修改文件处理器的默认行为。

**表 7.1 文件处理器配置参数**

| 配置属性 | 描述 | 默认值 |
|---|---|---|
| `java.util.logging.FileHandler.level` | 处理器级别 | `Level.ALL` |
| `java.util.logging.FileHandler.append` | 控制处理器应追加到现有文件，还是为每次程序运行打开新文件 | `false` |
| `java.util.logging.FileHandler.limit` | 在打开另一个文件之前要写入文件的近似最大字节数（`0` = 无限制） | `0 (no limit) in the FileHandler class, 5000 in the default log manager configuration` |
| `java.util.logging.FileHandler.pattern` | 日志文件名的模式。有关模式变量，请参见表 7.2。 | `%h/java%u.log` |
| `java.util.logging.FileHandler.count` | 轮换序列中的日志数量 | `1 (no rotation)` |
| `java.util.logging.FileHandler.filter` | 要使用的过滤器类 | `No filtering` |
| `java.util.logging.FileHandler.encoding` | 要使用的字符编码 | `The platform encoding` |
| `java.util.logging.FileHandler.formatter` | 记录格式化器 | `java.util.logging.XMLFormatter` |

你可能不希望使用默认日志文件名。因此，应使用另一种模式，例如 `%h/myapp.log`。（有关模式变量的说明，请参见表 7.2。）

如果多个应用程序（或同一应用程序的多个副本）使用同一个日志文件，则应打开追加标志。或者，在文件名模式中使用 `%u`，以便每个应用程序创建日志的唯一副本。

**表 7.2** 日志文件模式变量

| 变量 | 描述 |
|---|---|
| `%h` | `user.home` 系统属性的值 |
| `%t` | 系统临时目录 |
| `%u` | 用于解决冲突的唯一数字 |
| `%g` | 轮换日志的代数编号（如果指定了轮换且模式中不包含 `%g`，则使用 `.%g` 后缀） |
| `%%` | `%` 字符 |

打开文件轮换也是个好主意。日志文件按轮换序列保存，例如 myapp.log.0、myapp.log.1、myapp.log.2 等。每当文件超过大小限制时，最旧的日志会被删除，其他文件会被重命名，并创建一个代数编号为 0 的新文件。

> **提示：** 许多程序员将日志记录用作技术支持人员的辅助手段。如果程序在现场出现异常行为，用户可以回传日志文件以供检查。在这种情况下，应打开追加标志、使用轮换日志，或两者兼用。

你还可以通过扩展 `Handler` 或 `StreamHandler` 类来定义自己的处理器。我们在本节末尾的示例程序中定义了这样一个处理器。该处理器在窗口中显示记录（见图 7.2）。

![](img/127bccebb2cfadea3f02579edaad63c3_439_0.png)

![](img/127bccebb2cfadea3f02579edaad63c3_439_1.png)

**图 7.2** 在窗口中显示记录的日志处理器

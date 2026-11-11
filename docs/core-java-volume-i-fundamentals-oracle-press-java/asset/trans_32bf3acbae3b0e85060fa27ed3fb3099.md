
- `void entering(String className, String methodName)`
- `void entering(String className, String methodName, Object param)`
- `void entering(String className, String methodName, Object[] param)`
- `void exiting(String className, String methodName)`
- `void exiting(String className, String methodName, Object result)`

记录一条描述使用给定参数或返回值进入或退出方法的日志记录。

- `void throwing(String className, String methodName, Throwable t)`

记录一条描述抛出给定异常对象的日志记录。

- `void log(Level level, String message)`
- `void log(Level level, String message, Object obj)`
- `void log(Level level, String message, Object[] objs)`
- `void log(Level level, String message, Throwable t)`

记录一条具有给定级别和消息的日志记录，可选地包含对象或可抛出对象。要包含对象，消息必须包含格式占位符（{0}、{1} 等）。

- `void logp(Level level, String className, String methodName, String message)`
- `void logp(Level level, String className, String methodName, String message, Object obj)`
- `void logp(Level level, String className, String methodName, String message, Object[] objs)`
- `void logp(Level level, String className, String methodName, String message, Throwable t)`

记录一条具有给定级别、精确调用方信息和消息的日志记录，可选地包含对象或可抛出对象。

- `void logrb(Level level, String className, String methodName, ResourceBundle bundle, String message, Object... params)`
- `void logrb(Level level, String className, String methodName, ResourceBundle bundle, String message, Throwable thrown)`

记录一条具有给定级别、精确调用方信息、资源包和消息的日志记录，后跟对象或可抛出对象。

- `Level getLevel()`
- `void setLevel(Level l)`

获取并设置此日志记录器的级别。

- `Logger getParent()`
- `void setParent(Logger l)`

获取并设置此日志记录器的父日志记录器。

- `Handler[] getHandlers()`

获取此日志记录器的所有处理器。

- `void addHandler(Handler h)`
- `void removeHandler(Handler h)`

为此日志记录器添加或移除处理器。

- `boolean getUseParentHandlers()`
- `void setUseParentHandlers(boolean b)`

获取并设置“使用父处理器”属性。如果此属性为 true，则日志记录器会将所有已记录的日志记录转发给其父级的处理器。

- `Filter getFilter()`
- `void setFilter(Filter f)`

获取并设置此日志记录器的过滤器。

- `abstract void publish(LogRecord record)`
  将记录发送到预期目标。
- `abstract void flush()`
  刷新任何缓冲数据。
- `abstract void close()`
  刷新任何缓冲数据并释放所有关联资源。
- `Filter getFilter()`
- `void setFilter(Filter f)`
  获取并设置此处理器的过滤器。
- `Formatter getFormatter()`
- `void setFormatter(Formatter f)`
  获取并设置此处理器的格式化器。
- `Level getLevel()`
- `void setLevel(Level l)`
  获取并设置此处理器的级别。

### java.util.logging.ConsoleHandler 1.4

- `ConsoleHandler()`
  构造一个新的控制台处理器。

### java.util.logging.FileHandler 1.4

- `FileHandler(String pattern)`
- `FileHandler(String pattern, boolean append)`
- `FileHandler(String pattern, int limit, int count)`
- `FileHandler(String pattern, int limit, int count, boolean append)`
- `FileHandler(String pattern, long limit, int count, boolean append)`

构造一个文件处理器。模式格式见表 7.2。`limit` 是打开新日志文件之前的近似最大字节数。`count` 是轮换序列中的文件数。如果 `append` 为 true，则记录应追加到现有日志文件。

### `java.util.logging.LogRecord` 1.4

- `Level getLevel()`
  获取此记录的日志级别。
- `String getLoggerName()`
  获取正在记录此记录的日志记录器的名称。
- `ResourceBundle getResourceBundle()`
- `String getResourceBundleName()`
  获取用于本地化消息的资源包或其名称；如果未提供，则返回 null。
- `String getMessage()`
  获取本地化或格式化之前的“原始”消息。
- `Object[] getParameters()`
  获取参数对象；如果未提供，则返回 null。
- `Throwable getThrown()`
  获取抛出的对象；如果未提供，则返回 null。
- `String getSourceClassName()`
- `String getSourceMethodName()`

获取记录此日志的代码位置。此信息可能由日志记录代码提供，也可能从运行时堆栈自动推断。如果日志记录代码提供了错误的值，或者运行代码经过优化而无法推断确切位置，则此信息可能不准确。

- `long getMillis()`

  获取创建时间，以自 1970 年以来的毫秒数表示。

- `Instant getInstant()`

  以 `java.time.Instant` 形式获取创建时间（见第二卷[第 6 章](#)）。

- `long getSequenceNumber()`

  获取此记录的唯一序列号。

- `long getLongThreadID()`

  获取创建此记录的线程的唯一 ID。这些 ID 由 `LogRecord` 类分配，与其他线程 ID 没有关系。（`getThreadID` 方法返回 `int` 类型的 ID。它现在已被弃用，因为长时间运行的程序可能生成超过 `Integer.MAX_VALUE` 条日志记录。）

### `java.util.logging.LogManager` 1.4

- `static LogManager getLogManager()`

  获取全局 LogManager 实例。

- `void readConfiguration()`
- `void readConfiguration(InputStream in)`

  从系统属性 `java.util.logging.config.file` 指定的文件或给定输入流中读取日志配置。

- `void updateConfiguration(InputStream in, Function<String,BiFunction<String,String,String>> mapper)`
- `void updateConfiguration(Function<String,BiFunction<String,String,String>> mapper)`

  将日志配置与系统属性 `java.util.logging.config.file` 指定的文件或给定输入流合并。关于 mapper 参数的说明，见第 424 页的[第 7.5.3 节“更改日志管理器配置”](#)。

### java.util.logging.Filter 1.4

- `boolean isLoggable(LogRecord record)`

  如果应记录给定的日志记录，则返回 true。

### java.util.logging.Formatter 1.4

- `abstract String format(LogRecord record)`

  返回格式化给定日志记录后得到的字符串。

- `String getHead(Handler h)`
- `String getTail(Handler h)`

  返回应出现在包含日志记录的文档开头和结尾的字符串。Formatter 超类将这些方法定义为返回空字符串；如有必要，请覆盖它们。

- `String formatMessage(LogRecord record)`

  返回日志记录中已本地化并格式化的消息部分。

## 7.6 调试技巧

假设你编写了程序，并通过捕获和正确处理所有异常使其无懈可击。然后运行它，却发现它不能正常工作。现在该怎么办？（如果你从未遇到这个问题，可以跳过本章的剩余部分。）

当然，最好有一个方便而强大的调试器。Eclipse、IntelliJ 和 NetBeans 等专业开发环境都提供调试器。在本节中，我会提供一些技巧，在你启动调试器之前可能值得一试。

- 1. 可以使用如下代码打印或记录任何变量的值：

  ```java
  System.out.println("x=" + x);
  ```

  或者

  ```java
  Logger.getGlobal().info("x=" + x);
  ```

  如果 x 是数字，则将其转换为等效字符串。如果 x 是对象，Java 会调用其 toString 方法。要获取隐式参数对象的状态，请打印 this 对象的状态。

  ```java
  Logger.getGlobal().info("this=" + this);
  ```

  Java 库中的大多数类都非常认真地重写 toString 方法，以提供有关该类的有用信息。这对调试确实大有帮助。你也应该在自己的类中做出同样的努力。

- 2. 一个看似鲜为人知但非常有用的技巧是在每个类中放置一个单独的 main 方法。在其中，你可以放置一个单元测试桩，以便单独测试该类。

  ```java
  public class MyClass
  {
     methods and fields
     . . .
     public static void main(String[] args)
     {
        test code
  }
  ```




### 清单 8.1（续）

```java
if (descriptor.getName().equals(eventName)) return descriptor;
return null;
}
}
```

### 清单 8.2 `buttons1/ButtonFrame.java`

```java
package buttons1;

import javax.swing.*;

/**
 * A frame with a button panel.
 * @version 1.00 2007-11-02
 * @author Cay Horstmann
 */
public class ButtonFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 200;

   private JPanel panel;
   private JButton yellowButton;
   private JButton blueButton;
   private JButton redButton;

   public ButtonFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      panel = new JPanel();
      panel.setName("panel");
      add(panel);

      yellowButton = new JButton("Yellow");
      yellowButton.setName("yellowButton");
      blueButton = new JButton("Blue");
      blueButton.setName("blueButton");
      redButton = new JButton("Red");
      redButton.setName("redButton");

      panel.add(yellowButton);
      panel.add(blueButton);
      panel.add(redButton);
   }
}
```

## 8.2 编译器 API

在前面的章节中，你了解了如何与脚本语言中的代码交互。现在我们转向另一种场景：编译 Java 代码的 Java 程序。有不少工具需要调用 Java 编译器，例如：

- 开发环境
- Java 教学和辅导程序
- 构建和测试自动化工具
- 处理 Java 代码片段的模板工具，例如 JavaServer Pages（JSP）

过去，应用程序通过调用 `jdk/lib/tools.jar` 库中未公开的类来调用 Java 编译器。如今，用于编译的公共 API 已成为 Java 平台的一部分，不再需要使用 `tools.jar`。本节将介绍编译器 API。

### 8.2.1 轻松编译

调用编译器非常简单。下面是一个示例调用：

```java
JavaCompiler compiler = ToolProvider.getSystemJavaCompiler();
OutputStream outStream = ...;
OutputStream errStream = ...;
int result = compiler.run(null, outStream, errStream, "-sourcepath", "src", "Test.java");
```

结果值为 0 表示编译成功。

编译器会将输出和错误消息发送到提供的流中。你可以将这些参数设置为 `null`，此时将使用 `System.out` 和 `System.err`。`run` 方法的第一个参数是输入流。由于编译器不接受控制台输入，因此你可以始终将其保留为 `null`。（`run` 方法继承自通用的 `Tool` 接口，该接口允许工具读取输入。）

`run` 方法的其余参数就是你在命令行中调用 `javac` 时会传给它的参数。这些参数可以是选项或文件名。

### 8.2.2 使用编译任务

使用 `CompilationTask` 对象，你可以对编译过程拥有更多控制权。具体来说，你可以

- 控制程序代码的来源——例如，在字符串构建器中提供代码，而不是在文件中提供
- 控制类文件的位置——例如，将它们存储在数据库中
- 在编译期间出现错误和警告消息时监听它们
- 在后台运行编译器

源文件和类文件的位置由 `JavaFileManager` 控制。它负责为源文件和类文件确定 `JavaFileObject` 实例。一个 `JavaFileObject` 可以对应磁盘文件，也可以提供另一种读写其内容的机制。

要监听错误消息，请安装一个 `DiagnosticListener`。每当编译器报告警告或错误消息时，该监听器都会收到一个 `Diagnostic` 对象。`DiagnosticCollector` 类实现了这个接口。它只是收集所有诊断信息，以便你在编译完成后遍历它们。

`Diagnostic` 对象包含有关问题位置的信息（包括文件名、行号和列号），以及人类可读的描述。

要获得 `CompilationTask` 对象，请调用 `JavaCompiler` 类的 `getTask` 方法。你需要指定：

- 一个 `Writer`，用于接收任何未作为 `Diagnostic` 报告的编译器输出；若为 `null`，则使用 `System.err`
- 一个 `JavaFileManager`；若为 `null`，则使用编译器的标准文件管理器
- 一个 `DiagnosticListener`
- 选项字符串；若没有选项，则为 `null`
- 用于注解处理的类名；若未指定任何类名，则为 `null`（我们将在本章后面讨论注解处理）
- 源文件的 `JavaFileObject` 实例

最后三个参数需要以 `Iterable` 对象提供。例如，一组选项可以指定为

```java
Iterable<String> options = Arrays.asList("-g", "-d", "classes");
```

或者，你也可以使用任何集合类。

如果你希望编译器从磁盘读取源文件，可以让 `StandardJavaFileManager` 将文件名字符串或 `File` 对象转换为 `JavaFileObject` 实例。例如，

```java
StandardJavaFileManager fileManager = compiler.getStandardFileManager(null, null, null);
Iterable<JavaFileObject> fileObjects = fileManager.getJavaFileObjectsFromStrings(fileNames);
```

然而，如果你希望编译器从磁盘文件以外的位置读取源代码，就需要提供自己的 `JavaFileObject` 子类。清单 8.3 展示了一个源文件对象的代码，其数据包含在 StringBuilder 中。该类扩展了 SimpleJavaFileObject 便利类，并重写 getCharContent 方法以返回字符串构建器的内容。我们将在示例程序中使用这个类，在程序中动态生成一个 Java 类的代码，然后编译它。

CompilationTask 接口扩展了 Callable<Boolean> 接口。你可以将它传给 Executor，以便在另一个线程中执行，也可以直接调用 call 方法。返回 Boolean.FALSE 表示失败。

```java
Callable<Boolean> task = compiler.getTask(null, fileManager, diagnostics,
      options, null, fileObjects);
if (!task.call())
   System.out.println("Compilation failed");
```

如果你只是希望编译器在磁盘上生成类文件，则无需自定义 JavaFileManager。不过，我们的示例应用程序会在字节数组中生成类文件，随后使用特殊的类加载器从内存中读取它们。清单 8.4 定义了一个实现 JavaFileObject 接口的类。它的 openOutputStream 方法返回 ByteArrayOutputStream，编译器会将字节码存入其中。

要让编译器的文件管理器使用这些文件对象，结果有点棘手。该库没有提供实现 StandardJavaFileManager 接口的类。相反，你需要子类化 ForwardingJavaFileManager 类，该类将所有调用委托给给定的文件管理器。在我们的场景中，我们只想修改 getJavaFileForOutput 方法。我们通过以下概要实现这一点：

```java
JavaFileManager fileManager = compiler.getStandardFileManager(diagnostics, null, null);
fileManager = new ForwardingJavaFileManager<JavaFileManager>(fileManager)
   {
      public JavaFileObject getJavaFileForOutput(Location location, final String className,
            Kind kind, FileObject sibling) throws IOException
      {
         return custom file object
      };
   };
```

总之，如果你只想以通常方式调用编译器并读写磁盘文件，就调用 JavaCompiler 任务的 run 方法。你可以捕获输出和错误消息，但需要自行解析它们。

如果你希望对文件处理或错误报告有更多控制，请改用 CompilationTask 接口。它的 API 相当复杂，但你可以控制编译过程的各个方面。

### 清单 8.3 `compiler/StringBuilderJavaSource.java`

```java
package compiler;

import java.net.*;
import javax.tools.*;

/**
 * A Java source that holds the code in a string builder.
 * @version 1.00 2007-11-02
 * @author Cay Horstmann
 */
public class StringBuilderJavaSource extends SimpleJavaFileObject
{
    private StringBuilder code;

    /**
     * Constructs a new StringBuilderJavaSource.
     * @param name the name of the source file represented by this file object
     */
    public StringBuilderJavaSource(String name)
    {
        super(URI.create("string:///" + name.replace('.', '/') + Kind.SOURCE.extension),
              Kind.SOURCE);
        code = new StringBuilder();
    }

    public CharSequence getCharContent(boolean ignoreEncodingErrors)
    {
        return code;
    }

    public void append(String str)
    {
        code.append(str);
        code.append("\n");
    }
}
```

### 清单 8.4 `compiler/ByteArrayJavaClass.java`

```java
package compiler;

import java.io.*;
import java.net.*;
import javax.tools.*;
```


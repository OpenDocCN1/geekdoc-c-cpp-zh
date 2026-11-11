
```java
var loader = new ByteArrayClassLoader(classFileObjects);
var frame = (JFrame) loader.loadClass("x.Frame").getConstructor().newInstance();
frame.setVisible(true);
```

当您单击按钮时，背景会像往常一样改变颜色。要查看操作是动态编译的，请更改 action.properties 中的一行，例如：

```java
yellowButton.setBackground(java.awt.Color.YELLOW); yellowButton.setEnabled(false);
```

再次运行程序。现在黄色按钮在单击后会被禁用。另外，请查看代码目录。您不会在 x 包中找到这些类的任何源文件或类文件。此示例演示了如何将动态编译与内存中的源文件和类文件结合使用。

## 清单 8.3 `compiler/CompilerTest.java`

```java
package compiler;

import java.awt.*;
import java.io.*;
import java.nio.file.*;
import java.util.*;
import java.util.List;

import javax.swing.*;
import javax.tools.*;
import javax.tools.JavaFileObject.*;

/**
 * @version 1.10 2018-05-01
 * @author Cay Horstmann
 */
public class CompilerTest
{
   public static void main(final String[] args)
         throws IOException, ReflectiveOperationException
   {
      JavaCompiler compiler = ToolProvider.getSystemJavaCompiler();

      var classFileObjects = new ArrayList<ByteArrayClass>();
      var diagnostics = new DiagnosticCollector<JavaFileObject>();

      JavaFileManager fileManager = compiler.getStandardFileManager(diagnostics, null, null);
      fileManager = new ForwardingJavaFileManager<JavaFileManager>(fileManager)
      {
         public JavaFileObject getJavaFileForOutput(Location location,
               String className, Kind kind, FileObject sibling) throws IOException
         {
```

## 清单 8.3（续）

```java
static JavaFileObject buildSource(String superclassName)
   throws IOException, ClassNotFoundException
{
   var builder = new StringBuilder();
   builder.append("package x;\n\n");
   builder.append("public class Frame extends " + superclassName + " {\n");
   builder.append("  protected void addEventHandlers() {\n");
   var props = new Properties();
   props.load(Files.newInputStream(Paths.get(
      superclassName.replace(".", "/")).getParent().resolve("action.properties")));
   for (Map.Entry<Object, Object> e : props.entrySet())
   {
      var beanName = (String) e.getKey();
      var eventCode = (String) e.getValue();
      builder.append("  " + beanName + ".addActionListener(event -> {\n");
      builder.append(eventCode);
      builder.append("\n });\n");
   }
   builder.append("} }\n");
   return new StringSource("x.Frame", builder.toString());
}
}
```

## 清单 8.4 `buttons2/ButtonFrame.java`

```java
package buttons2;

import javax.swing.*;

/**
 * A frame with a button panel.
 * @version 1.00 2007-11-02
 * @author Cay Horstmann
 */
public abstract class ButtonFrame extends JFrame
{
   public static final int DEFAULT_WIDTH = 300;
   public static final int DEFAULT_HEIGHT = 200;

   protected JPanel panel;
   protected JButton yellowButton;
   protected JButton blueButton;
   protected JButton redButton;

   public ButtonFrame()
   {
       setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

       panel = new JPanel();
       add(panel);

       yellowButton = new JButton("Yellow");
       blueButton = new JButton("Blue");
       redButton = new JButton("Red");

       panel.add(yellowButton);
       panel.add(blueButton);
       panel.add(redButton);

       addEventHandlers();
   }

   protected abstract void addEventHandlers();
}
```

## 清单 8.5 `buttons2/action.properties`

```properties
yellowButton=panel.setBackground(java.awt.Color.YELLOW);
blueButton=panel.setBackground(java.awt.Color.BLUE);
```

## javax.tools.Tool 6

- `int run(InputStream in, OutputStream out, OutputStream err, String... arguments)`  
  使用给定的输入、输出和错误流以及给定的参数运行该工具。成功时返回 0，失败时返回非零值。

## javax.tools.JavaCompiler 6

- `StandardJavaFileManager getStandardFileManager(DiagnosticListener<? super JavaFileObject> diagnosticListener, Locale locale, Charset charset)`  
  获取此编译器的标准文件管理器。您可以按默认错误报告、区域设置和字符集传入 null。
- `JavaCompiler.CompilationTask getTask(Writer out, JavaFileManager fileManager, DiagnosticListener<? super JavaFileObject> diagnosticListener, Iterable<String> options, Iterable<String> classesForAnnotationProcessing, Iterable<? extends JavaFileObject> sourceFiles)`  
  获取一个编译任务，调用该任务时会编译给定的源文件。有关详细信息，请参阅前文的讨论。

| 类 | 版本 | 成员 | 描述 |
|---|---|---|---|
| `javax.tools.StandardJavaFileManager` | 6 | • `Iterable<? extends JavaFileObject> getJavaFileObjectsFromStrings(Iterable<String> filenames)`<br>• `Iterable<? extends JavaFileObject> getJavaFileObjectsFromFiles(Iterable<? extends File> files)` | 将一系列文件名或文件转换为一系列 JavaFileObject 实例。 |

| 类 | 版本 | 成员 | 描述 |
|---|---|---|---|
| `javax.tools.JavaCompiler.CompilationTask` | 6 | • `Boolean call()` | 执行编译任务。 |

| 类 | 版本 | 成员 | 描述 |
|---|---|---|---|
| `javax.tools.DiagnosticCollector<S>` | 6 | • `DiagnosticCollector()` | 构造一个空的收集器。 |
| `javax.tools.DiagnosticCollector<S>` | 6 | • `List<Diagnostic<? extends S>> getDiagnostics()` | 获取收集到的诊断信息。 |

| 类 | 版本 | 成员 | 描述 |
|---|---|---|---|
| `javax.tools.Diagnostic<S>` | 6 | • `S getSource()` | 获取与该诊断关联的源对象。 |
| `javax.tools.Diagnostic<S>` | 6 | • `Diagnostic.Kind getKind()` | 获取此诊断的类型——ERROR、WARNING、MANDATORY_WARNING、NOTE 或 OTHER。 |
| `javax.tools.Diagnostic<S>` | 6 | • `String getMessage(Locale locale)` | 获取描述此诊断所引发问题的消息。传入 null 以使用默认区域设置。 |
| `javax.tools.Diagnostic<S>` | 6 | • `long getLineNumber()`<br>• `long getColumnNumber()` | 获取此诊断所引发问题的位置。 |

| 类 | 成员 | 描述 |
|---|---|---|
| `javax.tools.SimpleJavaFileObject` | • `CharSequence getCharContent(boolean ignoreEncodingErrors)` | 为表示源文件并生成源代码的文件对象重写此方法。 |
| `javax.tools.SimpleJavaFileObject` | • `OutputStream openOutputStream()` | 为表示类文件并生成可写入字节码的流的文件对象重写此方法。 |

| 类 | 成员 | 描述 |
|---|---|---|
| `javax.tools.ForwardingJavaFileManager<M extends JavaFileManager>` | • `protected ForwardingJavaFileManager(M fileManager)` | 构造一个将所有调用委托给给定文件管理器的 JavaFileManager。 |
| `javax.tools.ForwardingJavaFileManager<M extends JavaFileManager>` | • `FileObject getFileForOutput(JavaFileManager.Location location, String className, JavaFileObject.Kind kind, FileObject sibling)` | 如果您想替换文件对象来写入类文件，请拦截此调用；kind 是 SOURCE、CLASS、HTML 或 OTHER。 |

## 8.3 使用注解

注解是插入到源代码中的标签，以便某些工具可以处理它们。这些工具可以在源代码级别操作，也可以处理编译器已将注解放入其中的类文件。

注解不会改变程序的编译方式。无论有没有注解，Java 编译器都会生成相同的虚拟机指令。

要从注解中获益，您需要选择一个处理工具。使用您的处理工具能够理解的注解，然后将处理工具应用到您的代码中。

注解的用途非常广泛，这种通用性一开始可能会令人困惑。以下是注解的一些用途：

- 自动生成辅助文件，例如部署描述符或 bean 信息类
- 自动生成用于测试、日志记录、事务语义等的代码

### 8.3.1 注解简介

我们将从基本概念开始讨论注解，并将其应用到一个具体示例中。在该示例中，我们将方法标记为 AWT 组件的事件监听器，并向您展示一个注解处理器，该处理器分析注解并连接监听器。然后我们将详细讨论语法规则，并以两个注解处理的高级示例结束本章。其中一个处理源代码级注解，另一个使用 Apache 字节码工程库处理类文件，向被注解的方法注入额外的字节码。

下面是一个简单注解的示例：

```java
public class MyClass
{
    ...
    @Test public void checkRandomInsertions()
    {
    }
}
```

注解 @Test 对 checkRandomInsertions 方法进行了注解。

在 Java 中，注解的使用方式类似于*修饰符*，并且放在被注解条目之前，*不带分号*。（修饰符是诸如 public 或 static 之类的关键字。）每个注解的名称前面都有一个 @ 符号，类似于 Javadoc 注释。但是，Javadoc 注释位于 /* ... */ 分隔符内，而注解是代码的一部分。

@Test 注解本身并不做任何事情。它需要一个工具才能发挥作用。例如，JUnit 测试工具（可从 http://junit.org 获取）在测试类时会调用所有标记为 @Test 的方法。另一个工具可能会从类文件中删除所有测试方法，以便在测试完成后它们不会随程序一起发布。

注解可以定义*元素*，例如

```java
@Test(timeout="10000")
```

这些元素可以由读取注解的工具来处理。元素还有其他形式；我们将在本章后面讨论。

除了方法之外，您还可以注解类、字段和局部变量——注解可以放在任何可以放置修饰符（如 public 或 static）的位置。此外，正如您将在第 471 页的 8.4 节“注解语法”中看到的，您还可以注解包、参数变量、类型参数和类型使用。


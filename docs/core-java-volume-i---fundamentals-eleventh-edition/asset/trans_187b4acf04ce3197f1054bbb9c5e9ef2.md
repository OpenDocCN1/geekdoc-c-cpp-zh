
如果你不提供处理器，程序将终止并向控制台打印一条消息，给出异常的类型。你可能已经见过这样的异常报告：当你意外使用空引用或越过数组边界时。

异常分为两种：*非受检异常*和*受检异常*。对于受检异常，编译器会检查你（程序员）是否意识到该异常并准备好处理其后果。然而，许多常见异常（例如边界错误或访问空引用）都是非受检的。编译器并不期望你提供处理器——毕竟，你应该把精力花在避免这些错误上，而不是为它们编写处理器。

但并非所有错误都可避免。如果尽管你尽了最大努力，异常仍可能发生，那么大多数 Java API 都会抛出受检异常。一个例子是 `Class.forName` 方法。你无法确保具有给定名称的类存在。在第 7 章中，你将看到几种异常处理策略。现在，我们只向你展示最简单的策略。

只要方法包含可能抛出受检异常的语句，就在方法名中添加 `throws` 子句。

```java
public static void doSomethingWithClass(String name)
   throws ReflectiveOperationException
{
   Class cl = Class.forName(name); // might throw exception
   do something with cl
}
```

任何调用此方法的方法也需要 `throws` 声明。这包括 `main` 方法。如果异常实际发生，`main` 方法会以堆栈跟踪终止。（你将在第 7 章学习如何捕获异常，而不是让它们终止程序。）

你只需要为受检异常提供 `throws` 子句。要找出哪些方法抛出受检异常很容易——每当你调用一个可能抛出受检异常的方法却没有提供处理器时，编译器就会报错。

## 5.7.3 资源

类通常有与之关联的数据文件，例如：

- 图像和声音文件
- 包含消息字符串和按钮标签的文本文件

在 Java 中，这种关联文件称为*资源*。

例如，考虑一个显示消息的对话框，如图 5.3 所示。

![](img/127bccebb2cfadea3f02579edaad63c3_295_0.png)

**图 5.3** 显示图像和文本资源

当然，面板中的书名和版权年份会因本书下一版而改变。为了便于跟踪这一变化，我们会将文本放入文件中，而不是将其硬编码为字符串。

但是，像 about.txt 这样的文件应该放在哪里？当然，直接将它和其余程序文件一起放入 JAR 文件会很方便。

`Class` 类提供了一项用于定位资源文件的有用服务。以下是必要的步骤：

1. 获取拥有资源的类的 `Class` 对象——例如 `ResourceTest.class`。
2. 某些方法（例如 `ImageIcon` 类的 `getImage` 方法）接受描述资源位置的 URL。然后你调用：

    ```java
    URL url = cl.getResource("about.gif");
    ```

3. 否则，使用 `getResourceAsStream` 方法获取一个输入流，用于读取文件中的数据。

关键在于，Java 虚拟机知道如何定位类，因此它可以在同一位置搜索关联资源。例如，假设 `ResourceTest` 类位于名为 `resources` 的包中。那么 `ResourceTest.class` 文件位于 resources 目录中，而你将图标文件放入同一目录。

除了将资源文件放在与类文件相同的目录中，你还可以提供相对或绝对路径，例如

```
data/about.txt
/corejava/title.txt
```

资源加载功能所做的全部事情就是自动加载文件。没有用于解释资源文件内容的标准方法。每个程序都必须有自己的方式来解释其资源文件。

资源的另一个常见应用是程序国际化。依赖语言的字符串（例如消息和用户界面标签）存储在资源文件中，每种语言一个文件。*国际化 API*（在第二卷第 7 章中讨论）支持一种用于组织和访问这些本地化文件的标准方法。

清单 5.13 是一个演示资源加载的程序。（不必担心读取文本和显示对话框的代码——我们稍后会介绍这些细节。）编译、构建 JAR 文件并执行它：

```bash
javac resource/ResourceTest.java
jar cvfe ResourceTest.jar resources.ResourceTest \
    resources/*.class resources/*.gif resources/data/*.txt corejava/*.txt
java -jar ResourceTest.jar
```

将 JAR 文件移动到另一个目录并再次运行，以检查程序是从 JAR 文件（而不是当前目录）读取资源文件。

### 清单 5.13 resources/ResourceTest.java

```java
package resources;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import javax.swing.*;

/**
 * @version 1.5 2018-03-15
 * @author Cay Horstmann
 */
public class ResourceTest
{
    public static void main(String[] args) throws IOException
    {
        Class cl = ResourceTest.class;
        URL aboutURL = cl.getResource("about.gif");
        var icon = new ImageIcon(aboutURL);

        InputStream stream = cl.getResourceAsStream("data/about.txt");
        var about = new String(stream.readAllBytes(), "UTF-8");
```

清单 5.14 向你展示如何打印出某个类的所有信息。该程序提示你输入类名，并写出所有方法和构造器的签名以及该类所有实例字段的名称。例如，如果你输入

```
    java.lang.Double
```

程序会打印

```
    public class java.lang.Double extends java.lang.Number
    {
       public java.lang.Double(java.lang.String);
       public java.lang.Double(double);

       public int hashCode();
       public int compareTo(java.lang.Object);
       public int compareTo(java.lang.Double);
       public boolean equals(java.lang.Object);
       public java.lang.String toString();
       public static java.lang.String toString(double);
       public static java.lang.Double valueOf(java.lang.String);
       public static boolean isNaN(double);
       public boolean isNaN();
       public static boolean isInfinite(double);
       public boolean isInfinite();
       public byte byteValue();
       public short shortValue();
       public int intValue();
       public long longValue();
       public float floatValue();
       public double doubleValue();
       public static double parseDouble(java.lang.String);
       public static native long doubleToLongBits(double);
       public static native long doubleToRawLongBits(double);
       public static native double longBitsToDouble(long);

       public static final double POSITIVE_INFINITY;
       public static final double NEGATIVE_INFINITY;
       public static final double NaN;
       public static final double MAX_VALUE;
       public static final double MIN_VALUE;
       public static final java.lang.Class TYPE;
       private double value;
       private static final long serialVersionUID;
    }
```

这个程序的非凡之处在于，它可以分析 Java 解释器能够加载的任何类，而不仅仅是程序编译时可用的类。我们将在下一章使用这个程序来窥探 Java 编译器自动生成的内部类。

### 清单 5.14 *（续）*

```java
48  public static void printConstructors(Class cl)
49  {
50     Constructor[] constructors = cl.getDeclaredConstructors();
51
52     for (Constructor c : constructors)
53     {
54        String name = c.getName();
55        System.out.print("  ");
56        String modifiers = Modifier.toString(c.getModifiers());
57        if (modifiers.length() > 0) System.out.print(modifiers + " ");
58        System.out.print(name + "(");
59
60        // print parameter types
61        Class[] paramTypes = c.getParameterTypes();
62        for (int j = 0; j < paramTypes.length; j++)
63        {
64           if (j > 0) System.out.print(", ");
65           System.out.print(paramTypes[j].getName());
66        }
67        System.out.println(");");
68     }
69  }
70
71  /**
72   * Prints all methods of a class
73   * @param cl a class
74   */
75  public static void printMethods(Class cl)
76  {
77     Method[] methods = cl.getDeclaredMethods();
78
79     for (Method m : methods)
80     {
81        Class retType = m.getReturnType();
82        String name = m.getName();
83
84        System.out.print("  ");
85        // print modifiers, return type and method name
86        String modifiers = Modifier.toString(m.getModifiers());
87        if (modifiers.length() > 0) System.out.print(modifiers + " ");
88        System.out.print(retType.getName() + " " + name + "(");
89
90        // print parameter types
91        Class[] paramTypes = m.getParameterTypes();
```

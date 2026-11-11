
```java
/**
 * A Java class that holds the bytecodes in a byte array.
 * @version 1.00 2007-11-02
 * @author Cay Horstmann
 */
public class ByteArrayJavaClass extends SimpleJavaFileObject
{
    private ByteArrayOutputStream stream;

    /**
     * Constructs a new ByteArrayJavaClass.
     * @param name the name of the class file represented by this file object
     */
    public ByteArrayJavaClass(String name)
    {
        super(URI.create("bytes:///" + name), Kind.CLASS);
        stream = new ByteArrayOutputStream();
    }

    public OutputStream openOutputStream() throws IOException
    {
        return stream;
    }

    public byte[] getBytes()
    {
        return stream.toByteArray();
    }
}
```

| `javax.tools.Tool` | 6 |
|---|---|
| • `int run(InputStream in, OutputStream out, OutputStream err, String... arguments)` | 使用给定的输入流、输出流和错误流以及给定参数运行该工具。成功返回 0，失败返回非零值。 |

| `javax.tools.JavaCompiler` | 6 |
|---|---|
| • `StandardJavaFileManager getStandardFileManager(DiagnosticListener<?> diagnosticListener, Locale locale, Charset charset)` | 获取此编译器的标准文件管理器。你可以为默认错误报告、区域设置和字符集提供 null。 |

一个非常简单的帧类示例，清单 8.6 展示了按钮操作的代码。注意，帧类的构造函数调用了一个抽象方法 addEventHandlers。我们的代码生成器将生成一个实现 addEventHandlers 方法的子类，为 action.properties 文件中的每一行添加一个动作监听器。（我们把这个众所周知的练习留给读者：将代码生成扩展到其他事件类型。）

我们将子类放入名为 x 的包中，希望该包在程序的其他地方没有被使用。生成的代码形式如下

```java
package x;
public class Frame extends SuperclassName
{
    protected void addEventHandlers()
    {
        componentName_1.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent) { code for event handler_1 }
        });
        // repeat for the other event handlers ...
    }
}
```

清单 8.7 中程序的 buildSource 方法会构建这段代码，并将其放入一个 StringBuilderJavaSource 对象中。该对象被传递给 Java 编译器。

我们使用一个带有 getJavaFileForOutput 方法的 ForwardingJavaFileManager，它为 x 包中的每个类构造一个 ByteArrayJavaClass 对象。这些对象捕获编译 x.Frame 类时生成的类文件。该方法在返回每个文件对象之前将其添加到列表中，以便我们稍后定位字节码。注意，编译 x.Frame 类会为主类生成一个类文件，并为每个监听器类生成一个类文件。

编译后，我们构建一个将类名与字节码数组关联起来的映射。一个简单的类加载器（见清单 8.8）加载存储在该映射中的类。

我们要求类加载器加载刚刚编译的类。然后，我们构造并显示应用程序的帧类。

```java
ClassLoader loader = new MapClassLoader(byteCodeMap);
Class<?> cl = loader.loadClass("x.Frame");
Frame frame = (Frame) cl.newInstance();
frame.setVisible(true);
```

当你单击按钮时，背景颜色会以通常的方式改变。要查看这些操作是动态编译的，请更改 action.properties 中的一行，例如像这样：

```java
yellowButton=panel.setBackground(java.awt.Color.YELLOW); yellowButton.setEnabled(false);
```

再次运行程序。现在，Yellow 按钮在单击后会被禁用。另外，查看一下代码目录。你不会找到 x 包中类的任何源文件或类文件。这个示例演示了如何对内存中的源文件和类文件使用动态编译。

## 清单 8.5 buttons2/ButtonFrame.java

```java
1 package buttons2;
2 import javax.swing.*;
3
4 /**
5  * A frame with a button panel.
6  * @version 1.00 2007-11-02
7  * @author Cay Horstmann
8  */
9 public abstract class ButtonFrame extends JFrame
10 {
11    public static final int DEFAULT_WIDTH = 300;
12    public static final int DEFAULT_HEIGHT = 200;
13
14    protected JPanel panel;
15    protected JButton yellowButton;
16    protected JButton blueButton;
17    protected JButton redButton;
18
19    protected abstract void addEventHandlers();
20
21    public ButtonFrame()
22    {
23       setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
24
25       panel = new JPanel();
26       add(panel);
27
28       yellowButton = new JButton("Yellow");
29       blueButton = new JButton("Blue");
30       redButton = new JButton("Red");
31
32       panel.add(yellowButton);
33       panel.add(blueButton);
34       panel.add(redButton);
35
36       addEventHandlers();
37    }
38 }
```

## 清单 8.7 *（续）*

```java
String frameClassName = args.length == 0 ? "buttons2.ButtonFrame" : args[0];
JavaFileObject source = buildSource(frameClassName);
JavaCompiler.CompilationTask task = compiler.getTask(null, fileManager, diagnostics, null,
    null, Arrays.asList(source));
Boolean result = task.call();

for (Diagnostic<? extends JavaFileObject> d : diagnostics.getDiagnostics())
    System.out.println(d.getKind() + ": " + d.getMessage(null));
fileManager.close();
if (!result)
{
    System.out.println("Compilation failed.");
    System.exit(1);
}

EventQueue.invokeLater(() ->
{
    try
    {
        Map<String, byte[]> byteCodeMap = new HashMap<>();
        for (ByteArrayJavaClass cl : classLoaders)
            byteCodeMap.put(cl.getName().substring(1), cl.getBytes());
        ClassLoader loader = new MapClassLoader(byteCodeMap);
        JFrame frame = (JFrame) loader.loadClass("x.Frame").newInstance();
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setTitle("CompilerTest");
        frame.setVisible(true);
    }
    catch (Exception ex)
    {
        ex.printStackTrace();
    }
});
}

/*
 * Builds the source for the subclass that implements the addEventHandlers method.
 * @return a file object containing the source in a string builder
 */
static JavaFileObject buildSource(String superclassName)
    throws IOException, ClassNotFoundException
{
    StringBuilderJavaSource source = new StringBuilderJavaSource("x.Frame");
    source.append("package x;\n");
    source.append("public class Frame extends " + superclassName + " {");
    source.append("protected void addEventHandlers() {");
    final Properties props = new Properties();
88  props.load(Class.forName(superclassName).getResourceAsStream("action.properties"));
89  for (Map.Entry<Object, Object> e : props.entrySet())
90  {
91      String beanName = (String) e.getKey();
92      String eventCode = (String) e.getValue();
93      source.append(beanName + ".addActionListener(event -> {");
94      source.append(eventCode);
95      source.append("});");
96  }
97  source.append(" }");
98  return source;
99 }
100 }
```

## 清单 8.8 `compiler/MapClassLoader.java`

```java
1  package compiler;
2
3  import java.util.*;
4
5  /**
6   * A class loader that loads classes from a map whose keys are class names and whose values are
7   * byte code arrays.
8   * @version 1.00 2007-11-02
9   * @author Cay Horstmann
10  */
11 public class MapClassLoader extends ClassLoader
12 {
13     private Map<String, byte[]> classes;
14
15     public MapClassLoader(Map<String, byte[]> classes)
16     {
17         this.classes = classes;
18     }
19
20     protected Class<?> findClass(String name) throws ClassNotFoundException
21     {
22         byte[] classBytes = classes.get(name);
23         if (classBytes == null) throw new ClassNotFoundException(name);
24         Class<?> cl = defineClass(name, classBytes, 0, classBytes.length);
25         if (cl == null) throw new ClassNotFoundException(name);
26         return cl;
27     }
28 }
```

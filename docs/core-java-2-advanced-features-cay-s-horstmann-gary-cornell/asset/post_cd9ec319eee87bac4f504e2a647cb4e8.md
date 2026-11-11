
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
| • `int run(InputStream in, OutputStream out, OutputStream err, String... arguments)` | runs the tool with the given input, output, and error streams and the given arguments. Returns 0 for success, a nonzero value for failure. |

| `javax.tools.JavaCompiler` | 6 |
|---|---|
| • `StandardJavaFileManager getStandardFileManager(DiagnosticListener<?> diagnosticListener, Locale locale, Charset charset)` | gets the standard file manager for this compiler. You can supply null for default error reporting, locale, and character set. |

very simple example of a frame class, and Listing 8.6 shows the code for the button actions. Note that the constructor of the frame class calls an abstract method addEventHandlers. Our code generator will produce a subclass that implements the addEventHandlers method, adding an action listener for each line in the action.properties file. (We leave it as the proverbial exercise to the reader to extend the code generation to other event types.)

We place the subclass into a package with the name x, which we hope is not used anywhere else in the program. The generated code has the form

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

The buildSource method in the program of Listing 8.7 builds up this code and places it into a StringBuilderJavaSource object. That object is passed to the Java compiler.

We use a ForwardingJavaFileManager with a getJavaFileForOutput method that constructs a ByteArrayJavaClass object for every class in the x package. These objects capture the class files generated when the x.Frame class is compiled. The method adds each file object to a list before returning it so that we can locate the bytecodes later. Note that compiling the x.Frame class produces a class file for the main class and one class file per listener class.

After compilation, we build a map that associates class names with bytecode arrays. A simple class loader (shown in Listing 8.8) loads the classes stored in this map.

We ask the class loader to load the class that we just compiled. Then, we construct and display the application's frame class.

```java
ClassLoader loader = new MapClassLoader(byteCodeMap);
Class<?> cl = loader.loadClass("x.Frame");
Frame frame = (Frame) cl.newInstance();
frame.setVisible(true);
```

When you click the buttons, the background color changes in the usual way. To see that the actions are dynamically compiled, change one of the lines in action.properties, for example, like this:

```java
yellowButton=panel.setBackground(java.awt.Color.YELLOW); yellowButton.setEnabled(false);
```

Run the program again. Now the Yellow button is disabled after you click it. Also, have a look at the code directories. You will not find any source or class files for the classes in the x package. This example demonstrates how you can use dynamic compilation with in-memory source and class files.

## Listing 8.5 buttons2/ButtonFrame.java

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

## Listing 8.7 *(Continued)*

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

## Listing 8.8 `compiler/MapClassLoader.java`

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

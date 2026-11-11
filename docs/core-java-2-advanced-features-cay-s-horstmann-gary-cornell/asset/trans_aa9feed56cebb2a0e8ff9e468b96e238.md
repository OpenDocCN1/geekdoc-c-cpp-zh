

## 3.7.5 使用 StAX 编写 XML 文档

在前一节中，你了解了如何通过编写 DOM 树来生成 XML 文档。如果你对 DOM 树没有其他用途，这种方法就不太高效。

StAX API 允许你直接写入 XML 树。从 `OutputStream` 构造一个 `XMLStreamWriter`：

```java
XMLOutputFactory factory = XMLOutputFactory.newInstance();
XMLStreamWriter writer = factory.createXMLStreamWriter(out);
```

要生成 XML 头，请调用

```java
writer.writeStartDocument();
```

然后调用

```java
writer.writeStartElement(name);
```

通过调用以下方法添加属性：

```java
writer.writeAttribute(name, value);
```

现在，你可以再次调用 `writeStartElement` 来添加子元素，或者使用以下方法写入字符：

```java
writer.writeCharacters(text);
```

写完全部子节点后，调用

```java
writer.writeEndElement();
```

这将关闭当前元素。

要写入没有子元素的元素（如 `<img ... />`），请使用以下调用：

```java
writer.writeEmptyElement(name);
```

最后，在文档末尾调用

```java
writer.writeEndDocument();
```

此调用会关闭所有未关闭的元素。

你仍然需要关闭 `XMLStreamWriter`，并且必须手动关闭，因为 `XMLStreamWriter` 接口并未扩展 `AutoCloseable` 接口。

与 DOM/XSLT 方法一样，你无需担心属性值和字符数据中的字符转义问题。但是，仍有可能生成格式错误的 XML，例如包含多个根节点的文档。此外，当前版本的 StAX 不支持生成缩进输出。

清单 3.10 中的程序演示了编写 XML 的两种方法。清单 3.11 和 3.12 显示了矩形绘图的框架和组件类。

### 清单 3.10 write/XMLWriteTest.java

```java
    1 package write;
    2 
    3 import java.awt.*;
    4 import javax.swing.*;
    5 
    6 /**
    7  * This program shows how to write an XML file. It saves a file describing a modern drawing in SVG
    8  * format.
    9  * @version 1.12 2016-04-27
    10 * @author Cay Horstmann
    11 */
    12 public class XMLWriteTest
    13 {
    14    public static void main(String[] args)
    15    {
    16       EventQueue.invokeLater(() ->
    17          {
    18             JFrame frame = new XMLWriteFrame();
    19             frame.setTitle("XMLWriteTest");
    20             frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    21             frame.setVisible(true);
    22          });
    23    }
    24 }
```

### 清单 3.11 write/XMLWriteFrame.java

```java
    1 package write;
    2 
    3 import java.io.*;
    4 import java.nio.file.*;
    5 
    6 import javax.swing.*;
    7 import javax.xml.stream.*;
    8 import javax.xml.transform.*;
    9 import javax.xml.transform.dom.*;
    10 import javax.xml.transform.stream.*;
    11 
    12 import org.w3c.dom.*;
    13 

/**
 * A frame with a component for showing a modern drawing.
 */
public class XMLWriteFrame extends JFrame
{
   private RectangleComponent comp;
   private JFileChooser chooser;

   public XMLWriteFrame()
   {
      chooser = new JFileChooser();

      // add component to frame

      comp = new RectangleComponent();
      add(comp);

      // set up menu bar

      JMenuBar menuBar = new JMenuBar();
      setJMenuBar(menuBar);

      JMenu menu = new JMenu("File");
      menuBar.add(menu);

      JMenuItem newItem = new JMenuItem("New");
      menu.add(newItem);
      newItem.addActionListener(event -> comp.newDrawing());

      JMenuItem saveItem = new JMenuItem("Save with DOM/XSLT");
      menu.add(saveItem);
      saveItem.addActionListener(event -> saveDocument());

      JMenuItem saveStAXItem = new JMenuItem("Save with StAX");
      menu.add(saveStAXItem);
      saveStAXItem.addActionListener(event -> saveStAX());

      JMenuItem exitItem = new JMenuItem("Exit");
      menu.add(exitItem);
      exitItem.addActionListener(event -> System.exit(0));
      pack();
   }

   /**
    * Saves the drawing in SVG format, using DOM/XSLT.
    */
public void saveDocument()
{
    try
    {
        if (chooser.showSaveDialog(this) != JFileChooser.APPROVE_OPTION) return;
        File file = chooser.getSelectedFile();
        Document doc = comp.buildDocument();
        Transformer t = TransformerFactory.newInstance().newTransformer();
        t.setOutputProperty(OutputKeys.DOCTYPE_SYSTEM,
            "http://www.w3.org/TR/2000/CR-SVG-20000802/DTD/svg-20000802.dtd");
        t.setOutputProperty(OutputKeys.DOCTYPE_PUBLIC, "-//W3C//DTD SVG 20000802//EN");
        t.setOutputProperty(OutputKeys.INDENT, "yes");
        t.setOutputProperty(OutputKeys.METHOD, "xml");
        t.setOutputProperty("{http://xml.apache.org/xslt}indent-amount", "2");
        t.transform(new DOMSource(doc), new StreamResult(Files.newOutputStream(file.toPath())));
    }
    catch (TransformerException | IOException ex)
    {
        ex.printStackTrace();
    }
}

/**
 * Saves the drawing in SVG format, using StAX.
 */
public void saveStAX()
{
    if (chooser.showSaveDialog(this) != JFileChooser.APPROVE_OPTION) return;
    File file = chooser.getSelectedFile();
    XMLOutputFactory factory = XMLOutputFactory.newInstance();
    try
    {
        XMLStreamWriter writer = factory.createXMLStreamWriter(
            Files.newOutputStream(file.toPath()));
        try
        {
            comp.writeDocument(writer);
        }
        finally
        {
            writer.close(); // Not autocloseable
        }
    }
    catch (XMLStreamException | IOException ex)
    {
        ex.printStackTrace();
    }
}
}
```

### 清单 3.12 `write/RectangleComponent.java`

```java
package write;

import java.awt.*;
import java.awt.geom.*;
import java.util.*;
import javax.swing.*;
import javax.xml.parsers.*;
import javax.xml.stream.*;
import org.w3c.dom.*;

/**
 * A component that shows a set of colored rectangles.
 */
public class RectangleComponent extends JComponent
{
    private static final Dimension PREFERRED_SIZE = new Dimension(300, 200);

    private java.util.List<Rectangle2D> rects;
    private java.util.List<Color> colors;
    private Random generator;
    private DocumentBuilder builder;

    public RectangleComponent()
    {
        rects = new ArrayList<>();
        colors = new ArrayList<>();
        generator = new Random();

        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        factory.setNamespaceAware(true);
        try
        {
            builder = factory.newDocumentBuilder();
        }
        catch (ParserConfigurationException e)
        {
            e.printStackTrace();
        }
    }

    /**
     * Create a new random drawing.
     */
    public void newDrawing()
    {
46  int n = 10 + generator.nextInt(20);
47  rects.clear();
48  colors.clear();
49  for (int i = 1; i <= n; i++)
50  {
51      int x = generator.nextInt(getWidth());
52      int y = generator.nextInt(getHeight());
53      int width = generator.nextInt(getWidth() - x);
54      int height = generator.nextInt(getHeight() - y);
55      rects.add(new Rectangle(x, y, width, height));
56      int r = generator.nextInt(256);
57      int g = generator.nextInt(256);
58      int b = generator.nextInt(256);
59      colors.add(new Color(r, g, b));
60  }
61  repaint();
62  }
63  
64  public void paintComponent(Graphics g)
65  {
66      if (rects.size() == 0) noDrawing();
67      Graphics2D g2 = (Graphics2D) g;
68  
69      // draw all rectangles
70      for (int i = 0; i < rects.size(); i++)
71      {
72          g2.setPaint(colors.get(i));
73          g2.fill(rects.get(i));
74      }
75  }
76  
77  /**
78   * Creates an SVG document of the current drawing.
79   * @return the DOM tree of the SVG document
80   */
81  public Document buildDocument()
82  {
83      String namespace = "http://www.w3.org/2000/svg";
84      Document doc = builder.newDocument();
85      Element svgElement = doc.createElementNS(namespace, "svg");
86      doc.appendChild(svgElement);
87      svgElement.setAttribute("width", "" + getWidth());
88      svgElement.setAttribute("height", "" + getHeight());
89      for (int i = 0; i < rects.size(); i++)
90      {
```


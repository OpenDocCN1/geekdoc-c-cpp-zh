
```xml
<xsd:attribute name="anchor" use="optional" default="CENTER">
    <xsd:simpleType>
        <xsd:restriction base="xsd:string">
            <xsd:enumeration value="NORTH" />
            <xsd:enumeration value="NORTHEAST" />
            <xsd:enumeration value="EAST" />
            <xsd:enumeration value="SOUTHEAST" />
            <xsd:enumeration value="SOUTH" />
            <xsd:enumeration value="SOUTHWEST" />
            <xsd:enumeration value="WEST" />
            <xsd:enumeration value="NORTHWEST" />
        </xsd:restriction>
    </xsd:simpleType>
</xsd:attribute>
<xsd:attribute name="ipady" type="xsd:int" use="optional" default="0" />
<xsd:attribute name="ipadx" type="xsd:int" use="optional" default="0" />
</xsd:complexType>

<xsd:complexType name="BeanType">
    <xsd:sequence>
        <xsd:element name="class" type="xsd:string"/>
        <xsd:element name="property" type="Property" minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
    <xsd:attribute name="id" type="xsd:ID" use="optional" />
</xsd:complexType>

<xsd:complexType name="PropertyType">
    <xsd:sequence>
        <xsd:element name="name" type="xsd:string"/>
        <xsd:element name="value" type="ValueType"/>
    </xsd:sequence>
</xsd:complexType>

<xsd:complexType name="ValueType">
    <xsd:choice>
        <xsd:element ref="bean"/>
        <xsd:element name="int" type="xsd:int"/>
        <xsd:element name="string" type="xsd:string"/>
        <xsd:element name="boolean" type="xsd:boolean"/>
    </xsd:choice>
</xsd:complexType>
</xsd:schema>
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_212_0.png)

Figure 3.5  Evaluating XPath expressions

**Listing 3.7** `xpath/XPathTester.java`

```java
package xpath;

import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.nio.file.*;
import java.util.*;
import javax.swing.*;
import javax.swing.border.*;
import javax.xml.namespace.*;
import javax.xml.parsers.*;
import javax.xml.xpath.*;
import org.w3c.dom.*;
import org.xml.sax.*;

/**
 * This program evaluates XPath expressions.
 * @version 1.02 2016-05-10
 * @author Cay Horstmann
 */
public class XPathTester
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
      {
         JFrame frame = new XPathFrame();
         frame.setTitle("XPathTest");
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         frame.setVisible(true);
      });
   }

   /**
    * This frame shows an XML document, a panel to type an XPath expression, and a text field to
    * display the result.
    */
   class XPathFrame extends JFrame
   {
      private DocumentBuilder builder;
      private Document doc;
      private XPath path;
      private JTextField expression;
      private JTextField result;
      private JTextArea docText;
      private JComboBox<String> typeCombo;

      public XPathFrame()
      {
         JMenu fileMenu = new JMenu("File");
         JMenuItem openItem = new JMenuItem("Open");
         openItem.addActionListener(event -> openFile());
         fileMenu.add(openItem);

         JMenuItem exitItem = new JMenuItem("Exit");
         exitItem.addActionListener(event -> System.exit(0));
         fileMenu.add(exitItem);

         JMenuBar menuBar = new JMenuBar();
         menuBar.add(fileMenu);
         setJMenuBar(menuBar);

         ActionListener listener = event -> evaluate();
         expression = new JTextField(20);
         expression.addActionListener(listener);
         JButton evaluateButton = new JButton("Evaluate");
         evaluateButton.addActionListener(listener);

         typeCombo = new JComboBox<String>(new String[] {
            "STRING", "NODE", "NODESET", "NUMBER", "BOOLEAN" });
         typeCombo.setSelectedItem("STRING");

         JPanel panel = new JPanel();
         panel.add(expression);
         panel.add(typeCombo);
         panel.add(evaluateButton);
         docText = new JTextArea(10, 40);
         result = new JTextField();
         result.setBorder(new TitledBorder("Result"));
         add(panel, BorderLayout.NORTH);
         add(new JScrollPane(docText), BorderLayout.CENTER);
         add(result, BorderLayout.SOUTH);

         try
         {
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            builder = factory.newDocumentBuilder();
         }
         catch (ParserConfigurationException e)
         {
            JOptionPane.showMessageDialog(this, e);
         }

         XPathFactory xfactory = XPathFactory.newInstance();
         path = xfactory.newXPath();
         pack();
      }

      /**
       * Open a file and load the document.
       */
      public void openFile()
      {
         JFileChooser chooser = new JFileChooser();
         chooser.setCurrentDirectory(new File("xpath"));

         chooser.setFileFilter(
            new javax.swing.filechooser.FileNameExtensionFilter("XML files", "xml"));
         int r = chooser.showOpenDialog(this);
         if (r != JFileChooser.APPROVE_OPTION) return;
         File file = chooser.getSelectedFile();

         try
         {
            docText.setText(new String(Files.readAllBytes(file.toPath())));
         }
         catch (IOException e)
         {
            JOptionPane.showMessageDialog(this, e);
         }
         catch (SAXException e)
         {
            JOptionPane.showMessageDialog(this, e);
         }
      }

      public void evaluate()
      {
         try
         {
            String typeName = (String) typeCombo.getSelectedItem();
            QName returnType = (QName) XPathConstants.class.getField(typeName).get(null);
            Object evalResult = path.evaluate(expression.getText(), doc, returnType);
            if (typeName.equals("NODESET"))
            {
               NodeList list = (NodeList) evalResult;
               // Can't use String.join since NodeList isn't Iterable
               StringJoiner joiner = new StringJoiner(", ", "{", "}");
               for (int i = 0; i < list.getLength(); i++)
                  joiner.add("" + list.item(i));
               result.setText("" + joiner);
            }
            else result.setText("" + evalResult);
         }
         catch (XPathExpressionException e)
         {
            result.setText("" + e);
         }
         catch (Exception e) // reflection exception
         {
            e.printStackTrace();
         }
      }
   }
}
```

| `javax.xml.xpath.XPathFactory` | 5.0 |
|---|---|
| `static XPathFactory newInstance()` | returns an XPathFactory instance for creating XPath objects. |
| `XPath newXPath()` | constructs an XPath object for evaluating XPath expressions. |

`javax.xml.xpath.XPath 5.0`

- `String evaluate(String expression, Object startingPoint)`
    evaluates an expression, beginning at the given starting point. The starting point can be a node or node list. If the result is a node or node set, the returned string consists of the data of all text node children.
- `Object evaluate(String expression, Object startingPoint, QName resultType)`
    evaluates an expression, beginning at the given starting point. The starting point can be a node or node list. The resultType is one of the constants STRING, NODE, NODESET, NUMBER, or BOOLEAN in the XPathConstants class. The return value is a String, Node, NodeList, Number, or Boolean.

## 3.5 Using Namespaces

The Java language uses packages to avoid name clashes. Programmers can use the same name for different classes as long as they aren't in the same package. XML has a similar *namespace* mechanism for element and attribute names.

A namespace is identified by a Uniform Resource Identifier (URI), such as

```text
http://www.w3.org/2001/XMLSchema
uuid:1c759aed-b748-475c-ab68-10679700c4f2
urn:com:books-r-us
```

The HTTP URL form is the most common. Note that the URL is just used as an identifier string, not as a locator for a document. For example, the namespace identifiers

```text
http://www.horstmann.com/corejava
http://www.horstmann.com/corejava/index.html
```

denote *different* namespaces, even though a web server would serve the same document for both URLs.

There need not be any document at a namespace URL—the XML parser doesn't attempt to find anything at that location. However, as a help to programmers who encounter a possibly unfamiliar namespace, it is customary to place a document explaining the purpose of the namespace at the URL location. For example, if you point your browser to the namespace URL for the XML Schema namespace (http://www.w3.org/2001/XMLSchema), you will find a document describing the XML Schema standard.

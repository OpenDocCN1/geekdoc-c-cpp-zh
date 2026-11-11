
![](img/7dd923a566750151a3aab0dacd0cdaa5_197_0.png)

Figure 3.4 A font dialog defined by an XML layout

a class that has a no-argument constructor and getter/setter pairs for reading and writing properties. (Such a class is called a JavaBean.)

A bean is defined by a class name and zero or more properties:

```dtd
<!ELEMENT bean (class, property*)>
<!ELEMENT class (#PCDATA)>
```

A property contains a name and a value:

```dtd
<!ELEMENT property (name, value)>
<!ELEMENT name (#PCDATA)>
```

The value is an integer, boolean, string, or another bean:

```dtd
<!ELEMENT value (int|string|boolean|bean)>
<!ELEMENT int (#PCDATA)>
<!ELEMENT string (#PCDATA)>
<!ELEMENT boolean (#PCDATA)>
```

Here is a typical example—a JLabel whose text property is set to the string "Face: " :

```xml
<bean>
  <class>javax.swing.JLabel</class>
  <property>
    <name>text</name>
    <value><string>Face: </string></value>
  </property>
</bean>
```

It seems like a bother to surround a string with the `<string>` tag. Why not just use `#PCDATA` for strings and leave the tags for the other types? Because then we would need to use mixed content and weaken the rule for the value element to

```dtd
<!ELEMENT value (#PCDATA | int | boolean | bean)*>
```

Such a rule would allow an arbitrary mixture of text and tags.

The program sets a property by using the BeanInfo class. BeanInfo enumerates the property descriptors of the bean. We search for the property with the matching name, and then call its setter method with the supplied value.

When our program reads in a user interface description, it has enough information to construct and arrange the user interface components. But, of course, the interface is not alive—no event listeners have been attached. To add event listeners, we have to locate the components. For that reason, we support an optional attribute of type ID for each bean:

```dtd
<!ATTLIST bean id ID #IMPLIED>
```

For example, here is a combo box with an ID:

```xml
<bean id="face">
  <class>javax.swing.JComboBox</class>
</bean>
```

Recall that the parser checks that IDs are unique.

A programmer can attach event handlers like this:

```java
gridBag = new GridBagPane("fontDialog.xml");
setContentPane(gridBag);
JComboBox face = (JComboBox) gridBag.get("face");
face.addActionListener(listener);
```

> **NOTE:** In this example, we only use XML to describe the component layout and leave it to programmers to attach the event handlers in the Java code. You could go a step further and add the code to the XML description. The most promising approach is to use a scripting language such as JavaScript for the code. If you want to add that enhancement, check out the Nashorn JavaScript interpreter described in Chapter 8.

The program in Listing 3.2 shows how to use the `GridBagPane` class to do all the boring work of setting up the grid bag layout. The layout is defined in Listing 3.4; Figure 3.4 shows the result. The program only initializes the combo boxes (which are too complex for the bean property-setting mechanism that the `GridBagPane` supports) and attaches event listeners. The `GridBagPane` class in Listing 3.3 parses the XML file, constructs the components, and lays them out. Listing 3.5 shows the DTD.

The program can also process a schema instead of a DTD if you choose a file that contains the string `-schema`.

Listing 3.6 contains the schema.

This example is a typical use of XML. The XML format is robust enough to express complex relationships. The XML parser adds value by taking over the routine job of validity checking and supplying defaults.

### Listing 3.2 read/GridBagTest.java

```java
package read;

import java.awt.*;
import java.awt.event.*;
import java.io.*;
import javax.swing.*;

/**
 * This program shows how to use an XML file to describe a gridbag layout.
 * @version 1.12 2016-04-27
 * @author Cay Horstmann
 */
public class GridBagTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
      {
         JFileChooser chooser = new JFileChooser(".");
         chooser.showOpenDialog(null);
         File file = chooser.getSelectedFile();
         JFrame frame = new FontFrame(file);
         frame.setTitle("GridBagTest");
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         frame.setVisible(true);
      });
   }
}

/**
 * This frame contains a font selection dialog that is described by an XML file.
 * @param file the file containing the user interface components for the dialog
 */
class FontFrame extends JFrame
{
   private GridBagPane gridbag;
   private JComboBox<String> face;
   private JComboBox<String> size;
   private JCheckBox bold;
   private JCheckBox italic;

   @SuppressWarnings("unchecked")
   public FontFrame(File file)
   {
      gridbag = new GridBagPane(file);
      add(gridbag);

      face = (JComboBox<String>) gridbag.get("face");
      size = (JComboBox<String>) gridbag.get("size");
      bold = (JCheckBox) gridbag.get("bold");
      italic = (JCheckBox) gridbag.get("italic");

      face.setModel(new DefaultComboBoxModel<String>(new String[] { "Serif",
            "SansSerif", "Monospaced", "Dialog", "DialogInput" }));

      size.setModel(new DefaultComboBoxModel<String>(new String[] { "8",
            "10", "12", "15", "18", "24", "36", "48" }));

      ActionListener listener = event -> setSample();

      face.addActionListener(listener);
      size.addActionListener(listener);
      bold.addActionListener(listener);
      italic.addActionListener(listener);

      setSample();
      pack();
   }

   /**
    * This method sets the text sample to the selected font.
    */
   public void setSample()
   {
      String fontFace = face.getItemAt(face.getSelectedIndex());
      int fontSize = Integer.parseInt(size.getItemAt(size.getSelectedIndex()));
      JTextArea sample = (JTextArea) gridbag.get("sample");
      int fontStyle = (bold.isSelected() ? Font.BOLD : 0)
                    + (italic.isSelected() ? Font.ITALIC : 0);

      sample.setFont(new Font(fontFace, fontStyle, fontSize));
      sample.repaint();
   }
}
```

### Listing 3.3 read/GridBagPane.java

```java
package read;

import java.awt.*;
import java.beans.*;
import java.io.*;
import java.lang.reflect.*;
import javax.swing.*;
import javax.xml.parsers.*;
import org.w3c.dom.*;

/**
 * This panel uses an XML file to describe its components and their grid bag layout positions.
 */
public class GridBagPane extends JPanel
{
    private GridBagConstraints constraints;

    /**
     * Constructs a grid bag pane.
     * @param file the name of the XML file that describes the pane's components and their
     * positions
     */
    public GridBagPane(File file)
    {
        setLayout(new GridBagLayout());
        constraints = new GridBagConstraints();

        try
        {
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            factory.setValidating(true);

            if (file.toString().contains("-schema"))
            {
                factory.setNamespaceAware(true);
                final String JAXP_SCHEMA_LANGUAGE =
                    "http://java.sun.com/xml/jaxp/properties/schemaLanguage";
                final String W3C_XML_SCHEMA = "http://www.w3.org/2001/XMLSchema";
                factory.setAttribute(JAXP_SCHEMA_LANGUAGE, W3C_XML_SCHEMA);
            }

            factory.setIgnoringElementContentWhitespace(true);

            DocumentBuilder builder = factory.newDocumentBuilder();
            Document doc = builder.parse(file);
            parseGridbag(doc.getDocumentElement());
        }
        catch (Exception e)
        {
            e.printStackTrace();
        }
    }

    /**
     * Gets a component with a given name.
     * @param name a component name
     * @return the component with the given name, or null if no component in this grid bag pane has
     * the given name
     */
    public Component get(String name)
    {
        Component[] components = getComponents();
        for (int i = 0; i < components.length; i++)
        {
            if (components[i].getName().equals(name)) return components[i];
        }
        return null;
    }

    /**
     * Parses a gridbag element.
     * @param e a gridbag element
     */
    private void parseGridbag(Element e)
    {
        NodeList rows = e.getChildNodes();
        for (int i = 0; i < rows.getLength(); i++)
        {
            Element row = (Element) rows.item(i);
            NodeList cells = row.getChildNodes();
```

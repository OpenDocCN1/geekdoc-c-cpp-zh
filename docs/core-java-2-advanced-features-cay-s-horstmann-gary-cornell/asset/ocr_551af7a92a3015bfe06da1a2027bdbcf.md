# Listing 3.11 *(Continued)*

```
```java
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
```
```
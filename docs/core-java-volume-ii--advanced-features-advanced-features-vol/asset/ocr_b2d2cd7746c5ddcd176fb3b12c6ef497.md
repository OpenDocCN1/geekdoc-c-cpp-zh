# Listing 8.3 *(Continued)*

```
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
```

# Listing 8.4 `buttons2/ButtonFrame.java`

```
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

   protected abstract void addEventHandlers();
}
```
```
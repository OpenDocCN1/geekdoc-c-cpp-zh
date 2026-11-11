```
~~~java
DocumentListener listener = new DocumentListener()
{
   public void insertUpdate(DocumentEvent event) { setColor(); }
   public void removeUpdate(DocumentEvent event) { setColor(); }
   public void changedUpdate(DocumentEvent event) { }
};
~~~
```

The `setColor` method uses the `getText` method to obtain the current user input strings from the text fields and sets the color.

Our program has one limitation. Users can type malformed input, such as "twenty", into the text field, or leave a field blank. For now, we catch the `NumberFormatException` that the `parseInt` method throws, and we simply don't update the color when the text field entry is not a number. In the next section, you will see how you can prevent the user from entering invalid input in the first place.

> > **NOTE:** Instead of listening to document events, you can add an action event listener to a text field. The action listener is notified whenever the user presses the Enter key. We don't recommend this approach, because users don't always remember to press Enter when they are done entering data. If you use an action listener, you should also install a focus listener so that you can track when the user leaves the text field.

# ### Listing 10.19 textChange/ColorFrame.java

```
~~~java
package textChange;

import java.awt.*;
import javax.swing.*;
import javax.swing.event.*;

/**
 * A frame with three text fields to set the background color.
 */
public class ColorFrame extends JFrame
{
   private JPanel panel;
   private JTextField redField;
   private JTextField greenField;
   private JTextField blueField;

   public ColorFrame()
   {
~~~
```
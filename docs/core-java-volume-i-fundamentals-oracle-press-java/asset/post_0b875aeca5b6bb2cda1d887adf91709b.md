
- 3. If you really want to go all out, combine several borders with a call to `BorderFactory.createCompoundBorder`.
- 4. Add the resulting border to your component by calling the `setBorder` method of the `JComponent` class.

For example, here is how you add an etched border with a title to a panel:

```java
Border etched = BorderFactory.createEtchedBorder();
Border titled = BorderFactory.createTitledBorder(etched, "A Title");
panel.setBorder(titled);
```

Different borders have different options for setting border widths and colors; see the API notes for details. True border enthusiasts will appreciate that there is also a `SoftBevelBorder` class for beveled borders with softened corners and that a `Border` can have rounded corners as well. You can construct these borders only by using one of the class constructors—there is no `BorderFactory` method for them.

### **javax.swing.BorderFactory** *1.2*

- `static Border createLineBorder(Color color)`
- `static Border createLineBorder(Color color, int thickness)`  
  creates a simple line border.
- `static MatteBorder createMatteBorder(int top, int left, int bottom, int right, Color color)`
- `static MatteBorder createMatteBorder(int top, int left, int bottom, int right, Icon tileIcon)`  
  creates a thick border that is filled with a color or a repeating icon.
- `static Border createEmptyBorder()`
- `static Border createEmptyBorder(int top, int left, int bottom, int right)`  
  creates an empty border.
- `static Border createEtchedBorder()`
- `static Border createEtchedBorder(Color highlight, Color shadow)`
- `static Border createEtchedBorder(int type)`
- `static Border createEtchedBorder(int type, Color highlight, Color shadow)`  
  creates a line border with a 3D effect. The type parameter is one of `EtchedBorder.RAISED`, `EtchedBorder.LOWERED`.
- `static Border createBevelBorder(int type)`
- `static Border createBevelBorder(int type, Color highlight, Color shadow)`
- `static Border createLoweredBevelBorder()`
- `static Border createRaisedBevelBorder()`  
  creates a border that gives the effect of a lowered or raised surface. The type parameter is one of `BevelBorder.RAISED`, `BevelBorder.LOWERED`.
- `static TitledBorder createTitledBorder(String title)`
- `static TitledBorder createTitledBorder(Border border)`
- `static TitledBorder createTitledBorder(Border border, String title)`
- `static TitledBorder createTitledBorder(Border border, String title, int justification, int position)`
- `static TitledBorder createTitledBorder(Border border, String title, int justification, int position, Font font)`
- `static TitledBorder createTitledBorder(Border border, String title, int justification, int position, Font font, Color color)`  
  creates a titled border with the specified properties. The justification parameter is one of the `TitledBorder` constants `LEFT`, `CENTER`, `RIGHT`, `LEADING`, `TRAILING`, or `DEFAULT_JUSTIFICATION` (left), and position is one of `ABOVE_TOP`, `TOP`, `BELOW_TOP`, `ABOVE_BOTTOM`, `BOTTOM`, `BELOW_BOTTOM`, or `DEFAULT_POSITION` (top).
- `static CompoundBorder createCompoundBorder(Border outsideBorder, Border insideBorder)`  
  combines two borders to a new border.

### **javax.swing.border.SoftBevelBorder** 1.2

- `SoftBevelBorder(int type)`
- `SoftBevelBorder(int type, Color highlight, Color shadow)`  
  creates a bevel border with softened corners. The type parameter is one of `SoftBevelBorder.RAISED`, `SoftBevelBorder.LOWERED`.

### **javax.swing.border.LineBorder** 1.2

- `public LineBorder(Color color, int thickness, boolean roundedCorners)`  
  creates a line border with the given color and thickness. If roundedCorners is true, the border has rounded corners.

### **javax.swing.JComponent** 1.2

- `void setBorder(Border border)`  
  sets the border of this component.

## 11.4.4 Combo Boxes

an editable combo box, that item may have any type, depending on the editor that takes the user edits and turns the result into an object. (See Volume II, Chapter 6 for a discussion of editors.) If your combo box isn’t editable, you are better off calling

```java
combo.getItemAt(combo.getSelectedIndex())
```

which gives you the selected item with the correct type.

In the example program, the user can choose a font style from a list of styles (Serif, SansSerif, Monospaced, etc.). The user can also type in another font.

Add the choice items with the `addItem` method. In our program, `addItem` is called only in the constructor, but you can call it any time.

```java
var faceCombo = new JComboBox<String>();
faceCombo.addItem("Serif");
faceCombo.addItem("SansSerif");
. . .
```

This method adds the string to the end of the list. You can add new items anywhere in the list with the `insertItemAt` method:

```java
faceCombo.insertItemAt("Monospaced", 0); // add at the beginning
```

You can add items of any type—the combo box invokes each item’s `toString` method to display it.

If you need to remove items at runtime, use the `removeItem` or `removeItemAt` method, depending on whether you supply the item to be removed or its position.

```java
faceCombo.removeItem("Monospaced");
faceCombo.removeItemAt(0); // remove first item
```

The `removeAllItems` method removes all items at once.

> **TIP:**
>
> If you need to add a large number of items to a combo box, the `addItem` method will perform poorly. Instead, construct a `DefaultComboBoxModel`, populate it by calling `addElement`, and then call the `setModel` method of the `JComboBox` class.

When the user selects an item from a combo box, the combo box generates an action event. To find out which item was selected, call `getSource` on the event parameter to get a reference to the combo box that sent the event. Then call the `getSelectedItem` method to retrieve the currently selected item. You will need to cast the returned value to the appropriate type, usually `String`.

```java
ActionListener listener = event ->
    label.setFont(new Font(
        faceCombo.getItemAt(faceCombo.getSelectedIndex()),
        Font.PLAIN,
        DEFAULT_SIZE));
```

Listing 11.4 shows the complete program.

### **Listing 11.4** comboBox/ComboBoxFrame.java

```java
package comboBox;

import java.awt.BorderLayout;
import java.awt.Font;

import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;

/**
 * A frame with a sample text label and a combo box for
 * selecting font faces.
 */
public class ComboBoxFrame extends JFrame
{
    private JComboBox<String> faceCombo;
    private JLabel label;
    private static final int DEFAULT_SIZE = 24;

    public ComboBoxFrame()
    {
        // add the sample text label

        label = new JLabel("The quick brown fox jumps over the lazy dog.");
        label.setFont(new Font("Serif", Font.PLAIN, DEFAULT_SIZE));
        add(label, BorderLayout.CENTER);

        // make a combo box and add face names

        faceCombo = new JComboBox<>();
        faceCombo.addItem("Serif");
        faceCombo.addItem("SansSerif");
        faceCombo.addItem("Monospaced");
        faceCombo.addItem("Dialog");
        faceCombo.addItem("DialogInput");

        // the combo box listener changes the label font to the selected face name

        faceCombo.addActionListener(event ->
            label.setFont(
                new Font(faceCombo.getItemAt(faceCombo.getSelectedIndex()),
                    Font.PLAIN, DEFAULT_SIZE)));

        // add combo box to a panel at the frame's southern
45        // border
46    var comboPanel = new JPanel();
47    comboPanel.add(faceCombo);
48    add(comboPanel, BorderLayout.SOUTH);
49    pack();
50 }
51}
```

### javax.swing.JComboBox 1.2

- `boolean isEditable()`
- `void setEditable(boolean b)`  
  gets or sets the editable property of this combo box.
- `void addItem(Object item)`  
  adds an item to the item list.
- `void insertItemAt(Object item, int index)`  
  inserts an item into the item list at a given index.
- `void removeItem(Object item)`  
  removes an item from the item list.
- `void removeItemAt(int index)`  
  removes the item at an index.
- `void removeAllItems()`  
  removes all items from the item list.
- `Object getSelectedItem()`  
  returns the currently selected item.

## 11.4.5 Sliders


| javax.swing.JTextArea 1.2 *(Continued)* |
| --- |
| - `void setWrapStyleWord(boolean word)`<br>If word is true, long lines are wrapped at word boundaries. If it is false, long lines are broken without taking word boundaries into account.<br><br>- `void setTabSize(int c)`<br>sets tab stops every c columns. Note that the tabs aren’t converted to spaces but cause alignment with the next tab stop. |

| javax.swing.JScrollPane 1.2 |
| --- |
| - `JScrollPane(Component c)`<br>creates a scroll pane that displays the content of the specified component. Scrollbars are supplied when the component is larger than the view. |

## 11.4 Choice Components

You now know how to collect text input from users, but there are many occasions where you would rather give users a finite set of choices than have them enter the data in a text component. Using a set of buttons or a list of items tells your users what choices you have. (It also saves you the trouble of error checking.) In this section, you will learn how to program checkboxes, radio buttons, lists of choices, and sliders.

### 11.4.1 Checkboxes

If you want to collect just a “yes” or “no” input, use a checkbox component. Checkboxes automatically come with labels that identify them. The user can check the box by clicking inside it and turn off the checkmark by clicking inside the box again. Pressing the space bar when the focus is in the checkbox also toggles the checkmark.

Figure 11.12 shows a simple program with two checkboxes, one for turning the italic attribute of a font on or off, and the other for boldface. Note that the second checkbox has focus, as indicated by the rectangle around the label. Each time the user clicks one of the checkboxes, the screen is refreshed, using the new font attributes.

**Listing 11.2** *(Continued)*

```java
48    add(buttonPanel, BorderLayout.SOUTH);
49    pack();
50 }
51}
52 }
```

| `javax.swing.JCheckBox` | 1.2 |
| --- | --- |
| - `JCheckBox(String label)`<br>- `JCheckBox(String label, Icon icon)` | constructs a checkbox that is initially unselected. |
| - `JCheckBox(String label, boolean state)` | constructs a checkbox with the given label and initial state. |
| - `boolean isSelected()`<br>- `void setSelected(boolean state)` | gets or sets the selection state of the checkbox. |

### 11.4.2 Radio Buttons

In the previous example, the user could check either, both, or neither of the two checkboxes. In many cases, we want the user to check only one of several boxes. When another box is checked, the previous box is automatically unchecked. Such a group of boxes is often called a *radio button group* because the buttons work like the station selector buttons on a radio. When you push in one button, the previously depressed button pops out. Figure 11.13 shows a typical example. We allow the user to select a font size from among the choices—Small, Medium, Large, or Extra large—but, of course, we will allow selecting only one size at a time.

Implementing radio button groups is easy in Swing. You construct one object of type `ButtonGroup` for every group of buttons. Then, you add objects of type `JRadioButton` to the button group. The button group object is responsible for turning off the previously set button when a new button is clicked.

```java
var group = new ButtonGroup();

var smallButton = new JRadioButton("Small", false);
group.add(smallButton);

var mediumButton = new JRadioButton("Medium", true);
group.add(mediumButton);
. . .
```

![](img/127bccebb2cfadea3f02579edaad63c3_681_0.png)

**Figure 11.13** A radio button group

The second argument of the constructor is true for the button that should be checked initially and false for all others. Note that the button group controls only the *behavior* of the buttons; if you want to group the buttons for layout purposes, you also need to add them to a container such as a JPanel.

If you look again at Figures 11.12 and 11.13, you will note that the appearance of the radio buttons is different from that of checkboxes. Checkboxes are square and contain a checkmark when selected. Radio buttons are round and contain a dot when selected.

The event notification mechanism for radio buttons is the same as for any other buttons. When the user checks a radio button, the button generates an action event. In our example program, we define an action listener that sets the font size to a particular value:

```java
ActionListener listener = event ->
    label.setFont(new Font("Serif", Font.PLAIN, size));
```

Compare this listener setup to that of the checkbox example. Each radio button gets a different listener object. Each listener object knows exactly what it needs to do—set the font size to a particular value. With checkboxes, we used a different approach: Both checkboxes have the same action listener that calls a method looking at the current state of both checkboxes.

Could we follow the same approach here? We could have a single listener that computes the size as follows:

```java
if (smallButton.isSelected()) size = 8;
else if (mediumButton.isSelected()) size = 12;
...
```

However, we prefer to use separate action listener objects because they tie the size values more closely to the buttons.

> **NOTE:** If you have a group of radio buttons, you know that only one of them is selected. It would be nice to be able to quickly find out which, without having to query all the buttons in the group. The ButtonGroup object controls all buttons, so it would be convenient if this object could give us a reference to the selected button. Indeed, the ButtonGroup class has a getSelection method, but that method doesn't return the radio button that is selected. Instead, it returns a ButtonModel reference to the model attached to the button. Unfortunately, none of the ButtonModel methods are very helpful. The ButtonModel interface inherits a method getSelectedObjects from the ItemSelectable interface that, rather uselessly, returns null. The getActionCommand method looks promising because the "action command" of a radio button is its text label. But the action command of its model is null. Only if you explicitly set the action command of all radio buttons with the setActionCommand method do the action command values of the models also get set. Then you can retrieve the action command of the currently selected button with buttonGroup.getSelection().getActionCommand().

Listing 11.3 is the complete program for font size selection that puts a set of radio buttons to work.

**Listing 11.3** radioButton/RadioButtonFrame.java

```java
package radioButton;

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

/**
 * A frame with a sample text label and radio buttons for selecting font sizes.
 */
public class RadioButtonFrame extends JFrame
{
   private JPanel buttonPanel;
   private ButtonGroup group;
   private JLabel label;
   private static final int DEFAULT_SIZE = 36;

   public RadioButtonFrame()
   {
      // add the sample text label

      label = new JLabel("The quick brown fox jumps over the lazy dog.");
      label.setFont(new Font("Serif", Font.PLAIN, DEFAULT_SIZE));

      add(label, BorderLayout.CENTER);

      // add the radio buttons

      buttonPanel = new JPanel();
      group = new ButtonGroup();

      addRadioButton("Small", 8);
      addRadioButton("Medium", 12);
      addRadioButton("Large", 18);
      addRadioButton("Extra large", 36);

      add(buttonPanel, BorderLayout.SOUTH);
      pack();
   }

   /**
    * Adds a radio button that sets the font size of the sample text.
    * @param name the string to appear on the button
    * @param size the font size that this button sets
    */
   public void addRadioButton(String name, int size)
   {
      boolean selected = size == DEFAULT_SIZE;
      var button = new JRadioButton(name, selected);
      group.add(button);
      buttonPanel.add(button);

      // this listener sets the label font size

      ActionListener listener = event -> label.setFont(new Font("Serif", Font.PLAIN, size));

      button.addActionListener(listener);
   }
}
```

| javax.swing.JRadioButton 1.2 |
| --- |
| - `JRadioButton(String label, Icon icon)`<br>constructs a radio button that is initially unselected. |
| - `JRadioButton(String label, boolean state)`<br>constructs a radio button with the given label and initial state. |

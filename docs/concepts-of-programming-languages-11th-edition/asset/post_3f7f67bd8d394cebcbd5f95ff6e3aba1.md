
The constructor for radio buttons takes two parameters: a label and the initial state of the radio button (true or false, for pressed and not pressed, respectively). If one radio button in a group is initially set to pressed, the others in the group default to unpressed. After the radio buttons are created, they are placed in their button group with the add method of the group object. Consider the following example:

```java
ButtonGroup payment = new ButtonGroup();
JRadioButton box1 = new JRadioButton("Visa", true);
JRadioButton box2 = new JRadioButton("Master Charge");
JRadioButton box3 = new JRadioButton("Discover");
payment.add(box1);
payment.add(box2);
payment.add(box3);
```

A JFrame object is a frame, which is displayed as a separate window. The JFrame class defines the data and methods that are needed for frames. So, a class that uses a frame can be a subclass of JFrame. A JFrame has several layers called panes. We are interested in just one of those layers, the content pane. Components of a GUI are placed in a JPanel object (a panel), which is used to organize and define the layout of the components. A frame is created and the panel containing the components is added to that frame's content pane.

Predefined graphic objects, such as GUI components, are placed directly in a panel. The following creates the panel object used in the following discussion of components:

```java
JPanel myPanel = new JPanel();
```

After the components have been created with constructors, they are placed in the panel with the add method, as in

```java
myPanel.add(button1);
```

### 14.6.2 The Java Event Model

When a user interacts with a GUI component, for example by clicking a button, the component creates an event object and calls an event handler through an object called an event listener, passing the event object. The event handler provides the associated actions. GUI components are event generators. In Java, events are connected to event handlers through event listeners. Event listeners are connected to event generators through event listener registration. Listener registration is done with a method of the class that implements the listener interface, as described later in this section. Only event listeners that are registered for a specific event are notified when that event occurs.

The listener method that receives the message implements an event handler. To make the event-handling methods conform to a standard protocol, an interface is used. An interface prescribes standard method protocols but does not provide implementations of those methods.

A class that needs to implement an event handler must implement an interface for the listener for that handler. There are several classes of events and listener interfaces. One class of events is `ItemEvent`, which is associated with the event of clicking a checkbox or a radio button, or selecting a list item. The `ItemListener` interface includes the protocol of a method, `itemStateChanged`, which is the handler for `ItemEvent` events. So, to provide an action that is triggered by a radio button click, the interface `ItemListener` must be implemented, which requires a definition of the method, `itemStateChanged`.

As stated previously, the connection of a component to an event listener is made with a method of the class that implements the listener interface. For example, because `ItemEvent` is the class name of event objects created by user actions on radio buttons, the `addItemListener` method is used to register a listener for radio buttons. The listener for button events created in a panel could be implemented in the panel or a subclass of `JPanel`. So, for a radio button named `button1` in a panel named `myPanel` that implements the `ItemEvent` handler for buttons, we would register the listener with the following statement:

```java
button1.addItemListener(this);
```

Each event handler method receives an event parameter, which provides information about the event. Event classes have methods to access that information. For example, when called through a radio button, the `isSelected` method returns `true` or `false`, depending on whether the button was on or off (pressed or not pressed), respectively.

All the event-related classes are in the `java.awt.event` package, so it is imported to any class that uses events.

The following is an example application, `RadioB`, that illustrates the use of events and event handling. This application constructs radio buttons that control the font style of the contents of a text field. It creates a `Font` object for each of four font styles. Each of these has a radio button to enable the user to select the font style.

The purpose of this example is to show how events raised by GUI components can be handled to change the output display of the program dynamically. Because of our narrow focus on event handling, some parts of this program are not explained here.

```java
/* RadioB.java
   An example to illustrate event handling with interactive
   radio buttons that control the font style of a textfield
*/
package radiob;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class RadioB extends JPanel implements
    ItemListener {
    private JTextField text;
```

**Figure 14.2**  
Output of `RadioB.java`  
Source: Java radio applet screenshot.

![](img/e22931b583977bc24a4263ee43d0f0bb_650_0.png)

```java
// The event handler
public void itemStateChanged(ItemEvent e) {
    // Determine which button is on and set the font
    // accordingly
    if (plain.isSelected())
        text.setFont(plainFont);
    else if (bold.isSelected())
        text.setFont(boldFont);
    else if (italic.isSelected())
        text.setFont(italicFont);
    else if (boldItalic.isSelected())
        text.setFont(boldItalicFont);
} // End of itemStateChanged

// The main method
public static void main(String[] args) {
    // Create the window frame
    JFrame myFrame = new JFrame("Radio button example");

    // Create the content pane and set it to the frame
    JComponent myContentPane = new RadioB();
    myContentPane.setOpaque(true);
    myFrame.setContentPane(myContentPane);

    // Display the window.
    myFrame.pack();
    myFrame.setVisible(true);
}
} // End of RadioB
```

The `RadioB.java` application produces the screen shown in Figure 14.2.

## 14.7 Event Handling in C#

Event handling in C# (and in the other .NET languages) is similar to that of Java. .NET provides two approaches to creating GUIs in applications, the original Windows Forms and the more recent Windows Presentation Foundation. The latter is the more sophisticated and complex of the two. Because

```csharp
plain.CheckedChanged +=
    new EventHandler(rb_CheckedChanged);
```

Following is the `RadioB` example from Section 14.6 rewritten in C#. Once again, because our focus is on event handling, we do not explain all of the details of the program.

```csharp
// RadioB.cs
// An example to illustrate event handling with
//    interactive radio buttons that control the font
// style of a string of text

namespace RadioB {

    using System;
    using System.Drawing;
    using System.Windows.Forms;
    public class RadioB : Form {
        private Label text = new Label();
        private RadioButton plain = new RadioButton();
        private RadioButton bold = new RadioButton();
        private RadioButton italic = new RadioButton();
        private RadioButton boldItalic = new RadioButton();

        // Constructor for RadioB
        public RadioB() {

            // Initialize the attributes of the text and radio
            // buttons
            text.AutoSize = true;
            text.Text = "In what font style should I appear?";
            plain.Location = new Point(220, 0);
            plain.Text = "Plain";
            plain.Checked = true;
            bold.Location = new Point(350, 0);
            bold.Text = "Bold";
            italic.Location = new Point(480, 0);
            italic.Text = "Italics";
            boldItalic.Location = new Point(610, 0);
            boldItalic.Text = "Bold/Italics";

            // Add the text and the radio buttons to the form
            Controls.Add(text);
            Controls.Add(plain);
            Controls.Add(bold);
            Controls.Add(italic);
            Controls.Add(boldItalic);

            // Register the event handler for the radio buttons
            plain.CheckedChanged +=
                new EventHandler(rb_CheckedChanged);
```


Heavyweight components are more complex than lightweight components in general. A frame, for example, has multiple panes, which are responsible for various characteristics of the frame window. All visible elements of a Java interface are displayed in a frame’s content pane.

Generally, we can create a Java GUI-based application by creating a frame in which the program interface is displayed. The interface is often organized onto a primary panel, which is added to the frame’s content pane. The components in the primary panel are often organized using other panels as needed.

Containers are generally not useful unless they help us organize and display other components. Let’s examine another fundamental GUI component. A label is a component that displays a line of text in a GUI. A label can also display an image, a topic discussed later in this chapter. Usually, labels are used to display information or identify other components in the GUI. Labels can be found in almost every GUI-based program.

Let’s look at an example that uses frames, panels, and labels. When the program in Listing 3.7 is executed, a new window appears on the screen displaying a phrase. The text of the phrase is displayed using two label components. The labels are organized in a panel, and the panel is displayed in the content pane of the frame.

The JFrame constructor takes a string as a parameter, which it displays in the title bar of the frame. The call to the setDefaultCloseOperation method determines what will happen when the close button (the X) in the corner of the frame is clicked. In most cases we’ll simply let that button terminate the program, as indicated by the EXIT_ON_CLOSE constant.

A panel is created by instantiating the JPanel class. The background color of the panel is set using the setBackground method. The setPreferredSize method accepts a Dimension object as a parameter, which is used to indicate the width and height of the component in pixels. The size of many components can be set this way, and most also have setMinimumSize and setMaximumSize methods to help control the look of the interface.

The labels are created by instantiating the JLabel class, passing to its constructor the text of the label. In this program two separate label components are created.

Containers have an add method that allows other components to be added to them. Both labels are added to the primary panel and are from that point on considered to be part of that panel. The order in which components are added to a container often matters. In this case, it determines which label appears above the other.

Finally, the content pane of the frame is obtained using the getContentPane method, immediately after which the add method of the content pane is called to add the primary panel.

### LISTING 3.7

```java
//****************************************************************
// Authority.java      Author: Lewis/Loftus
//
// Demonstrates the use of frames, panels, and labels.
//****************************************************************

import java.awt.*;
import javax.swing.*;

public class Authority
{
    //-------------------------------------------------------------
    // Displays some words of wisdom.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Authority");

        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        JPanel primary = new JPanel();
        primary.setBackground (Color.yellow);
        primary.setPreferredSize (new Dimension(250, 75));

        JLabel label1 = new JLabel ("Question authority,");
        JLabel label2 = new JLabel ("but raise your hand first.");

        primary.add (label1);
        primary.add (label2);

        frame.getContentPane().add(primary);
        frame.pack();
        frame.setVisible(true);
    }
}
```

### DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_173_0.png)

- g. A component that displays a line of text in a GUI.
- h. Determines how the components in a container are arranged on the screen.

- SR 3.38 Run the Authority program. Describe what happens if you resize the frame by dragging the bottom-right corner towards the right. Explain.

- SR 3.39 Which of the following statements best describes how the GUI of the Authority program is constructed?

    - A frame is added to a panel, which is added to two labels.
    - Labels are added to a panel, which is added to the content pane of a frame.
    - Frames, panels, and labels are added to the foreground.
    - A panel displays two labels to the user.

- SR 3.40 What is the result of separately making each of the following changes to the Authority program? You may make the change, compile and run the program, and observe and report the results. Briefly explain what you observe.

    a. The dimensions passed to the setPreferredSize method are (300, 300) instead of (250, 75).

    b. The background color is set to black instead of yellow.

    c. The order of the two label instantiation statements is reversed (i.e., first you create label2 as a new JLabel, passing it the string "but raise your hand first.", and then you create label1 as a new JLabel, passing it the string "Question authority,").

    d. The order of the two primary add statements is reversed (i.e., first you add label2 to the primary panel, and then you add label1).

## 3.10 Nested Panels

In the previous section, we saw an example in which two labels were contained in a panel that was contained in a frame. Such relationships make up the containment hierarchy of an interface, which can be as intricate as needed to create the visual effect desired.

> KEY CONCEPT
> Panels can be nested to create an intricate containment hierarchy of components.

In particular, it is common to have multiple layers of nested panels to organize and group components in various ways. While you shouldn’t include unnecessary components in the containment hierarchy, don’t hesitate to include extra scaffolding in the creation of an interface to help achieve the effect you want.

The program in Listing 3.8, NestedPanels, creates two subpanels, each containing a label. Both subpanels are put onto another panel, which is then added to the content pane of the frame.

### LISTING 3.8

```java
//*************************************************
// NestedPanels.java    Author: Lewis/Loftus
//
// Demonstrates a basic component hierarchy.
//*************************************************

import java.awt.*;
import javax.swing.*;

public class NestedPanels
{
    //-------------------------------------------------
    // Presents two colored panels nested within a third.
    //-------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Nested Panels");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        // Set up first subpanel
        JPanel subPanel1 = new JPanel();
        subPanel1.setPreferredSize (new Dimension(150, 100));
        subPanel1.setBackground (Color.green);
        JLabel label1 = new JLabel ("One");
        subPanel1.add (label1);

        // Set up second subpanel
        JPanel subPanel2 = new JPanel();
        subPanel2.setPreferredSize (new Dimension(150, 100));
        subPanel2.setBackground (Color.red);
        JLabel label2 = new JLabel ("Two");
        subPanel2.add (label2);

        // Set up primary panel
        JPanel primary = new JPanel();
        primary.setBackground (Color.blue);
        primary.add (subPanel1);
        primary.add (subPanel2);

        frame.getContentPane().add(primary);
        frame.pack();
        frame.setVisible(true);
    }
}
```

### DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_177_0.png)

Note that the primary panel in the program was not explicitly sized. It sized itself as needed to accommodate the two panels contained in it. Also note that the subpanels have a buffer around them through which the blue of the primary panel can be seen. Such spacing is a function of the layout manager that is used to govern the container and the characteristics set for the components themselves. These issues are explored further in later Graphics Track sections.

As you did with the previous example, execute and experiment with this one. Resize the frame to see the effect on the components. Note that the size of the subpanels stays fixed, and that the orientation of the two panels changes depending on the width of the primary panel (which expands as the frame expands).

After you are comfortable with the way the components are laid out relative to each other, change the background color of all panels to the same color (say, green) to see how the distinction between panels can be invisible if the interface is designed accordingly.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 3.41 What is the containment hierarchy of a Java graphical user interface?
- SR 3.42 In the NestedPanels program, how many panels are created? What are the names of the panel variables?

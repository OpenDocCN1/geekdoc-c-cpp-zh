
## LISTING 7.22

```
//***************************************************************************
// GridPanel.java      Author: Lewis/Loftus
//
// Represents the panel in the LayoutDemo program that demonstrates
// the grid layout manager.
//***************************************************************************

import java.awt.*;
import javax.swing.*;

public class GridPanel extends JPanel
{
    //-------------------------------------------------------------
    // Sets up this panel with some buttons to show how grid
    // layout affects their position, shape, and size.
    //-------------------------------------------------------------
    public GridPanel()
    {
        setLayout (new GridLayout (2, 3));

        setBackground (Color.green);

        JButton b1 = new JButton ("BUTTON 1");
        JButton b2 = new JButton ("BUTTON 2");
        JButton b3 = new JButton ("BUTTON 3");
        JButton b4 = new JButton ("BUTTON 4");
        JButton b5 = new JButton ("BUTTON 5");

        add (b1);
        add (b2);
        add (b3);
        add (b4);
        add (b5);
    }
}
```

## LISTING 7.2.2 continued

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_388_0.png)

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_388_1.png)

By default, there are no horizontal and vertical gaps between the grid cells. The gap sizes can be specified using an overloaded constructor or with the appropriate GridLayout methods.

## Box Layout

A box layout organizes components either vertically or horizontally, in one row or one column, as shown in Figure 7.10. It is easy to use, yet when combined with other box layouts, it can produce complex GUI designs similar to those that can be accomplished with a GridBagLayout, which in general is far more difficult to master.

When a BoxLayout object is created, we specify that it will follow either the X axis (horizontal) or the Y axis (vertical), using constants defined in the BoxLayout class. Unlike other layout managers, the constructor of a BoxLayout takes as its

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_389_0.png)

## FIGURE 7.10 Box layout organizes components either vertically or horizontally

first parameter the component that it will govern. Therefore a new BoxLayout object must be created for each component. Listing 7.23 shows the panel used by the LayoutDemo program to demonstrate the box layout.

Components in containers governed by a box layout are organized (top to bottom or left to right) in the order in which they are added to the container.

There are no gaps between the components in a box layout. Unlike previous layout managers we’ve explored, a box layout does not have a specific vertical or horizontal gap that can be specified for the entire container. Instead, we can add invisible components to the container that take up space between other components. The Box class, which is also part of the Java standard class library, contains static methods that can be used to create these invisible components.

The two types of invisible components used in the BoxPanel class are rigid areas, which have a fixed size, and glue, which specifies where excess space in a container should go. A rigid area is created using the createRigidArea method of the Box class, and takes a Dimension object as a parameter to define the size of the invisible area. Glue is created using the createHorizontalGlue method or createVerticalGlue method, as appropriate.

Note that in our example, the space between buttons separated by a rigid area remains constant even when the container is resized. Glue, on the other hand, expands or contracts as needed to fill the space.

A box layout—more than most of the other layout managers—respects the alignments and the minimum, maximum, and preferred sizes of the components it governs. Therefore, setting the characteristics of the components that go into the container is another way to tailor the visual effect.

## LISTING 7.23

```
//***************************************************************************
// BoxPanel.java      Author: Lewis/Loftus
//
// Represents the panel in the LayoutDemo program that demonstrates
// the box layout manager.
//***************************************************************************

import java.awt.*;
import javax.swing.*;

public class BoxPanel extends JPanel
{
    //-------------------------------------------------------------
    // Sets up this panel with some buttons to show how a vertical
    // box layout (and invisible components) affects their position.
    //-------------------------------------------------------------
    public BoxPanel()
    {
        setLayout (new BoxLayout (this, BoxLayout.Y_AXIS));

        setBackground (Color.green);

        JButton b1 = new JButton ("BUTTON 1");
        JButton b2 = new JButton ("BUTTON 2");
        JButton b3 = new JButton ("BUTTON 3");
        JButton b4 = new JButton ("BUTTON 4");
        JButton b5 = new JButton ("BUTTON 5");

        add (b1);
        add (Box.createRigidArea (new Dimension (0, 10)));
        add (b2);
        add (Box.createVerticalGlue());
        add (b3);
        add (b4);
        add (Box.createRigidArea (new Dimension (0, 20)));
        add (b5);
    }
}
```

## LISTING 7.2.2 continued

## Layout Manager Demo

- Intro
- Flow
- Border
- Grid
- Box

- BUTTON 1
- BUTTON 2
- BUTTON 3
- BUTTON 4
- BUTTON 5

## Layout Manager Demo

- Intro
- Flow
- Border
- Grid
- Box

- BUTTON 1
- BUTTON 2

- BUTTON 3
- BUTTON 4
- BUTTON 5

## SELF-REVIEW QUESTIONS *(see answers in Appendix N)*

- SR 7.28  When is a layout manager consulted?
- SR 7.29  How does the flow layout manager behave?
- SR 7.30  Describe the areas of a border layout.
- SR 7.31  What effect does a glue component in a box layout have?

## 7.12 Borders

Java provides the ability to put a *border* around any Swing component. A border is not a component itself but rather defines how the edge of any component should be drawn and has an important effect on the design of a GUI. A border provides visual cues as to how GUI components are organized and can be used to give titles to components. Figure 7.11 lists the predefined borders in the Java standard class library.

The BorderFactory class is useful for creating borders for components. It has many methods for creating specific types of borders. A border is applied to a component by using the component’s setBorder method.

The program in Listing 7.24 demonstrates several types of borders. It simply creates several panels, sets a different border for each, and then displays them in a larger panel by using a grid layout.

> **KEY CONCEPT**
> 
> Borders can be applied to Swing components to group objects and focus attention.

| Border | Description |
|---|---|
| Empty Border | Puts buffering space around the edge of a component, but otherwise has no visual effect. |
| Line Border | A simple line surrounding the component. |
| Etched Border | Creates the effect of an etched groove around a component. |
| Bevel Border | Creates the effect of a component raised above the surface or sunken below it. |
| Titled Border | Includes a text title on or around the border. |
| Matte Border | Allows the size of each edge to be specified. Uses either a solid color or an image. |
| Compound Border | A combination of two borders. |

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_392_0.png)

## LISTING 7.24

```
p5.setBorder (BorderFactory.createTitledBorder ("Title"));
p5.add (new JLabel ("Titled Border"));
panel.add (p5);

JPanel p6 = new JPanel();
TitledBorder tb = BorderFactory.createTitledBorder ("Title");
tb.setTitleJustification (TitledBorder.RIGHT);
p6.setBorder (tb);
p6.add (new JLabel ("Titled Border (right)"));
panel.add (p6);

JPanel p7 = new JPanel();
Border b1 = BorderFactory.createLineBorder (Color.blue, 2);
Border b2 = BorderFactory.createEtchedBorder ();
p7.setBorder (BorderFactory.createCompoundBorder (b1, b2));
p7.add (new JLabel ("Compound Border"));
panel.add (p7);

JPanel p8 = new JPanel();
Border mb = BorderFactory.createMatteBorder (1, 5, 1, 1,
                                             Color.red);
p8.setBorder (mb);
p8.add (new JLabel ("Matte Border"));
panel.add (p8);

frame.getContentPane().add (panel);
frame.pack();
frame.setVisible(true);
}
}
```

Let’s look at each type of border created in this program. An *empty border* is applied to the larger panel that holds all the others, to create a buffer of space around the outer edge of the frame. The sizes of the top, left, bottom, and right edges of the empty border are specified in pixels. The *line border* is created using a particular color and specifies the line thickness in pixels (3 in this case). The line thickness defaults to 1 pixel if left unspecified. The *etched border* created in this program uses default colors for the highlight and shadow of the etching, but both could be explicitly set if desired.

A *bevel border* can be either raised or lowered. The default coloring is used in this program, although the coloring of each aspect of the bevel can be tailored as

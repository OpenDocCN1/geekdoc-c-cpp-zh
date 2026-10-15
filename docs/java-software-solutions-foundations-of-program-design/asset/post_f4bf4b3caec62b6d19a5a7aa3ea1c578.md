
# LISTING 5.15 *continued*

```java
italic = new JCheckBox ("Italic");
italic.setBackground (Color.cyan);

StyleListener listener = new StyleListener();
bold.addItemListener (listener);
italic.addItemListener (listener);

add (saying);
add (bold);
add (italic);

setBackground (Color.cyan);
setPreferredSize (new Dimension(300, 100));
}

/************************************************************
//  Represents the listener for both check boxes.
/************************************************************
private class StyleListener implements ItemListener
{
    //--------------------------------------------------------
    //  Updates the style of the label font style.
    //--------------------------------------------------------
    public void itemStateChanged (ItemEvent event)
    {
        int style = Font.PLAIN;

        if (bold.isSelected())
            style = Font.BOLD;

        if (italic.isSelected())
            style += Font.ITALIC;

        saying.setFont (new Font ("Helvetica", style, 36));
    }
}
```

This program also uses the Font class, which represents a particular *character font*. A Font object is defined by the font name, the font style, and the font size. The font name establishes the general visual characteristics of the characters. We are using the Helvetica font in this program. The style of a Java font can be plain,

bold, italic, or bold and italic combined. The check boxes in our GUI are set up to change the characteristics of our font style.

The style of a font is represented as an integer, and integer constants defined in the Font class are used to represent the various aspects of the style. The constant PLAIN is used to represent a plain style. The constants BOLD and ITALIC are used to represent bold and italic, respectively. The sum of the BOLD and ITALIC constants indicates a style that is both bold and italic.

The itemStateChanged method of the listener determines what the revised style should be now that one of the check boxes has changed state. It initially sets the style to be plain. Then each check box is consulted in turn using the isSelected method, which returns a boolean value. First, if the bold check box is selected (checked), then the style is set to bold. Then, if the italic check box is selected, the ITALIC constant is added to the style variable. Finally, the font of the label is set to a new font with its revised style.

Note that, given the way the listener is written in this program, it doesn’t matter which check box was clicked to generate the event. Both check boxes are processed by the same listener. It also doesn’t matter whether the changed check box was toggled from selected to unselected or vice versa. The state of both check boxes is examined if either is changed.

## Radio Buttons

A radio button is used with other radio buttons to provide a set of mutually exclusive options. Unlike a check box, a radio button is not particularly useful by itself. It has meaning only when it is used with one or more other radio buttons.

Only one option out of the group is valid. At any point in time, one and only one button of the group of radio buttons is selected (on). When a radio button from the group is pushed, the other button in the group that is currently on is automatically toggled off.

> KEY CONCEPT
> Radio buttons operate as a group, providing a set of mutually exclusive options.

The term “radio buttons” comes from the way the buttons worked on an old-fashioned car radio. At any point, one button was pushed to specify the current choice of station; when another was pushed, the current one automatically popped out.

The QuoteOptions program, shown in Listing 5.16, displays a label and a group of radio buttons. The radio buttons determine which quote is displayed in the label. Because only one of the quotes can be displayed at a time, the use of radio buttons is appropriate. For example, if the Comedy radio button is selected, the comedy quote is displayed in the label. If the Philosophy button is then pressed, the Comedy radio button is automatically toggled off and the comedy quote is replaced by a philosophical one.

VideoNote
Examples using check boxes and radio buttons.

## LISTING 5.16

```
//************************************************************************
//  QuoteOptions.java        Author: Lewis/Loftus
//
//  Demonstrates the use of radio buttons.
//************************************************************************

import javax.swing.JFrame;

public class QuoteOptions
{
    //------------------------------------------------------------
    // Creates and presents the program frame.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Quote Options");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        QuoteOptionsPanel panel = new QuoteOptionsPanel();
        frame.getContentPane().add (panel);

        frame.pack();
        frame.setVisible(true);
    }
}
```

## DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_283_0.png)

## 5.8 Check Boxes and Radio Buttons

The QuoteOptionsPanel class, shown in Listing 5.17, sets up and displays the GUI components. A radio button is represented by the JRadioButton class. Because the radio buttons in a set work together, the ButtonGroup class is used to define a set of related radio buttons.

Note that each button is added to the button group, and also that each button is added individually to the panel. A ButtonGroup object is not a container to organize and display components; it is simply a way to define the group of radio buttons that work together to form a set of dependent options. The ButtonGroup object ensures that the currently selected radio button is turned off when another in the group is selected.

A radio button produces an action event when it is selected. The actionPerformed method of the listener first retrieves the source of the event using the getSource method and then compares it to each of the three radio buttons in turn. Depending on which button was selected, the text of the label is set to the appropriate quote.

```java
//****************************** QuoteOptionsPanel.java ******************************
// QuoteOptionsPanel.java Author: Lewis/Loftus
// Demonstrates the use of radio buttons.
//******************************


import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class QuoteOptionsPanel extends JPanel
{
    private JLabel quote;
    private JRadioButton comedy, philosophy, carpentry;
    private String comedyQuote, philosophyQuote, carpentryQuote;

    //--------------------------------------------------
    // Sets up a panel with a label and a set of radio buttons
    // that control its text.
    //--------------------------------------------------
    public QuoteOptionsPanel()
    {
        comedyQuote = "Take my wife, please.";
        philosophyQuote = "I think, therefore I am.";
        carpentryQuote = "Measure twice. Cut once.";
    }
```

## LISTING 5.17 continued

```
quote = new JLabel (comedyQuote);
quote.setFont (new Font ("Helvetica", Font.BOLD, 24));

comedy = new JRadioButton ("Comedy", true);
comedy.setBackground (Color.green);
philosophy = new JRadioButton ("Philosophy");
philosophy.setBackground (Color.green);
carpentry = new JRadioButton ("Carpentry");
carpentry.setBackground (Color.green);

ButtonGroup group = new ButtonGroup();
group.add (comedy);
group.add (philosophy);
group.add (carpentry);

QuoteListener listener = new QuoteListener();
comedy.addActionListener (listener);
philosophy.addActionListener (listener);
carpentry.addActionListener (listener);

add (quote);
add (comedy);
add (philosophy);
add (carpentry);

setBackground (Color.green);
setPreferredSize (new Dimension(300, 100));
}

//**************************************************************
// Represents the listener for all radio buttons.
//**************************************************************
private class QuoteListener implements ActionListener
{
    //-------------------------------------------------------------
    // Sets the text of the label depending on which radio
    // button was pressed.
    //-------------------------------------------------------------
    public void actionPerformed (ActionEvent event)
    {
        Object source = event.getSource();
```

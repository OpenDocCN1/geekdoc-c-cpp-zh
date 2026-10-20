
JButton button3 is added next (lines 57–59). Both the weightx value and weighty value are set to zero, and the value of fill is BOTH. JButton button3 will grow if the window is resized—it’s affected by the weight values of button2. The weightx value for button2 is much larger than that for button3. When resizing occurs, button2 will occupy a larger percentage of the new space. The button is placed at row 1, column 2. One row and one column are occupied.

Both the JTextField textField (line 62) and JTextArea textArea2 (line 65) have a weightx value of 0 and a weighty value of 0. The value of fill is BOTH. The JTextField is placed at row 3, column 0, and the JTextArea at row 3, column 2. The JTextField occupies one row and two columns, the JTextArea one row and one column.

Method addComponent’s parameters are a Component reference component and integers row, column, width and height. Lines 72–73 set the GridBagConstraints variables gridx and gridy. The gridx variable is assigned the column in which the Component will be placed, and the gridy value is assigned the row in which the Component will be placed. Lines 74–75 set the GridBagConstraints variables gridwidth and gridheight. The gridwidth variable specifies the number of columns the Component will span in the grid, and the gridheight variable specifies the number of rows the Component will span in the grid. Line 76 sets the GridBagConstraints for a component in the GridBagLayout. Method setConstraints of class GridBagLayout takes a Component argument and a GridBagConstraints argument. Line 77 adds the component to the JFrame.

When you execute this application, try resizing the window to see how the constraints for each GUI component affect its position and size in the window.

## GridBagConstraints Constants RELATIVE and REMAINDER

Instead of gridx and gridy, a variation of GridBagLayout uses GridBagConstraints constants RELATIVE and REMAINDER. RELATIVE specifies that the next-to-last component in a particular row should be placed to the right of the previous component in the row. REMAINDER specifies that a component is the last component in a row. Any component that is not the second-to-last or last component on a row must specify values for GridBagConstraints variables gridwidth and gridheight. The application in Figs. 25.23–25.24 arranges components in GridBagLayout, using these constants.

```
// Fig. 25.23: GridBagFrame2.java
// Demonstrating GridBagLayout constants.
import java.awt.GridBagLayout;
import java.awt.GridBagConstraints;
import java.awt.Component;
import javax.swing.JFrame;
import javax.swing.JComboBox;
import javax.swing.JTextField;
import javax.swing.JList;
import javax.swing.JButton;

public class GridBagFrame2 extends JFrame
{
    private GridBagLayout layout; // layout of this frame
    private GridBagConstraints constraints; // constraints of this layout
```

Fig. 25.23 | GridBagConstraints constants RELATIVE and REMAINDER. (Part 1 of 3.)

```
16
17 // set up GUI
18 public GridBagFrame2()
19 {
20     super( "GridBagLayout" );
21     layout = new GridBagLayout();
22     setLayout( layout ); // set frame layout
23     constraints = new GridBagConstraints(); // instantiate constraints
24
25     // create GUI components
26     String[] metals = { "Copper", "Aluminum", "Silver" };
27     JComboBox comboBox = new JComboBox( metals );
28
29     JTextField textField = new JTextField( "TextField" );
30
31     String[] fonts = { "Serif", "Monospaced" };
32     JList list = new JList( fonts );
33
34     String[] names = { "zero", "one", "two", "three", "four" };
35     JButton[] buttons = new JButton[ names.length ];
36
37     for ( int count = 0; count < buttons.length; count++ )
38         buttons[ count ] = new JButton( names[ count ] );
39
40     // define GUI component constraints for textField
41     constraints.weightx = 1;
42     constraints.weighty = 1;
43     constraints.fill = GridBagConstraints.BOTH;
44     constraints.gridwidth = GridBagConstraints.REMAINDER;
45     addComponent( textField );
46
47     // buttons[0] -- weightx and weighty are 1: fill is BOTH
48     constraints.gridwidth = 1;
49     addComponent( buttons[ 0 ] );
50
51     // buttons[1] -- weightx and weighty are 1: fill is BOTH
52     constraints.gridwidth = GridBagConstraints.RELATIVE;
53     addComponent( buttons[ 1 ] );
54
55     // buttons[2] -- weightx and weighty are 1: fill is BOTH
56     constraints.gridwidth = GridBagConstraints.REMAINDER;
57     addComponent( buttons[ 2 ] );
58
59     // comboBox -- weightx is 1: fill is BOTH
60     constraints.weighty = 0;
61     constraints.gridwidth = GridBagConstraints.REMAINDER;
62     addComponent( comboBox );
63
64     // buttons[3] -- weightx is 1: fill is BOTH
65     constraints.weighty = 1;
66     constraints.gridwidth = GridBagConstraints.REMAINDER;
67     addComponent( buttons[ 3 ] );
68
```

```
69    // buttons[4] -- weightx and weighty are 1: fill is BOTH
70    constraints.gridwidth = GridBagConstraints.RELATIVE;
71    addComponent( buttons[ 4 ] );
72
73    // list -- weightx and weighty are 1: fill is BOTH
74    constraints.gridwidth = GridBagConstraints.REMAINDER;
75    addComponent( list );
76 } // end GridBagFrame2 constructor
77
78    // add a component to the container
79    private void addComponent( Component component )
80    {
81        layout.setConstraints( component, constraints );
82        add( component ); // add component
83    } // end method addComponent
84 } // end class GridBagFrame2
```

## Fig. 25.23 | GridBagConstraints constants RELATIVE and REMAINDER. (Part 3 of 3.)

```
1  // Fig. 25.24: GridBagDemo2.java
2  // Demonstrating GridBagLayout constants.
3  import javax.swing.JFrame;
4
5  public class GridBagDemo2
6  {
7      public static void main( String[] args )
8      {
9          GridBagFrame2 gridBagFrame = new GridBagFrame2();
10         gridBagFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
11         gridBagFrame.setSize( 300, 200 ); // set frame size
12         gridBagFrame.setVisible( true ); // display frame
13     } // end main
14  } // end class GridBagDemo2
```

![](img/009e962758dcc71dbc43a493362e6dc0_1076_0.png)

## Fig. 25.24 | Test class for GridBagDemo2.

Lines 21–22 create a GridBagLayout and use it to set the JFrame’s layout manager. The components that are placed in GridBagLayout are created in lines 27–38—they are a JComboBox, a JTextField, a JList and five JButtons.

The JTextField is added first (lines 41–45). The weightx and weighty values are set to 1. The fill variable is set to BOTH. Line 44 specifies that the JTextField is the last component on the line. The JTextField is added to the content pane with a call to our utility method addComponent (declared at lines 79–83). Method addComponent takes a Component argument and uses GridBagLayout method setConstraints to set the constraints for the Component. Method add attaches the component to the content pane.

JButton buttons[ 0 ] (lines 48–49) has weightx and weighty values of 1. The fill variable is BOTH. Because buttons[ 0 ] is not one of the last two components on the row, it’s given a gridwidth of 1 and so will occupy one column. The JButton is added to the content pane with a call to utility method addComponent.

JButton buttons[ 1 ] (lines 52–53) has weightx and weighty values of 1. The fill variable is BOTH. Line 52 specifies that the JButton is to be placed relative to the previous component. The Button is added to the JFrame with a call to addComponent.

JButton buttons[ 2 ] (lines 56–57) has weightx and weighty values of 1. The fill variable is BOTH. This JButton is the last component on the line, so REMAINDER is used. The JButton is added to the content pane with a call to addComponent.

The JComboBox (lines 60–62) has a weightx of 1 and a weighty of 0. The JComboBox will not grow vertically. The JComboBox is the only component on the line, so REMAINDER is used. The JComboBox is added to the content pane with a call to addComponent.

JButton buttons[ 3 ] (lines 65–67) has weightx and weighty values of 1. The fill variable is BOTH. This JButton is the only component on the line, so REMAINDER is used. The JButton is added to the content pane with a call to addComponent.

JButton buttons[ 4 ] (lines 70–71) has weightx and weighty values of 1. The fill variable is BOTH. This JButton is the next-to-last component on the line, so RELATIVE is used. The JButton is added to the content pane with a call to addComponent.

The JList (lines 74–75) has weightx and weighty values of 1. The fill variable is BOTH. The JList is added to the content pane with a call to addComponent.

## 25.10 Wrap-Up

This chapter completes our introduction to GUIs. In this chapter, we discussed additional GUI topics, such as menus, sliders, pop-up menus, multiple-document interfaces, tabbed panes and Java’s pluggable look-and-feel. All these components can be added to existing applications to make them easier to use and understand. We also presented additional layout managers for organizing and sizing GUI components. In the next chapter, you’ll learn about multithreading, which allows you to specify that an application should perform multiple tasks at once.

## Summary

## Section 25.2 JSlider

- JSliders enable you to select from a range of integer values. They can display major and minor tick marks, and labels for the tick marks (p. 1001). They also support snap-to ticks (p. 1001)—positioning the thumb (p. 1001) between two tick marks causes snaps it to the closest tick mark.

- JSliders (p. 1001) have either horizontal or vertical orientation. For a horizontal JSlider, the minimum value is at the extreme left and the maximum value at the extreme right. For a vertical JSlider, the minimum value is at the extreme bottom and the maximum value at the extreme top. The position of the thumb indicates the current value of the JSlider. Method getValue (p. 1005) of class JSlider returns the current thumb position.

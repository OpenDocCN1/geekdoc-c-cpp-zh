
event-dispatch thread) for each lightweight component as the GUI is displayed. For paintComponent to be called again, an event must occur (such as covering and uncovering the component with another window).

If you need paintComponent to execute (i.e., if you want to update the graphics drawn on a Swing component), you can call method repaint, which is inherited by all JComponents indirectly from class Component (package java.awt). The header for repaint is

```
public void repaint()
```

## 15.3 Color Control

Class Color declares methods and constants for manipulating colors in a Java program. The predeclar ed color constants are summarized in Fig. 15.3, and several color methods and constructors are summarized in Fig. 15.4. Two of the methods in Fig. 15.4 are Graphics methods that are specific to colors.

| Color constant | RGB value |
|---|---|
| public final static Color RED | 255, 0, 0 |
| public final static Color GREEN | 0, 255, 0 |
| public final static Color BLUE | 0, 0, 255 |
| public final static Color ORANGE | 255, 200, 0 |
| public final static Color PINK | 255, 175, 175 |
| public final static Color CYAN | 0, 255, 255 |
| public final static Color MAGENTA | 255, 0, 255 |
| public final static Color YELLOW | 255, 255, 0 |
| public final static Color BLACK | 0, 0, 0 |
| public final static Color WHITE | 255, 255, 255 |
| public final static Color GRAY | 128, 128, 128 |
| public final static Color LIGHT_GRAY | 192, 192, 192 |
| public final static Color DARK_GRAY | 64, 64, 64 |

Fig. 15.3 | Color constants and their RGB values.

| Method | Description |
|---|---|
| Color constructors and methods | |
| public Color( int r, int g, int b ) | Creates a color based on red, green and blue components expressed as integers from 0 to 255. |
| public Color( float r, float g, float b ) | Creates a color based on red, green and blue components expressed as floating-point values from 0.0 to 1.0. |

Fig. 15.4 | Color methods and color-related Graphics methods. (Part 1 of 2.)

| Method | Description |
|---|---|
| public int getRed() | Returns a value between 0 and 255 representing the red content. |
| public int getGreen() | Returns a value between 0 and 255 representing the green content. |
| public int getBlue() | Returns a value between 0 and 255 representing the blue content. |
| *Graphics methods for manipulating Colors* | |
| public Color getColor() | Returns Color object representing current color for the graphics context. |
| public void setColor( Color c ) | Sets the current color for drawing with the graphics context. |

Fig. 15.4 | Color methods and color-related Graphics methods. (Part 2 of 2.)

Every color is created from a red, a green and a blue component. Together these components are called RGB values. All three RGB components can be integers in the range from 0 to 255, or all three can be floating-point values in the range 0.0 to 1.0. The first RGB component specifies the amount of red, the second the amount of green and the third the amount of blue. The larger the RGB value, the greater the amount of that particular color. Java enables you to choose from 256 × 256 × 256 (approximately 16.7 million) colors. Not all computers are capable of displaying all these colors. The computer will display the closest color it can.

Two of class Color’s constructors are shown in Fig. 15.4—one that takes three int arguments and one that takes three float arguments, with each argument specifying the amount of red, green and blue. The int values must be in the range 0–255 and the float values in the range 0.0–1.0. The new Color object will have the specified amounts of red, green and blue. Color methods getRed, getGreen and getBlue return integer values from 0 to 255 representing the amounts of red, green and blue, respectively. Graphics method getColor returns a Color object representing the current drawing color. Graphics method setColor sets the current drawing color.

## Drawing in Different Colors

Figures 15.5–15.6 demonstrate several methods from Fig. 15.4 by drawing filled rectangles and Strings in several different colors. When the application begins execution, class ColorJPanel’s paintComponent method (lines 10–37 of Fig. 15.5) is called to paint the window. Line 17 uses Graphics method setColor to set the drawing color. Method setColor receives a Color object. The expression new Color( 255, 0, 0 ) creates a new Color object that represents red (red value 255, and 0 for the green and blue values). Line 18 uses Graphics method fillRect to draw a filled rectangle in the current color. Method fillRect draws a rectangle based on its four arguments. The first two integer values represent the upper-left x-coordinate and upper-left y-coordinate, where the Graphics object begins drawing the rectangle. The third and fourth arguments are nonnegative integers that

Line 19 (Fig. 15.5) uses Graphics method drawString to draw a String in the current color. The expression g.getColor() retrieves the current color from the Graphics object. We then concatenate the Color with string "Current RGB: ", resulting in an implicit call to class Color's toString method. The String representation of a Color contains the class name and package (java.awt.Color) and the red, green and blue values.

## Look-and-Feel Observation 15.1

People perceive colors differently. Choose your colors carefully to ensure that your application is readable, both for people who can perceive color and for those who are color blind. Try to avoid using many different colors in close proximity.

Lines 22–24 and 27–29 perform the same tasks again. Line 22 uses the Color constructor with three float arguments to create a dark green color (0.50f for red, 0.75f for green and 0.0f for blue). Note the syntax of the values. The letter f appended to a floating-point literal indicates that the literal should be treated as type float. Recall that by default, floating-point literals are treated as type double.

Line 27 sets the current drawing color to one of the predeclared Color constants (Color.BLUE). The Color constants are static, so they're created when class Color is loaded into memory at execution time.

The statement in lines 35–36 makes calls to Color methods getRed, getGreen and getBlue on the predeclared Color.MAGENTA constant. Method main of class ShowColors (lines 8–18 of Fig. 15.6) creates the JFrame that will contain a ColorJPanel object where the colors will be displayed.

// execute application
public static void main( String[] args )
{
    // create frame for ColorJPanel
    JFrame frame = new JFrame( "Using colors" );
    frame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );

    ColorJPanel colorJPanel = new ColorJPanel(); // create ColorJPanel
    frame.add( colorJPanel ); // add colorJPanel to frame
    frame.setSize( 400, 180 ); // set frame size
    frame.setVisible( true ); // display frame
} // end main
} // end class ShowColors

![](img/009e962758dcc71dbc43a493362e6dc0_675_0.png)

Fig. 15.6 | Creating JFrame to display colors on JPanel. (Part 2 of 2.)

![](img/009e962758dcc71dbc43a493362e6dc0_676_0.png)

## Software Engineering Observation 15.1

To change the color, you must create a new Color object (or use one of the predeclared Color constants). Like String objects, Color objects are immutable (not modifiable).

Package javax.swing provides the JColorChooser GUI component that enables application users to select colors. The application of Figs. 15.7–15.8 demonstrates a JColorChooser dialog. When you click the Change Color button, a JColorChooser dialog appears. When you select a color and press the dialog’s OK button, the background color of the application window changes.

// Fig. 15.7: ShowColors2JFrame.java
// Choosing colors with JColorChooser.
import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JColorChooser;
import javax.swing.JPanel;

public class ShowColors2JFrame extends JFrame
{
    private JButton changeColorJButton;
    private Color color = Color.LIGHT_GRAY;
    private JPanel colorJPanel;

    // set up GUI
    public ShowColors2JFrame()
    {
        super( "Using JColorChooser" );

        // create JPanel for display color
        colorJPanel = new JPanel();
        colorJPanel.setBackground( color );

        // set up changeColorJButton and register its event handler
        changeColorJButton = new JButton( "Change Color" );
        changeColorJButton.addActionListener(

            new ActionListener() // anonymous inner class
            {
                // display JColorChooser when user clicks button
                public void actionPerformed( ActionEvent event )
                {
                    color = JColorChooser.showDialog(
                        ShowColors2JFrame.this, "Choose a color", color );

                    // set default color, if no color is returned
                    if ( color == null )
                        color = Color.LIGHT_GRAY;



42
43        // change content pane's background color
44        colorJPanel.setBackground( color );
45    } // end method actionPerformed
46    } // end anonymous inner class
47 ); // end call to addActionListener
49    add( colorJPanel, BorderLayout.CENTER ); // add colorJPanel
50    add( changeColorJButton, BorderLayout.SOUTH ); // add button
52    setSize( 400, 130 ); // set frame size
53    setVisible( true ); // display frame
54    } // end ShowColor2JFrame constructor
55 } // end class ShowColors2JFrame

Fig. 15.7 | JColorChooser dialog. (Part 2 of 2.)

1  // Fig. 15.8: ShowColors2.java
2  // Choosing colors with JColorChooser.
3  import javax.swing.JFrame;
5  public class ShowColors2
6  {
7      // execute application
8      public static void main( String[] args )
9      {
10         ShowColors2JFrame application = new ShowColors2JFrame();
11         application.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
12     } // end main
13  } // end class ShowColors2

(a) Initial application window

(b) JColorChooser window

![](img/009e962758dcc71dbc43a493362e6dc0_677_0.png)

![](img/009e962758dcc71dbc43a493362e6dc0_677_1.png)

Select a color from one of the color swatches

(c) Application window after changing JPanel's background color

![](img/009e962758dcc71dbc43a493362e6dc0_677_2.png)

Fig. 15.8 | Choosing colors with JColorChooser.

Class JColorChooser provides static method showDialog, which creates a JColorChooser object, attaches it to a dialog box and displays the dialog. Lines 36–37 of Fig. 15.7 invoke this method to display the color chooser dialog. Method showDialog returns the selected Color object, or null if the user presses Cancel or closes the dialog without pressing OK. The method takes three arguments—a reference to its parent Component, a String to display in the title bar of the dialog and the initial selected Color for the dialog. The parent component is a reference to the window from which the dialog is displayed (in this case the JFrame, with the reference name frame). The dialog will be centered on the parent. If the parent is null, the dialog is centered on the screen. While the color chooser dialog is on the screen, the user cannot interact with the parent component until the dialog is dismissed. This type of dialog is called a modal dialog.

After the user selects a color, lines 40–41 determine whether color is null, and, if so, set color to Color.LIGHT_GRAY. Line 44 invokes method setBackground to change the background color of the JPanel. Method setBackground is one of the many Component methods that can be used on most GUI components. The user can continue to use the Change Color button to change the background color of the application. Figure 15.8 contains method main, which executes the program.

Figure 15.8(b) shows the default JColorChooser dialog that allows the user to select a color from a variety of color swatches. There are three tabs across the top of the dialog—Swatches, HSB and RGB. These represent three different ways to select a color. The HSB tab allows you to select a color based on hue, saturation and brightness—values that are used to define the amount of light in a color. We do not discuss HSB values. For more information on them, visit en.wikipedia.org/wiki/HSL_and_HSV. The RGB tab allows you to select a color by using sliders to select the red, green and blue components. The HSB and RGB tabs are shown in Fig. 15.9.

![](img/009e962758dcc71dbc43a493362e6dc0_678_0.png)

Fig. 15.9 | HSB and RGB tabs of the JColorChooser dialog. (Part 1 of 2.)

## 15.4 Manipulating Fonts

This section introduces methods and constants for manipulating fonts. Most font methods and font constants are part of class Font. Some methods of class Font and class Graphics are summarized in Fig. 15.10.

Fig. 15.9 | HSB and RGB tabs of the JColorChooser dialog. (Part 2 of 2.)

Fig. 15.10 | Font-related methods and constants. (Part 1 of 2.)

| Method or constant | Description |
|---|---|
| Font constants, constructors and methods | |
| public final static int PLAIN | A constant representing a plain font style. |
| public final static int BOLD | A constant representing a bold font style. |
| public final static int ITALIC | A constant representing an italic font style. |
| public Font( String name, int style, int size ) | Creates a Font object with the specified font name, style and size. |
| public int getStyle() | Returns an int indicating the current font style. |
| public int getSize() | Returns an int indicating the current font size. |
| public String getName() | Returns the current font name as a string. |
| public String getFamily() | Returns the font's family name as a string. |
| public boolean isPlain() | Returns true if the font is plain, else false. |
| public boolean isBold() | Returns true if the font is bold, else false. |
| public boolean isItalic() | Returns true if the font is italic, else false. |

![](img/009e962758dcc71dbc43a493362e6dc0_679_0.png)

| Method or constant | Description |
|---|---|
| *Graphics methods for manipulating Fonts* |  |
| `public Font getFont()` | Returns a Font object reference representing the current font. |
| `public void setFont( Font f )` | Sets the current font to the font, style and size specified by the Font object reference f. |

Fig. 15.10 | Font-related methods and constants. (Part 2 of 2.)

Class Font’s constructor takes three arguments—the font name, font style and font size. The font name is any font currently supported by the system on which the program is running, such as standard Java fonts Monospaced, SansSerif and Serif. The font style is Font.PLAIN, Font.ITALIC or Font.BOLD (each is a static field of class Font). Font styles can be used in combination (e.g., Font.ITALIC + Font.BOLD). The font size is measured in points. A point is 1/72 of an inch. Graphics method setFont sets the current drawing font—the font in which text will be displayed—to its Font argument.

> **Portability Tip 15.2**
> *The number of fonts varies across systems. Java provides five font names—Serif, Monospaced, SansSerif, Dialog and DialogInput—that can be used on all Java platforms. The Java runtime environment (JRE) on each platform maps these logical font names to actual fonts installed on the platform. The actual fonts used may vary by platform.*

The application of Figs. 15.11–15.12 displays text in four different fonts, with each font in a different size. Figure 15.11 uses the Font constructor to initialize Font objects (in lines 16, 20, 24 and 29) that are each passed to Graphics method setFont to change the drawing font. Each call to the Font constructor passes a font name (Serif, Monospaced or SansSerif) as a string, a font style (Font.PLAIN, Font.ITALIC or Font.BOLD) and a font size. Once Graphics method setFont is invoked, all text displayed following the call will appear in the new font until the font is changed. Each font’s information is displayed in lines 17, 21, 25 and 30–31 using method drawString. The coordinates passed to drawString corresponds to the lower-left corner of the baseline of the font. Line 28 changes the drawing color to red, so the next string displayed appears in red. Lines 30–31 display information about the final Font object. Method getFont of class Graphics returns a Font object representing the current font. Method getName returns the current font name as a string. Method getSize returns the font size in points.

> **Software Engineering Observation 15.2**
> *To change the font, you must create a new Font object. Font objects are immutable—class Font has no set methods to change the characteristics of the current font.*

Figure 15.12 contains the main method, which creates a JFrame to display a FontJPanel. We add a FontJPanel object to this JFrame (line 15), which displays the graphics created in Fig. 15.11.

// Fig. 15.11: FontJPanel.java
// Display strings in different fonts and colors.
import java.awt.Font;
import java.awt.Color;
import java.awt.Graphics;
import javax.swing.JPanel;

public class FontJPanel extends JPanel
{
    // display Strings in different fonts and colors
    public void paintComponent( Graphics g )
    {
        super.paintComponent( g ); // call superclass's paintComponent

        // set font to Serif (Times), bold, 12pt and draw a string
        g.setFont( new Font( "Serif", Font.BOLD, 12 ) );
        g.drawString( "Serif 12 point bold.", 20, 30 );

        // set font to Monospaced (Courier), italic, 24pt and draw a string
        g.setFont( new Font( "Monospaced", Font.ITALIC, 24 ) );
        g.drawString( "Monospaced 24 point italic.", 20, 50 );

        // set font to SansSerif (Helvetica), plain, 14pt and draw a string
        g.setFont( new Font( "SansSerif", Font.PLAIN, 14 ) );
        g.drawString( "SansSerif 14 point plain.", 20, 70 );

        // set font to Serif (Times), bold/italic, 18pt and draw a string
        g.setColor( Color.RED );
        g.setFont( new Font( "Serif", Font.BOLD + Font.ITALIC, 18 ) );
        g.drawString( g.getFont().getName() + " " + g.getFont().getSize() + " point bold italic.", 20, 90 );
    } // end method paintComponent
} // end class FontJPanel

Fig. 15.11 | Graphics method setFont changes the drawing font.

// Fig. 15.12: Fonts.java
// Using fonts.
import javax.swing.JFrame;

public class Fonts
{
    // execute application
    public static void main( String[] args )
    {
        // create frame for FontJPanel
        JFrame frame = new JFrame( "Using fonts" );
        frame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );

        FontJPanel fontJPanel = new FontJPanel(); // create FontJPanel
        frame.add( fontJPanel ); // add fontJPanel to frame

Fig. 15.12 | Creating a JFrame to display fonts. (Part 1 of 2.)

```
// Fig. 23.6: WelcomeApplet.java
// Applet that draws a String.
import java.awt.Graphics;  // program uses class Graphics
import javax.swing.JApplet; // program uses class JApplet

public class WelcomeApplet extends JApplet
{
    // draw text on applet's background
    public void paint( Graphics g )
    {
        // call superclass version of method paint
        super.paint( g );

        // draw a String at x-coordinate 25 and y-coordinate 25
        g.drawString( "Welcome to Java Programming!", 25, 25 );
    } // end method paint
} // end class WelcomeApplet
```

WelcomeApplet executing in the appletviewer

Upper-left corner of drawing area is location (0, 0). Drawing area extends from below the Applet menu to above the status bar. x-coordinates increase from left to right. y-coordinates increase from top to bottom.

Applet menu

Status bar mimics what would be displayed in the browser's status bar as the applet loads and begins executing

Pixel coordinate (25, 25) at which the string is displayed

WelcomeApplet executing in Mozilla Firefox

Upper-left corner of drawing area

Pixel coordinate (25, 25)

# Fig. 23.6 | Applet that draws a String.

# Creating the Applet Class

Line 3 imports class Graphics to enable the applet to draw graphics, such as lines, rectangles, ovals and strings of characters. Class JApplet (imported at line 4) from package javax.swing is used to create applets. As with applications, every Java applet contains at least one public class declaration. An applet container can create only objects of classes that are public and extend JApplet (or its superclass Applet). For this reason, class WelcomeApplet (lines 6–17) extends JApplet.
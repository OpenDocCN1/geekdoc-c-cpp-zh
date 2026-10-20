Line 25 of Fig. 15.29 casts the Graphics reference received by paintComponent to a Graphics2D reference and assigns it to g2d to allow access to the Java 2D features.

```
// Fig. 15.29: ShapesJPanel.java
// Demonstrating some Java 2D shapes.
import java.awt.Color;
import java.awt.Graphics;
import java.awt.BasicStroke;
import java.awt.GradientPaint;
import java.awt.TexturePaint;
import java.awt.Rectangle;
import java.awt.Graphics2D;
import java.awt.geom.Ellipse2D;
import java.awt.geom.Rectangle2D;
import java.awt.geom.RoundRectangle2D;
import java.awt.geom.Arc2D;
import java.awt.geom.Line2D;
import java.awt.image.BufferedImage;
import javax.swing.JPanel;

public class ShapesJPanel extends JPanel
{
    // draw shapes with Java 2D API
    public void paintComponent( Graphics g )
    {
        super.paintComponent( g ); // call superclass's paintComponent

        Graphics2D g2d = ( Graphics2D ) g; // cast g to Graphics2D

        // draw 2D ellipse filled with a blue-yellow gradient
        g2d.setPaint( new GradientPaint( 5, 30, Color.BLUE, 35, 100, Color.YELLOW, true ) );
        g2d.fill( new Ellipse2D.Double( 5, 30, 65, 100 ) );

        // draw 2D rectangle in red
        g2d.setPaint( Color.RED );
        g2d.setStroke( new BasicStroke( 10.0f ) );
        g2d.draw( new Rectangle2D.Double( 80, 30, 65, 100 ) );

        // draw 2D rounded rectangle with a buffered background
        BufferedImage buffImage = new BufferedImage( 10, 10, BufferedImage.TYPE_INT_RGB );

        // obtain Graphics2D from buffImage and draw on it
        Graphics2D gg = buffImage.createGraphics();
        gg.setColor( Color.YELLOW ); // draw in yellow
        gg.fillRect( 0, 0, 10, 10 ); // draw a filled rectangle
        gg.setColor( Color.BLACK ); // draw in black
        gg.drawRect( 1, 1, 6, 6 ); // draw a rectangle
        gg.setColor( Color.BLUE ); // draw in blue
        gg.fillRect( 1, 1, 3, 3 ); // draw a filled rectangle
        gg.setColor( Color.RED ); // draw in red
```
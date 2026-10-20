# Error-Prevention Tip 14.1

In a JComponent subclass’s paintComponent method, the first statement should always call the superclass’s paintComponent method to ensure that an object of the subclass displays correctly.

# Common Programming Error 14.5

If an overridden paintComponent method does not call the superclass’s version, the subclass component may not display properly. If an overridden paintComponent method calls the superclass’s version after other drawing is performed, the drawing will be erased.

# Defining the Custom Drawing Area

The Painter application of Figs. 14.34–14.35 demonstrates a customized subclass of JPanel that is used to create a dedicated drawing area. The application uses the mouseDragged event handler to create a simple drawing application. The user can draw pictures by dragging the mouse on the JPanel. This example does not use method mouseMoved, so our event-listener class (the anonymous inner class at lines 22–34) extends MouseMotionAdapter. Since this class already declares both mouseMoved and mouseDragged, we can simply override mouseDragged to provide the event handling this application requires.

```
// Fig. 14.34: PaintPanel.java
// Using class MouseMotionAdapter.
import java.awt.Point;
import java.awt.Graphics;
import java.awt.event.MouseEvent;
import java.awt.event.MouseMotionAdapter;
import javax.swing.JPanel;

public class PaintPanel extends JPanel
{
    private int pointCount = 0; // count number of points

    // array of 10000 java.awt.Point references
    private Point[] points = new Point[ 10000 ];

    // set up GUI and register mouse event handler
    public PaintPanel()
    {
        // handle frame mouse motion event
        addMouseMotionListener(

            new MouseMotionAdapter() // anonymous inner class
            {
                // store drag coordinates and repaint
                public void mouseDragged( MouseEvent event )
                {
                    if ( pointCount < points.length )
                    {

```
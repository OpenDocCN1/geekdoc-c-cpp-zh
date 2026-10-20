Figure 7.25 begins with the usual import statements for creating drawings (lines 3–5). Lines 10–11 declare and create two new color constants—VIOLET and INDIGO. As you may know, the colors of a rainbow are red, orange, yellow, green, blue, indigo and violet. Java has predefined constants only for the first five colors. Lines 15–17 initialize an array with the colors of the rainbow, starting with the innermost arcs first. The array begins with two Color.WHITE elements, which, as you’ll soon see, are for drawing the empty arcs at the center of the rainbow. The instance variables can be initialized when they’re declared, as shown in lines 10–17. The constructor (lines 20–23) contains a single statement that calls method setBackground (which is inherited from class JPanel) with the parameter Color.WHITE. Method setBackground takes a single Color argument and sets the background of the component to that color.

```
// Fig. 7.25: DrawRainbow.java
// Demonstrates using colors in an array.
import java.awt.Color;
import java.awt.Graphics;
import javax.swing.JPanel;

public class DrawRainbow extends JPanel
{
    // define indigo and violet
    private final static Color VIOLET = new Color( 128, 0, 128 );
    private final static Color INDIGO = new Color( 75, 0, 130 );

    // colors to use in the rainbow, starting from the innermost
    // The two white entries result in an empty arc in the center
    private Color[] colors =
        { Color.WHITE, Color.WHITE, VIOLET, INDIGO, Color.BLUE,
          Color.GREEN, Color.YELLOW, Color.ORANGE, Color.RED };

    // constructor
    public DrawRainbow()
    {
        setBackground( Color.WHITE ); // set the background to white
    } // end DrawRainbow constructor

    // draws a rainbow using concentric arcs
    public void paintComponent( Graphics g )
    {
        super.paintComponent( g );

        int radius = 20; // radius of an arc

        // draw the rainbow near the bottom-center
        int centerX = getWidth() / 2;
        int centerY = getHeight() - 10;

        // draws filled arcs starting with the outermost
        for ( int counter = colors.length; counter > 0; counter-- )
        {
```
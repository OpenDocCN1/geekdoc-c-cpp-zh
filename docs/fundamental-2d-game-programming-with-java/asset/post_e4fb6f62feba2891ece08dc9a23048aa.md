
## TEXT

The first time I tried to draw some text on the screen for the frame-per-second, it was easy. But for those of you who have noticed, all of the text drawing has hard-coded values, such as the following code:

```
// draw directions on top of bouncing balls
super.render( g );
g.drawString( "Ball Count: " + ballCount, 20, 35 );
g.drawString( "Press [SPACE] to launch.", 20, 50 );
g.drawString( "Press Up arrow to increase ball count", 20, 65 );
g.drawString( "Press Down arrow to decrease ball count", 20, 80 );
```

If the font size changes, the hard-coded numbers for the height no longer work. But placing text in a specific position is harder than it seems.

## UNDERSTANDING JAVA FONTS

To create a new font in Java, three parameters are passed to the constructor: the font name, style, and size.

```
Font( String name, int style, int size )
```

The font name is a string with the name of the font, such as Courier New. You can obtain a list of all available fonts from the GraphicsEnvironment object.

```
public static void main( String[] args ) {
GraphicsEnvironment ge =
GraphicsEnvironment.getLocalGraphicsEnvironment();
String[] fontFamilies = ge.getAvailableFontFamilyNames();
for( String fontFamily : fontFamilies ) {
 System.out.println( fontFamily );
 }
}
```

The size of the font is the point size, such as 12 for a twelve-point font. The style can be plain, bold, italic, or bold and italic, which is obtained by combining the bold and italic with the OR | operator.

```
Font plain = new Font( "Name", Font.PLAIN, 12 );
Font bold = new Font( "Name", Font.BOLD, 12 );
Font italic = new Font( "Name", Font.ITALIC, 12 );
Font boldItalic = new Font( "Name", Font.BOLD | Font.ITALIC, 12 );
```

Remember, before you get the width and height of the current font, you must create the font object and set it in the Graphics object.

The BoxedTextProblem example code, shown in Figure 11.1 and located in the javagames.text package, shows the differences between drawing text and images to the screen by trying to draw a rectangle around some text.

```
package javagames.text;

import java.awt.Color;
import java.awt.Font;
import java.awt.Graphics;
import javagames.util.SimpleFramework;

public class BoxedTextProblem extends SimpleFramework {
 public BoxedTextProblem() {
 appWidth = 640;
 appHeight = 640;
 appSleep = 10L;
 appTitle = "Boxed Text Problem";
 appBackground = Color.WHITE;
 appFPSColor = Color.BLACK;
 }
}
@Override
protected void initialize() {
 super.initialize();
 }

@Override
protected void render( Graphics g ) {
    super.render( g );

    // Box this text...
    g.setColor( Color.BLACK );
    String box = "great Java, now what?";
    Font font = new Font( "Arial", Font.PLAIN, 24 );
    g.setFont( font );
    g.drawString( box, 20, 50 );
    g.setColor( Color.RED );
    g.drawRect( 20, 50, 200, 20 );
}

public static void main( String[] args ) {
    launchApp( new BoxedTextProblem() );
}
}
```

Ignore that the width of the rectangle is just a guess. Even though both the rectangle and text are drawn with their upper-left position at (20, 50), the results are not similar. See Figure 11.1.

![](img/588a4cda8f2acae94a7e1987bf99400d_337_0.png)

### Figure 11.1 Boxed Text Problem. © 2014 Timothy Wright.

The problem is that text is not treated the same as images. Although images are drawn from the upper-left corner, text is drawn from the baseline, and the height and width of the rendered string depends on the selected font type, style, and size.

![](img/588a4cda8f2acae94a7e1987bf99400d_338_0.png)

### Figure 11.2
Text Metrics.
© 2014 Timothy Wright.

The baseline runs across the bottom of the font. However, some letters will drop below the baseline. The ascent value rises from the baseline to the top of the font. The descent value is the distance letters drop below the baseline, and the leading value is the space between lines so that the letters do not touch. Together, these three values form the total height of the font. See Figure 11.2.

Height = ascent + descent + leading

As with most problems in Java, there are multiple ways to solve this problem.

![](img/588a4cda8f2acae94a7e1987bf99400d_338_1.png)

### Figure 11.3
Boxed Text Solution.
© 2014 Timothy Wright.

The BoxedTextSolution code, as shown in Figure 11.3 and located in the javagames.text package, demonstrates the necessary steps to place a border around some text without guessing at the values. The first step is to get the FontMetrics from the Graphics object.

```
FontMetrics fm = g.getFontMetrics();
```

Because some fonts have a different width for each letter, you need the string value to determine the width.

```
int width = fm.stringWidth(str);
```

Now that the width of the string is available, the next step is to draw the text so that the upper-left corner is not placed at the baseline, but remains the upper-left corner. Because the starting point is drawn at the baseline, adding the ascent, which is the distance the text rises from the y coordinate, places the text in the correct position.

```
g.drawString(str, x, y + fm.getAscent());
```

A line can now be drawn using the upper-left position because the text is shifted by the ascent value. All that is left is to calculate the height of the font.

```
int height = fm.getAscent() + fm.getDescent() + fm.getLeading();
```

With the upper-left position, the height, the width, and the text drawn in the correct spot, placing a box around the text is easy. The BoxedTextSolution steps through the necessary method calls to place a box around some text. Correctly boxing text is essential to placing game text exactly where it is needed.

```
package javagames.text;

import java.awt.*;
import javagames.util.SimpleFramework;

public class BoxedTextSolution extends SimpleFramework {
    public BoxedTextSolution() {
        appWidth = 640;
        appHeight = 640;
        appSleep = 10L;
        appTitle = "Boxed Text Solution";
        appBackground = Color.WHITE;
        appFPSColor = Color.BLACK;
    }

    @Override
    protected void initialize() {
        super.initialize();
    }

    @Override
    protected void render( Graphics g ) {
        super.render( g );

        // Set the font...
        Font font = new Font( "Arial", Font.PLAIN, 24 );
        g.setFont( font );
        FontMetrics fm = g.getFontMetrics();
        int x = 20;
        int y = 50;
        // Draw the top...
        String str = "draw the top line";
        g.setColor( Color.DARK_GRAY );
        g.drawString( str, x, y );
        int width = 100;
        g.setColor( Color.RED );
        g.drawLine( x, y, x + width, y );
        // Calculate the string width...
        y += 40;
        str = "Calculate correct width";
        g.setColor( Color.DARK_GRAY );
        g.drawString( str, x, y );
        width = fm.stringWidth( str );
        g.setColor( Color.GREEN );
        g.drawLine( x, y, x + width, y );
        // Use Ascent to offset y
        y += 40;
        g.setColor( Color.DARK_GRAY );
        str = "offset text with the Ascent";
        g.drawString( str, x, y + fm.getAscent() );
        width = fm.stringWidth( str );
        g.setColor( Color.BLUE );
        g.drawLine( x, y, x + width, y );
        // Ascent+Descent+Leading=Height
        y += 40;
        g.setColor( Color.DARK_GRAY );
        str = "Calculate height of font";
        g.drawString( str, x, y + fm.getAscent() );
        width = fm.stringWidth( str );
        g.setColor( Color.BLUE );
        g.drawLine( x, y, x + width, y );
        int height = fm.getAscent() + fm.getDescent() + fm.getLeading();
        g.drawLine( x, y + height, x + width, y + height );
        // Box the text
        y += 40;
        g.setColor( Color.DARK_GRAY );
        str = "Groovy, we got it!!!";
        g.drawString( str, x, y + fm.getAscent() );
        width = fm.stringWidth(str);
        g.setColor(Color.BLUE);
        height = fm.getAscent() + fm.getDescent() + fm.getLeading();
        g.drawRect(x, y, width, height);
    }
    public static void main(String[] args) {
        launchApp(new BoxedTextSolution());
    }
}
```

## MAKING A DRAW STRING UTILITY

Now that you can determine the placement of text based on the font size, you can add some utility methods to the Utility class, located in the javagames.util package. Given a starting position and an array of strings, the utility methods draw the text to the screen with the correct spacing, keeping the starting position in the upper-left corner.

```
public class Utility {
    // previous code here
    public static int drawString(Graphics g, int x, int y, String str) {
        return drawString(g, x, y, new String[]{ str });
    }
    public static int drawString(
        Graphics g, int x, int y, List<String> str) {
        return drawString(g, x, y, str.toArray(new String[0]));
    }
    public static int drawString(
        Graphics g, int x, int y, String... str) {
        FontMetrics fm = g.getFontMetrics();
        int height = fm.getAscent() + fm.getDescent() + fm.getLeading();
        for (String s : str) {
            g.drawString(s, x, y + fm.getAscent());
            y += height;
        }
        return y;
    }
}
```

Notice that the new methods return the new y position once the text is drawn. This allows more text to be appended to the previously drawn text. Using the new utility methods, the following code can be added to the SimpleFramework, located in the javagames.util package.

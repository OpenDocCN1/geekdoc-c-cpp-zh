
### NOTE:

The fill method paints one fewer pixel to the right and the bottom. For example, if you draw a new `Rectangle2D.Double(0, 0, 10, 20)`, then the drawing includes the pixels with x = 10 and y = 20. If you fill the same rectangle, those pixels are not painted.

Define colors with the Color class. The java.awt.Color class offers predefined constants for the following 13 standard colors:

```
BLACK, BLUE, CYAN, DARK_GRAY, GRAY, GREEN, LIGHT_GRAY,
MAGENTA, ORANGE, PINK, RED, WHITE, YELLOW
```

You can specify a custom color by creating a Color object by its red, green, and blue components, each a value between 0 and 255:

```java
g2.setPaint(new Color(0, 128, 128)); // a dull blue-green
g2.drawString("Welcome!", 75, 125);
```

### NOTE:

In addition to solid colors, you can call setPaint with instances of classes that implement the Paint interface. This enables drawing with gradients and textures.

To set the *background* color, use the setBackground method of the Component class, an ancestor of JComponent.

```java
var component = new MyComponent();
component.setBackground(Color.PINK);
```

There is also a `setForeground` method. It specifies the default color that is used for drawing on the component.

### **java.awt.Color** 1.0

- `Color(int r, int g, int b)`  
  creates a color object with the given red, green, and blue components between 0 and 255.

### **java.awt.Graphics2D** 1.2

- `Paint getPaint()`
- `void setPaint(Paint p)`  
  gets or sets the paint property of this graphics context. The Color class implements the Paint interface. Therefore, you can use this method to set the paint attribute to a solid color.
- `void fill(Shape s)`  
  fills the shape with the current paint.

### **java.awt.Component** 1.0

- `Color getForeground()`
- `Color getBackground()`
- `void setForeground(Color c)`
- `void setBackground(Color c)`  
  gets or sets the foreground or background color.

## 10.3.3 Using Fonts

The “Not a Hello World” program at the beginning of this chapter displayed a string in the default font. Sometimes, you will want to show your text in a different font. You can specify a font by its *font face name*. A font face name is composed of a *font family name*, such as “Helvetica”, and an optional suffix such as “Bold”. For example, the font faces “Helvetica” and “Helvetica Bold” are both considered to be part of the family named “Helvetica.”

To find out which fonts are available on a particular computer, call the `getAvailableFontFamilyNames` method of the `GraphicsEnvironment` class. The method returns an array of strings containing the names of all available fonts. To obtain an instance of the `GraphicsEnvironment` class that describes the graphics environment of the user’s system, use the static `getLocalGraphicsEnvironment` method. The following program prints the names of all fonts on your system:

```java
import java.awt.*;
public class ListFonts
{
    public static void main(String[] args)
    {
        String[] fontNames = GraphicsEnvironment
            .getLocalGraphicsEnvironment()
            .getAvailableFontFamilyNames();
        for (String fontName : fontNames)
            System.out.println(fontName);
    }
}
```

The AWT defines five *logical* font names:

- SansSerif
- Serif
- Monospaced
- Dialog
- DialogInput

These names are always mapped to some fonts that actually exist on the client machine. For example, on a Windows system, SansSerif is mapped to Arial.

In addition, the Oracle JDK always includes three font families named “Lucida Sans,” “Lucida Bright,” and “Lucida Sans Typewriter.”

To draw characters in a font, you must first create an object of the class `Font`. Specify the font face name, the font style, and the point size. Here is an example of how you construct a Font object:

```java
var sansbold14 = new Font("SansSerif", Font.BOLD, 14);
```

The third argument is the point size. Points are commonly used in typography to indicate the size of a font. There are 72 points per inch.

You can use a logical font name in place of the font face name in the `Font` constructor. Specify the style (plain, **bold**, *italic*, or ***bold italic***) by setting the second Font constructor argument to one of the following values:

- `Font.PLAIN`
- `Font.BOLD`
- `Font.ITALIC`
- `Font.BOLD + Font.ITALIC`

The font is plain with a font size of 1 point. Use the `deriveFont` method to get a font of the desired size:

```java
Font f = f1.deriveFont(14.0F);
```

![](img/0e7b74ef51a065c077b42cd87b362288_856_0.png)

### CAUTION:

There are two overloaded versions of the deriveFont method. One of them (with a float parameter) sets the font size, the other (with an int parameter) sets the font style. Thus, `f1.deriveFont(14)` sets the style and not the size! (The result is an *italic* font because it happens that the binary representation of 14 has the ITALIC bit but not the BOLD bit set.)

Here's the code that displays the string "Hello, World!" in the standard sans serif font on your system, using 14-point bold type:

```java
var sansbold14 = new Font("SansSerif", Font.BOLD, 14);
g2.setFont(sansbold14);
var message = "Hello, World!";
g2.drawString(message, 75, 100);
```

Next, let's *center* the string in its component instead of drawing it at an arbitrary position. We need to know the width and height of the string in pixels. These dimensions depend on three factors:

- The font used (in our case, sans serif, bold, 14 point);
- The string (in our case, "Hello, World!"); and
- The device on which the font is drawn (in our case, the user's screen).

To obtain an object that represents the font characteristics of the screen device, call the `getFontRenderContext` method of the `Graphics2D` class. It returns an object of the `FontRenderContext` class. Simply pass that object to the `getStringBounds` method of the `Font` class:

```java
FontRenderContext context = g2.getFontRenderContext();
Rectangle2D bounds = sansbold14.getStringBounds(message, context);
```

The `getStringBounds` method returns a rectangle that encloses the string.

To interpret the dimensions of that rectangle, you should know some basic typesetting terms (see Figure 10.9). The *baseline* is the imaginary line where, for example, the bottom of a character like 'e' rests. The *ascent* is the distance from the baseline to the top of an *ascender*, which is the upper part of a letter like 'b' or 'k', or an uppercase character. The *descent* is the distance from the baseline to a *descender*, which is the lower portion of a letter like ‘p’ or ‘g’.

![](img/0e7b74ef51a065c077b42cd87b362288_858_0.png)

**Figure 10.9** Typesetting terms illustrated

*Leading* is the space between the descent of one line and the ascent of the next line. (The term has its origin from the strips of lead that typesetters used to separate lines.) The *height* of a font is the distance between successive baselines, which is the same as descent + leading + ascent.

The width of the rectangle that the `getStringBounds` method returns is the horizontal extent of the string. The height of the rectangle is the sum of ascent, descent, and leading. The rectangle has its origin at the baseline of the string. The top y coordinate of the rectangle is negative. Thus, you can obtain string width, height, and ascent as follows:

```java
double stringWidth = bounds.getWidth();
double stringHeight = bounds.getHeight();
double ascent = -bounds.getY();
```

If you need to know the descent or leading, use the `getLineMetrics` method of the Font class. That method returns an object of the `LineMetrics` class, which has methods to obtain the descent and leading:

```java
LineMetrics metrics = f.getLineMetrics(message, context);
float descent = metrics.getDescent();
float leading = metrics.getLeading();
```

```java
6  import javax.swing.*;
7
8  /**
9   * @version 1.35 2018-04-10
10  * @author Cay Horstmann
11  */
12 public class FontTest
13 {
14    public static void main(String[] args)
15    {
16       EventQueue.invokeLater(() ->
17          {
18             var frame = new FontFrame();
19             frame.setTitle("FontTest");
20             frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
21             frame.setVisible(true);
22          });
23    }
24 }
25
26 /**
27  * A frame with a text message component.
28  */
29 class FontFrame extends JFrame
30 {
31    public FontFrame()
32    {
33       add(new FontComponent());
34       pack();
35    }
36 }
37
38 /**
39  * A component that shows a centered message in a box.
40  */
41 class FontComponent extends JComponent
42 {
43    private static final int DEFAULT_WIDTH = 300;
```

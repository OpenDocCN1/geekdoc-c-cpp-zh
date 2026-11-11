# Listing 3.12 `write/RectangleComponent.java`

```
```java
package write;

import java.awt.*;
import java.awt.geom.*;
import java.util.*;
import javax.swing.*;
import javax.xml.parsers.*;
import javax.xml.stream.*;
import org.w3c.dom.*;

/**
 * A component that shows a set of colored rectangles.
 */
public class RectangleComponent extends JComponent
{
    private static final Dimension PREFERRED_SIZE = new Dimension(300, 200);

    private java.util.List<Rectangle2D> rects;
    private java.util.List<Color> colors;
    private Random generator;
    private DocumentBuilder builder;

    public RectangleComponent()
    {
        rects = new ArrayList<>();
        colors = new ArrayList<>();
        generator = new Random();

        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        factory.setNamespaceAware(true);
        try
        {
            builder = factory.newDocumentBuilder();
        }
        catch (ParserConfigurationException e)
        {
            e.printStackTrace();
        }
    }

    /**
     * Create a new random drawing.
     */
    public void newDrawing()
    {
```
```
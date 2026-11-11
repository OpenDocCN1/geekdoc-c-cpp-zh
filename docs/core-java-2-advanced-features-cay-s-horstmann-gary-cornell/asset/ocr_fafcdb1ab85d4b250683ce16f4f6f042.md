# **Listing 11.11** *(Continued)*

```
```java
38    FontRenderContext context = g2.getFontRenderContext();
39    Font f = new Font("Serif", Font.PLAIN, 72);
40    GeneralPath clipShape = new GeneralPath();
41
42    TextLayout layout = new TextLayout("Hello", f, context);
43    AffineTransform transform = AffineTransform.getTranslateInstance(0, 72);
44    Shape outline = layout.getOutline(transform);
45    clipShape.append(outline, false);
46
47    layout = new TextLayout("World", f, context);
48    transform = AffineTransform.getTranslateInstance(0, 144);
49    outline = layout.getOutline(transform);
50    clipShape.append(outline, false);
51
52    g2.draw(clipShape);
53    g2.clip(clipShape);
54
55    final int NLINES = 50;
56    Point2D p = new Point2D.Double(0, 0);
57    for (int i = 0; i < NLINES; i++)
58    {
59       double x = (2 * getWidth() * i) / NLINES;
60       double y = (2 * getHeight() * (NLINES - 1 - i)) / NLINES;
61       Point2D q = new Point2D.Double(x, y);
62       g2.draw(new Line2D.Double(p, q));
63    }
64
65
66    public Dimension getPreferredSize() { return PREFERRED_SIZE; }
67 }
```
```

# **java.awt.print.Printable 1.2**

+   - **int print(Graphics g, PageFormat format, int pageNumber)**
+     renders a page and returns PAGE_EXISTS, or returns NO_SUCH_PAGE.
+   - **Parameters:**
+     - **g**: The graphics context onto which the page is rendered
+     - **format**: The format of the page to draw on
+     - **pageNumber**: The number of the requested page
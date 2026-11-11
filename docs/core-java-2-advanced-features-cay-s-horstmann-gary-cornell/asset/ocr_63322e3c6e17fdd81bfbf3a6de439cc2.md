# Listing 11.13 *(Continued)*

```
```java
/**
 * Constructs a banner.
 * @param m the message string
 */
public Banner(String m)
{
    message = m;
}

/**
 * Gets the page count of this section.
 * @param g2 the graphics context
 * @param pf the page format
 * @return the number of pages needed
 */
public int getPageCount(Graphics2D g2, PageFormat pf)
{
    if (message.equals("")) return 0;
    FontRenderContext context = g2.getFontRenderContext();
    Font f = new Font("Serif", Font.PLAIN, 72);
    Rectangle2D bounds = f.getStringBounds(message, context);
    scale = pf.getImageableHeight() / bounds.getHeight();
    double width = scale * bounds.getWidth();
    int pages = (int) Math.ceil(width / pf.getImageableWidth());
    return pages;
}

public int print(Graphics g, PageFormat pf, int page) throws PrinterException
{
    Graphics2D g2 = (Graphics2D) g;
    if (page > getPageCount(g2, pf)) return Printable.NO_SUCH_PAGE;
    g2.translate(pf.getImageableX(), pf.getImageableY());

    drawPage(g2, pf, page);
    return Printable.PAGE_EXISTS;
}

public void drawPage(Graphics2D g2, PageFormat pf, int page)
{
    if (message.equals("")) return;
    page--; // account for cover page

    drawCropMarks(g2, pf);
    g2.clip(new Rectangle2D.Double(0, 0, pf.getImageableWidth(), pf.getImageableHeight()));
    g2.translate(-page * pf.getImageableWidth(), 0);
    g2.scale(scale, scale);
    FontRenderContext context = g2.getFontRenderContext();
```
```
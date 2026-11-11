```
```java
/**
 * Removes a square from the collection.
 * @param s the square to remove
 */
public void remove(Rectangle2D s)
{
    if (s == null) return;
    if (s == current) current = null;
    squares.remove(s);
    repaint();
}

private class MouseHandler extends MouseAdapter
{
    public void mousePressed(MouseEvent event)
    {
        // add a new square if the cursor isn't inside a square
        current = find(event.getPoint());
        if (current == null) add(event.getPoint());
    }

    public void mouseClicked(MouseEvent event)
    {
        // remove the current square if double clicked
        current = find(event.getPoint());
        if (current != null && event.getClickCount() >= 2) remove(current);
    }
}

private class MouseMotionHandler implements MouseMotionListener
{
    public void mouseMoved(MouseEvent event)
    {
        // set the mouse cursor to cross hairs if it is inside a rectangle

        if (find(event.getPoint()) == null) setCursor(Cursor.getDefaultCursor());
        else setCursor(Cursor.getPredefinedCursor(Cursor.CROSSHAIR_CURSOR));
    }

    public void mouseDragged(MouseEvent event)
    {
        if (current != null)
        {
            int x = event.getX();
            int y = event.getY();

            // drag the current rectangle to center it at (x, y)
```
```
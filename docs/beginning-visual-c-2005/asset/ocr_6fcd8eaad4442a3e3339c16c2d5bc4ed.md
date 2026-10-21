# Creating the Document and Improving the View

The problem you have with rectangles is that the element classes all assume the mapping mode is MM_TEXT, and in MM_LOENGLISH the rectangles are upside-down because of the reversal of the y axis. When you apply LPtoDP() to a rectangle, it is assumed to be oriented properly with respect to the MM_LOENGLISH axes. Because yours are not, the function mirrors the rectangles in the x axis. This creates a problem when you call InvalidateRect() to invalidate an area of a view because the mirrored rectangle in device coordinates is not recognized by Windows as being inside the visible client area.

You have two options for dealing with this. You can modify the element classes so that the enclosing rectangles are the right way up for MM_LOENGLISH, or you can re-normalize the rectangle that you intend to pass to the InvalidateRect() function. The latter is the easiest course because you only need to modify one member of the view class, OnUpdate():

```
```cpp
void CSketcherView::OnUpdate(CView* pSender, LPARAM lHint, Object* pHint)
{
    // Invalidate the area corresponding to the element pointed to
    // if there is one, otherwise invalidate the whole client area
    if(pHint)
    {
        CClientDC aDC(this);  // Create a device context
        OnPrepareDC(&aDC);  // Get origin adjusted
        // Get the enclosing rectangle and convert to client coordinates
        CRect aRect = ((CEElement*)pHint)->GetBoundRect();
        aDC.LPtoDP(&aRect);
        aRect.NormalizeRect();
        InvalidateRect(aRect);  // Get the area redrawn
    }
    else
        InvalidateRect(0);
}
```
```

That should do it for the program as it stands. If you rebuild Sketcher, you should have scrolling working, with support for multiple views. You’ll need to remember to re-normalize any rectangle that you convert to device coordinates for use with InvalidateRect() in the future. Any reverse conversions are also affected.

# Deleting and Moving Shapes

Being able to delete shapes is a fundamental requirement in a drawing program. One question relating to this is how you’re going to select the element you want to delete. Of course, after you decide how to select an element, this applies equally well if you want to move an element, so you can treat moving and deleting elements as related problems. But first consider how you’re going to bring move and delete operations into the program.

A neat way of providing move and delete functions would be to have a pop-up context menu appear at the cursor position when you click the right mouse button. You could then put Move and Delete as items on the menu. A pop-up that works like this is a very handy facility that you can use in lots of different situations.
# Creating the Document and Improving the View

RectVisible(), which checks whether a rectangle that you supply to it as an argument overlaps the area that Windows requires to be redrawn. You can use this to make sure you only draw the elements that are in the area Windows wants redrawn, thus improving the performance of the application:

```
void CSketcherView::OnDraw(CDC* pDC)
{
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    if(!pDoc)
        return;

    POSITION aPos = pDoc->GetListHeadPosition();
    CElement* pElement = 0;             // Store for an element pointer
    while(aPos)                         // Loop while aPos is not null
    {
        pElement = pDoc->GetNext(aPos); // Get the current element pointer
        // If the element is visible...
        if(pDC->RectVisible(pElement->GetBoundRect()))
            pElement->Draw(pDC);        // ...draw it
    }
}
```

You get the position for the first entry in the list and store it in aPos. You use the value stored in aPos to control the while loop that retrieves each pointer entry in turn so the loop continues until aPos is NULL. You retrieve the bounding rectangle for each element using the GetBoundRect() member of the object and pass it to the RectVisible() function in the if statement. As a result, only elements that overlap the area that Windows has identified as invalid are drawn. Drawing on the screen is a relatively expensive operation in terms of time, so checking for just the elements that need to be redrawn, rather than drawing everything each time, improves performance considerably.

# Adding an Element to the Document

The last thing you need to do to have a working document in our program is to add the code to the OnLButtonUp() handler in the CSketcherView class to add the temporary element to the document:

```
void CSketcherView::OnLButtonUp(UINT nFlags, CPoint point)
{
    if(this == GetCapture())
        ReleaseCapture();        // Stop capturing mouse messages

    // If there is an element, add it to the document
    if(m_pTempElement)
    {
        GetDocument()->AddElement(m_pTempElement);
        InvalidateRect(0);        // Redraw the current window
        m_pTempElement = 0;       // Reset the element pointer
    }
}
```

Of course, you must check that there really is an element before you add it to the document. The user might just have clicked the left mouse button without moving the mouse. After adding the element to the list in the document, you call InvalidateRect() to get the client area for the current view redrawn.
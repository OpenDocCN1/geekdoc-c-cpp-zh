
# Chapter 15

The argument of 0 invalidates the whole of the client area in the view. Because of the way the rubberbanding process works, some elements may not be displayed properly if you don’t do this. If you draw a horizontal line, for instance, and then rubberband a rectangle with the same color so that its top or bottom edge overlaps the line, the overlapped bit of line disappears. This is because the edge being drawn is XORed with the line underneath, so you get the background color back. You also reset the pointer m_pTempElement to avoid confusion when another element is created.

## Exercising the Document

After saving all the modified files, you can build the latest version of Sketcher and execute it. You’ll now be able to produce art such as “the happy programmer” shown in Figure 15-8.

![](img/2359b0c604600c58fba3539c738a356e_825_0.png)

Figure 15-8

The program is now working more realistically. It stores a pointer to each element in the document object, so they’re all automatically redrawn as necessary. The program also does a proper cleanup of the document data when it’s deleted.

There are still some limitations in the program that you can address. For instance:

- You can open another view window by using the Window > New Window menu option in the program. This capability is built in to an MDI application and opens a new view to an existing document, not a new document. If you draw in one window, however, the elements are not drawn in the other window. Elements never appear in windows other than the one where they were drawn, unless the area they occupy needs to be redrawn for some other reason.
- You can only draw in the client area you can see. It would be nice to be able to scroll the view and draw over a bigger area.
- Neither can you delete an element, so if you make a mistake, you either live with it or start over with a new document.

These are all quite serious deficiencies that, together, make the program fairly useless as it stands. You’ll overcome all of them before the end of this chapter.

## Improving the View

The first item that you can try to fix is the updating of all the document windows that are displayed when an element is drawn. The problem arises because only the view in which an element is drawn knows about the new element. Each view is acting independently of the others and there is no communication between them. You need to arrange for any view that adds an element to the document to let all the other views know about it, and they need to take the appropriate action.

### Updating Multiple Views

The document class conveniently contains a function UpdateAllViews() to help with this particular problem. This function essentially provides a means for the document to send a message to all its views. You just need to call it from the OnLButtonUp() function in the CSketcherView class, whenever you have added a new element to the document:

```
void CSketcherView::OnLButtonUp(UINT nFlags, CPoint point)
{
    if(this == GetCapture())
        ReleaseCapture();                // Stop capturing mouse messages

    // If there is an element, add it to the document
    if(m_pTempElement)
    {
        GetDocument()->AddElement(m_pTempElement);
        GetDocument()->UpdateAllViews(0,0,m_pTempElement);  // Tell all the views
        m_pTempElement = 0;                // Reset the element pointer
    }
}
```

When the m_pTempElement pointer is not NULL, the specific action of the function has been extended to call the UpdateAllViews() member of your document class. This function communicates with the views by causing the OnUpdate() member function in each view to be called. The three arguments to UpdateAllViews() are described in Figure 15-9.

The first argument to the UpdateAllViews() function call is often the this pointer for the current view. This suppresses the call of the OnUpdate() function for the current view. This is a useful feature when the current view is already up to date. In the case of Sketcher, because you are rubber-banding you want to get the current view redrawn as well, so by specifying the first argument as 0 you get the OnUpdate() function called for all the views, including the current view. This removes the need to call InvalidateRect() as you did before.

You don’t use the second argument to UpdateAllViews() here, but you do pass the pointer to the new element through the third argument. Passing a pointer to the new element allows the views to figure out which bit of their client area needs to be redrawn.

![](img/2359b0c604600c58fba3539c738a356e_827_0.png)

# Figure 15-9

To catch the information passed to the UpdateAllViews() function, you add the OnUpdate() member function to the view class. You can do this from the Class wizard and looking at the properties for CSketcherView. As I’m sure you recall, you display the properties for a class by right-clicking the class name and selecting Properties from the pop-up. If you click the Overrides button in the Properties window, you’ll be able to find OnUpdate in the list of functions you can override. Click the function name, then the <Add> OnUpdate option that shows in the drop-down list in the adjacent column. If you close the Properties window, you’ll be able to edit the code for the OnUpdate() override you have added in the Editor pane. You only need to add the highlighted code below to the function definition:

```
void CSketcherView::OnUpdate(CView* pSender, LPARAM lHint, CObject* pHint)
{
    // Invalidate the area corresponding to the element pointed to
    // if there is one, otherwise invalidate the whole client area
    if(pHint)
        InvalidateRect(((CElement*)pHint)->GetBoundRect());
    else
        InvalidateRect(0);
}
```

Note that you must uncomment the parameter names in the generated version of the function; otherwise, it won’t compile with the additional code here. The three arguments passed to the OnUpdate() function in the view class correspond to the arguments that you passed in the UpdateAllViews() function call. Thus, pHint contains the address of the new element. However, you can’t assume that this is

always the case. The OnUpdate() function is also called when a view is first created, but with a NULL pointer for the third argument. Therefore, the function checks that the pHint pointer isn’t NULL and only then gets the bounding rectangle for the element passed as the third argument. It invalidates this area in the client area of the view by passing the rectangle to the InvalidateRect() function. This area is redrawn by the OnDraw() function in this view when the next WM_PAINT message is sent to the view. If the pHint pointer is NULL, the whole client area is invalidated.

You might be tempted to consider redrawing the new element in the OnUpdate() function. This isn’t a good idea. You should only do permanent drawing in response to the Windows WM_PAINT message. This means that the OnDraw() function in the view should be the only place that’s initiating any drawing operations for document data. This ensures that the view is drawn correctly whenever Windows deems it necessary.

If you build and execute Sketcher with the new modifications included, you should find that all the views are updated to reflect the contents of the document.

## Scrolling Views

Adding scrolling to a view looks remarkably easy at first sight; the water is in fact deeper and murkier that it at first appears, but jump in anyway. The first step is to change the base class for CSketcherView from CView to CScrollView. This new base class has the scrolling functionality built in, so you can alter the definition of the CSketcherView class to:

```
class CSketcherView: public CScrollView
{
    // Class definition as before...
};
```

You must also modify two lines of code at the beginning of the SketcherView.cpp file which refer to the base class for CSketcherView. You need to replace CView with CScrollView as the base class:

```
IMPLEMENT_DYNCREATE(CSketcherView, CScrollView)

BEGIN_MESSAGE_MAP(CSketcherView, CScrollView)
```

However, this is still not quite enough. The new version of the view class needs to know some things about the area you are drawing on, such as the size and how far the view is to be scrolled when you use the scroller. This information has to be supplied before the view is first drawn. You can put the code to do this in the OnInitialUpdate() function in the view class.

You supply the information that is required by calling a function that is inherited from the CScrollView class: SetScrollSizes(). The arguments to this function are explained in Figure 15-10.

Scrolling a distance of one line occurs when you click on the up or down arrow on the scroll bar; a page scroll occurs when you click on the scrollbar itself. You have an opportunity to change the mapping mode here. MM_LOENGLISH would be a good choice for the Sketcher application, but first get scrolling working with the MM_TEXT mapping mode because there are still some difficulties to be uncovered.

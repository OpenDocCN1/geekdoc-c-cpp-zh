always the case. The OnUpdate() function is also called when a view is first created, but with a NULL pointer for the third argument. Therefore, the function checks that the pHint pointer isn’t NULL and only then gets the bounding rectangle for the element passed as the third argument. It invalidates this area in the client area of the view by passing the rectangle to the InvalidateRect() function. This area is redrawn by the OnDraw() function in this view when the next WM_PAINT message is sent to the view. If the pHint pointer is NULL, the whole client area is invalidated.

You might be tempted to consider redrawing the new element in the OnUpdate() function. This isn’t a good idea. You should only do permanent drawing in response to the Windows WM_PAINT message. This means that the OnDraw() function in the view should be the only place that’s initiating any drawing operations for document data. This ensures that the view is drawn correctly whenever Windows deems it necessary.

If you build and execute Sketcher with the new modifications included, you should find that all the views are updated to reflect the contents of the document.

# Scrolling Views

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
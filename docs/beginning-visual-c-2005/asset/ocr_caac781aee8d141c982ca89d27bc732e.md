only look at the ones you’re going to use in the Sketcher program here in this chapter and go into others as you need them later on.

Note that MFC includes some more specialized classes for graphics output that are derived from CDC. For example, you be using objects of CClientDC because it is derived from CDC and contains all the members we will discuss at this point. The advantage that CClientDC has over CDC is that it always contains a device context that represents only the client area of a window, and this is precisely what you want in most circumstances.

# Displaying Graphics

In a device context, you draw entities such as lines, circles, and text relative to a current position. A current position is a point in the client area that was set either by the previous entity that was drawn, or by calling a function to set it. For example, you could extend the OnDraw() function to set the current position as follows:

```
void CSketcherView::OnDraw(CDC* pDC)
{
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    if (!pDoc)
        return;

    pDC->MoveTo(50, 50);    // Set the current position as 50,50
}
```

The shaded line calls the MoveTo() function for the CDC object pointed to by pDC. This member function simply sets the current position to the x and y coordinates you specify as arguments. As you saw earlier, the default mapping mode is MM_TEXT, so the coordinates are in pixels and the current position will be set to a point 50 pixels from the inside left border of the window, and 50 pixels down from the top of the client area.

The CDC class overloads the MoveTo() function to provide flexibility over how you specify the position that you want to set as the current position. There are two versions of the function, declared in the CDC class as:

```
CPoint MoveTo(int x, int y);    // Move to position x,y
CPoint MoveTo(POINT aPoint);    // Move to position defined by aPoint
```

The first version accepts the x and y coordinates as separate arguments. The second accepts one argument of type POINT, which is a structure defined as:

```
typedef struct tagPOINT
{
    LONG x;
    LONG y;
} POINT;
```

The coordinates are members of the struct and are of type LONG (which is type defined in the Windows API corresponding to a 32-bit signed integer). You may prefer to use a class instead of a structure, in which case you can use objects of the class CPoint anywhere that a POINT object can be used. The class CPoint has data members x and y of type LONG, and using CPoint objects has the advantage that the
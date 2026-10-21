
## Defining the CCurve Class

When you move the cursor while drawing a curve, you’re not creating a sequence of new curves but rather extending the same curve, so each successive point adds another segment to the curve’s definition. You therefore need to create a curve object as soon as you have the two points from the WM_LBUTTONDOWN message and the first WM_MOUSEMOVE message. Points defined with subsequent mouse move messages then define additional segments to the existing curve object. You’ll need to add a function, AddSegment(), to the CCurve class to extend the curve once it has been created by the constructor.

A further point to consider is how you are to calculate the enclosing rectangle. This is defined by getting the minimum x and minimum y pair from all the defining points to establish the upper-left corner of the rectangle, and the maximum x and maximum y pair for the bottom right. This involves going through all the points in the list. You will, therefore, compute the enclosing rectangle incrementally in the AddSegment() function as points are added to the curve.

With the constructor and the AddSegment() function added, the complete definition of the CCurve class is:

```
class CCurve: public CElement
{
public:
    ~CCurve(void);
    virtual void Draw(CDC* pDC);        // Function to display a curve

    // Constructor for a curve object
    CCurve(CPoint FirstPoint, CPoint SecondPoint, COLORREF aColor);

    void AddSegment(CPoint& aPoint);    //Add a segment to the curve

protected:
    CCurve(void);                       // Default constructor - should not be used
    CList<CPoint, CPoint&> m_PointList; // Type safe point list
};
```

You should modify the definition of the class in Elements.h to correspond with the previous code. The constructor has the first two defining points and the color as parameters, so it only defines a curve with one segment. This is called in the CreateElement() function invoked by the OnMouseMove() function in the view class the first time a WM_MOUSEMOVE message is received for a curve, so don’t forget to modify the definition of the CreateElement() function in CSketcherView to call the CCurve class constructor with the correct arguments. The statement using the CCurve constructor in the switch in the CreateElement() function should be changed to:

```
case CURVE:
    return new CCurve(m_FirstPoint, m_SecondPoint, pDoc->GetElementColor());
```

After the constructor has been called, all subsequent WM_MOUSEMOVE messages results in the AddSegment() function being called to add a segment to the existing curve, as shown in Figure 15-6:

![](img/2359b0c604600c58fba3539c738a356e_817_0.png)

This shows the complete sequence of message handler calls for a curve comprised of nine segments. The sequence is indicated by the numbered arrows. The code for the OnMouseMove() function in CSketcherView needs to be updated as follows:

```cpp
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
CClientDC adc(this);  // Device context for the current view
if ((nFlags & MK_LBUTTON) && (this==GetCapture()))
{
m_SecondPoint = point;  // Save the current cursor position
if(m_pTempElement)
{
if(CURVE == GetDocument()->GetElementType())  // Is it a curve?
{
// We are drawing a curve
// so add a segment to the existing curve
static_cast<CCurve*>(m_pTempElement)->AddSegment(m_SecondPoint);
m_pTempElement->Draw(&adc);  // Now draw it
return;
// We are done
}
}
adc.SetROP2(R2_NOTXORPEN);  // Set drawing mode
// Redraw the old element so it disappears from the view
m_pTempElement->Draw(&adc);
// Delete the old element
delete m_pTempElement;  // Delete the old element
m_pTempElement = 0;  // Reset the pointer to 0
// Create an element of the type and color 
// recorded in the document object
m_pTempElement = CreateElement();
m_pTempElement->Draw(&adc);
}
}
```

You have to treat an element of type **CURVE** as a special case after it has been created because on all subsequent calls of the `OnMouseMove()` handler you want to call the `AddSegment()` function for the existing element, rather than construct a new one in place of the old. You don’t want to set the drawing mode in this instance because you don’t need to erase the previous curve each time. You take care of this by moving the call to `SetROP2()` to a position after the code processing a curve.

Adding the curve segment and drawing the extended curve is taken care of within the `if` statement you have added. Note that you must cast the `m_pTempElement` pointer to type `CCurve*` to use it to call `AddSegment()` for the old element because `AddSegment()` is not a virtual function. If you don’t add the cast, you’ll get an error because the compiler tries to resolve the call statically to a member of the `CElement` class.

## Implementing the CCurve Class

Write the code for the constructor; this should be added to `Elements.cpp` in place of the temporary constructor that you used in the last chapter. It needs to store the two points passed as arguments in the `CList` data member, `m_PointList`:

```
CCurve::CCurve(CPoint FirstPoint,CPoint SecondPoint, COLORREF aColor)
{
    m_PointList.AddTail(FirstPoint);      // Add the 1st point to the list
    m_PointList.AddTail(SecondPoint);     // Add the 2nd point to the list
    m_Color = aColor;                     // Store the color
    m_Pen = 1;                            // Set the pen width

    // Construct the enclosing rectangle assuming MM_TEXT mode
    m_EnclosingRect = CRect(FirstPoint, SecondPoint);
    m_EnclosingRect.NormalizeRect();
}
```

The points are added to the list, `m_PointList`, by calling the `AddTail()` member of the `CList` template class. This function adds a copy of the point passed as an argument to the end of the list. The enclosing rectangle is defined in exactly the same way that defined it for a line.

You can add the `AddSegment()` function to `Elements.cpp` next. This function is called when additional curve points are recorded, after the first version of a curve object has been created. This member function is very simple:

```
void CCurve::AddSegment(CPoint& aPoint)
{
    m_PointList.AddTail(aPoint);             // Add the point to the end

    // Modify the enclosing rectangle for the new point
    m_EnclosingRect = CRect(min(aPoint.x, m_EnclosingRect.left),
                            min(aPoint.y, m_EnclosingRect.top),
                            max(aPoint.x, m_EnclosingRect.right),
                            max(aPoint.y, m_EnclosingRect.bottom));
}
```

The `min()` and `max()` functions you use here are standard macros that are the equivalent of using the conditional operator for choosing the minimum or maximum of two values. The new point is added to the tail of the list in the same way as in the constructor. It’s important that each new point is added to the

list in a way that is consistent with the constructor because you’ll draw the segments using the points in sequence, from the beginning to the end of the list. Each line segment is drawn from the end point of the previous line to the new point. If the points are not in the right sequence, the line segments won’t be drawn correctly. After adding the new point, the enclosing rectangle for the curve is redefined, taking account of the new point.

The last member function you need to define for the interface to the CCurve class is Draw():

```
void CCurve::Draw(CDC* pDC)
{
    // Create a pen for this object and
    // initialize it to the object color and line width of 1 pixel
    CPen aPen;
    if(!aPen.CreatePen(PS_SOLID, m_Pen, m_Color))
    {
        // Pen creation failed. Close the program
        AfxMessageBox(_T("Pen creation failed drawing a curve"), MB_OK);
        AfxAbort();
    }

    CPen* pOldPen = pDC->SelectObject(&aPen);  // Select the pen

    // Now draw the curve
    // Get the position in the list of the first element
    POSITION aPosition = m_PointList.GetHeadPosition();

    // As long as it’s good, move to that point
    if(aPosition)
        pDC->MoveTo(m_PointList.GetNext(aPosition));

    // Draw a segment for each of the following points
    while(aPosition)
        pDC->LineTo(m_PointList.GetNext(aPosition));

    pDC->SelectObject(pOldPen);            // Restore the old pen
}
```

You draw the CCurve object by iterating through all the points in the list from the beginning, drawing each segment as you go. You get a POSITION value for the first element by using the function GetHeadPosition() and then use MoveTo() to set the first point as the current position in the device context. You then draw line segments in the while loop as long as aPosition is not NULL. The GetNext() function call that appears as the argument to the LineTo() function returns the current point and simultaneously increments aPosition to refer to the next point in the list.

## Exercising the CCurve Class

With the changes I’ve just discussed added to the Sketcher program, you have implemented all the code necessary for the element shapes in your menu. You can now build the Sketcher program once more, and execute it. You should be able to create curves in all four colors. A typical application window is shown in Figure 15-7.

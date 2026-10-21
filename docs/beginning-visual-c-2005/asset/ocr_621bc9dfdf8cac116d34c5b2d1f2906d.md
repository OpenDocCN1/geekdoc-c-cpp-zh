# Chapter 15

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

# Exercising the CCurve Class

With the changes I’ve just discussed added to the Sketcher program, you have implemented all the code necessary for the element shapes in your menu. You can now build the Sketcher program once more, and execute it. You should be able to create curves in all four colors. A typical application window is shown in Figure 15-7.
# Chapter 15

This is a very simple change. You set the new local variable aColor to the current color stored in m_Color, and the if statement will reset the value of aColor to SELECT_COLOR when pElement is equal to this — which is the case when the current element and the selected element are the same. You also need to add the definition for SELECT_COLOR to the OurConstants.h file:

```
//Definitions of constants
#pragma once

// Element type definitions
// Each type value must be unique
const unsigned int LINE = 101U;
const unsigned int RECTANGLE = 102U;
const unsigned int CIRCLE = 103U;
const unsigned int CURVE = 104U;

// Color values for drawing
const COLORREF BLACK = RGB(0,0,0);
const COLORREF RED = RGB(255,0,0);
const COLORREF GREEN = RGB(0,255,0);
const COLORREF BLUE = RGB(0,0,255);
const COLORREF SELECT_COLOR = RGB(255,0,180);
```

Now you should add an #include directive for OurConstants.h to the CElements.cpp file to make the definition of SELECT_COLOR available. You have nearly implemented the highlighting. The derived classes of the CElement class are now able to draw themselves as selected — you just need a mechanism to cause an element to be selected. So where should you do this? You determine which element, if any, is under the cursor in the OnMouse() handler in the CSketcherView class, so that’s obviously the place to expedite the highlighting.

The amendments to the OnMouseMove() handler are:

```
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
// Define a Device Context object for the view
CCilentDC aDC(this); // DC is for this view
OnPrepareDC(&aDC); // Get origin adjusted
aDC.SetROP2(R2_NOTXORPEN); // Set the drawing mode
if((nFlags&MK_LBUTTON) && (this==GetCapture()))
{
aDC.DPtoLP(&point); // convert point to Logical
m_SecondPoint = point; // Save the current cursor position
if(m_pTempElement)
{
if(CURVE == GetDocument()->GetElementType()) // Is it a curve?
{
// We are drawing a curve
// so add a segment to the existing curve
static_cast<CCurve*>(m_pTempElement)->AddSegment(m_SecondPoint);
}
}
}
```
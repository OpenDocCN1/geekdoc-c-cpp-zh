
# Chapter 14

Add the specifications of the function, as shown, and click the Finish button. A declaration for the function member is added to the class definition and you are taken directly to a skeleton for the function in `CSketcherView.cpp`. If you added the declaration to the class definition manually, you’ll need to add the complete definition for the function to the `.cpp` file. This is:

```cpp
// Create an element of the current type
CElement* CSketcherView::CreateElement(void)
{
    // Get a pointer to the document for this view
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);                 // Verify the pointer is good

    // Now select the element using the type stored in the document
    switch(pDoc->GetElementType())
    {
        case RECTANGLE:
            return new CRectangle(m_FirstPoint, m_SecondPoint,
                                  pDoc->GetElementColor());

        case CIRCLE:
            return new CCircle(m_FirstPoint, m_SecondPoint,
                               pDoc->GetElementColor());

        case CURVE:
            return new CCurve(pDoc->GetElementColor());

        case LINE:
            return new CLine(m_FirstPoint, m_SecondPoint,
                             pDoc->GetElementColor());

        default:
            // Something's gone wrong
            AfxMessageBox(_T("Bad Element code"), MB_OK);
            AfxAbort();
            return NULL;
    }
}
```

The lines that aren’t shaded are those that will have been supplied automatically if you added the function to the class using the Add > Add Function dialog. The first thing you do here is get a pointer to the document by calling `GetDocument()`, as you’ve seen before. For safety, you use the `ASSERT_VALID()` macro to ensure that a good pointer is returned. In the debug version of MFC that’s used in the debug version of your application, this macro calls the `AssertValid()` member of the object, which is specified as the argument to the macro. This checks the validity of the current object, and if the pointer is `NULL` or the object is defective in some way, an error message is displayed. In the release version of MFC, the `ASSERT_VALID()` macro does nothing.

The switch statement selects the element to be created based on the type returned by a function in the document class, `GetElementType()`. Another function in the document class is used to obtain the current element color. You can add the definitions for both these functions directly to the `CSketcherDoc` class definition because they are very simple:

```cpp
class CSketcherDoc: public CDocument
{
    // Rest of the class definition as before...
    // Operations
public:
    unsigned int GetElementType()      // Get the element type
    { return m_Element; }
    COLORREF GetElementColor()         // Get the element color
    { return m_Color; }
    // Rest of the class definition as before...
};
```

Each of the functions returns the value stored in the corresponding data member. Remember that putting a member function definition in the class definition is equivalent to a request to make the function inline, so as well as being simple, these should be fast.

## Dealing with WM_LBUTTONUP Messages

The WM_LBUTTONUP message completes the process of creating an element. The job of the handler for this message is to pass the final version of the element that was created to the document object, and then clean up the view object data members. You can access and edit the code for this handler in the same way as you did for the previous one. Add the following lines to the function:

```cpp
void CSketcherView::OnLButtonUp(UINT nFlags, CPoint point)
{
    // Make sure there is an element
    if(m_pTempElement)
    {
        // Call a document class function to store the element
        // pointed to by m_pTempElement in the document object
        delete m_pTempElement;      // This code is temporary
        m_pTempElement = 0;         // Reset the element pointer
    }
}
```

The if statement verifies that m_pTempElement is not zero before processing it. It’s always possible that the user could press and release the left mouse button without moving the mouse, in which case no element would have been created. As long as there is an element, the pointer to the element is passed to the document object; you’ll add the code for this in the next chapter. In the meantime, you just delete the element here so as not to pollute the heap. Finally, the m_pTempElement pointer is reset to 0, ready for the next time the user draws an element.

## Exercising Sketcher

Before you can run the example with the mouse message handlers, you must update the OnDraw() function in the CSketcherView class implementation to get rid of any old code that you added earlier.

To make sure that the OnDraw() function is clean, go to Class View and double-click the function name to take you to its implementation in SketcherView.cpp. Delete any old code that you added, but leave in the first four lines that the wizard provided to get a pointer to the document object. You'll need this later to get to the elements when they're stored in the document. The code for the function should now be:

```cpp
void CSketcherView::OnDraw(CDC* pDC)
{
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    if (!pDoc)
        return;
}
```

Because you have no elements in the document as yet, you don't need to add anything to this function at this point. When you start storing data in the document in the next chapter, you'll add code to draw the elements in response to a WM_PAINT message. Without it, the elements just disappear whenever you resize the view, as you'll see.

## Running the Example

After making sure that you have saved all the source files, build the program. If you haven't made any mistakes entering the code, you'll get a clean compile and link, so you can execute the program. You can draw lines, circles and rectangles in any of the four colors the program supports. A typical window is shown in Figure 14-20.

![](img/2359b0c604600c58fba3539c738a356e_795_0.png)

Figure 14-20

Try experimenting with the user interface. Note that you can move the window around and that the shapes stay in the window as long as you don't move it so far that they're outside the borders of the application window. If you do, the elements do not reappear after you move it back. This is because the existing elements are never redrawn. When the client area is covered and uncovered, Windows sends a WM_PAINT message to the application that causes the OnDraw() member of the view object to be called. As you know, the OnDraw() function for the view doesn’t do anything at present. This gets fixed when you use the document to store the elements.

When you resize the view window, the shapes disappear immediately, but when you move the whole view around, they remain (as long as they don’t slide beyond the application window border). How come? Well, when you resize the window, Windows invalidates the whole client area and expects your application to redraw it in response to the WM_PAINT message. If you move the view around, Windows takes care of relocating the client area as it is. You can demonstrate this by moving the view so that a shape is partially obscured. When you slide it back, you still have a partial shape, with the bit that was obscured erased.

If you try drawing a shape while dragging the cursor outside the client view area, you’ll notice some peculiar effects. Outside the view window, you lose track of the mouse, which tends to mess up the rubber-banding mechanism. What’s going on?

## Capturing Mouse Messages

The problem is caused by the fact that Windows is sending the mouse messages to the window under the cursor. As soon as the cursor leaves the client area of your application view window, the WM_MOUSEMOVE messages are being sent elsewhere. You can fix this by using some inherited members of the CSketcherView class.

The view class inherits a function, SetCapture(), which you can call to tell Windows that you want your view window to get all the mouse messages until such time as you say otherwise, by calling another inherited function in the view class, ReleaseCapture(). You can capture the mouse as soon as the left button is pressed by modifying the handler for the WM_LBUTTONDOWN message:

```cpp
// Handler for left mouse button down message
void CSketcherView::OnLButtonDown(UINT nFlags, CPoint point)
{
    m_FirstPoint = point;        // Record the cursor position
    SetCapture();                // Capture subsequent mouse messages
}
```

Now you must call the ReleaseCapture() function in the WM_LBUTTONUP handler. If you don’t do this, other programs cannot receive any mouse messages as long as your program continues to run. Of course, you should only release the mouse if you’ve captured it earlier. The GetCapture() function that the view class inherits returns a pointer to the window that has captured the mouse, and this gives you a way of telling whether or not you have captured mouse messages. You just need to add the following to the handler for WM_LBUTTONUP:

```cpp
void CSketcherView::OnLButtonUp(UINT nFlags, CPoint point)
{
    if(this == GetCapture())
        ReleaseCapture();        // Stop capturing mouse messages

    // Make sure there is an element
```

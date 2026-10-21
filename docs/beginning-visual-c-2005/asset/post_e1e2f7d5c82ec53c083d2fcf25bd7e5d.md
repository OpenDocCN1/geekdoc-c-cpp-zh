
## Chapter 14

the definitions of the standard system header files available in the file. You may need to add #include directives for the files containing definitions for Application Wizard-generated classes if you use any in the code.

Of course, you'll have to add each of the member function definitions to this file manually because ClassWizard wasn't involved in defining the classes. You're now ready to add the constructor for the CLine class to the Elements.cpp file.

The code for this is:

```cpp
// CLine class constructor
CLine::CLine(CPoint Start, CPoint End, COLORREF aColor)
{
    m_StartPoint = Start;               // Set line start point
    m_EndPoint = End;                   // Set line end point
    m_Color = aColor;                   // Set line color
}
```

You first store the start point in the m_StartPoint member that is inherited from the CElement class. Later you'll add code to allow an element to be moved and to enable a line to be moved by just changing the start point and the end point must be defined relative to the start point. You do this by subtracting the x and y coordinate values of Start from those of End. Both x and y are public members of the CPoint class so you can refer to them directly. Finally, you store the color in the m_Color member that is inherited from the CElement class.

The Draw() function for the CLine class isn’t too difficult either, although you do need to take account of the color to be used when the line is drawn:

```cpp
// Draw a CLine object
void CLine::Draw(CDC* pDC)
{
    // Create a pen for this object and
    // initialize it to the object color and line width of 1 pixel
    CPen aPen;
    if(!aPen.CreatePen(PS_SOLID, m_Pen, m_Color))
    {
        // Pen creation failed. Abort the program
        AfxMessageBox(_T("Pen creation failed drawing a line"), MB_OK);
        AfxAbort();
    }
    CPen* pOldPen = pDC->SelectObject(&aPen); // Select the pen
    // Now draw the line
    pDC->MoveTo(m_StartPoint);
    pDC->LineTo(m_EndPoint);
    // Restore the old pen
    pDC->SelectObject(pOldPen);
}
```

I have called the rectangle that is used to draw a shape the ‘enclosing rectangle,’ while the rectangle that takes into account the width of the pen I’ve called the ‘bounding rectangle’ to differentiate it. Figure 14-17 shows the shapes with their enclosing rectangles, and their bounding rectangles offset by the line thickness. This is obviously exaggerated here so you can see what’s happening.

The differences in how you calculate the coordinates for the bounding rectangle in different mapping modes only concerns the y coordinate; calculation of the x coordinate is the same for all mapping modes. To get the corners of the bounding rectangle in the MM_TEXT mapping mode, subtract the line thickness from the y coordinate of the upper-left corner of the defining rectangle, and add it to the y coordinate of the lower-right corner. However, in MM_LOENGLISH (and all the other mapping modes), the y axis increases in the opposite direction, so you need to add the line thickness to the y coordinate of the upper-left corner of the defining rectangle, and subtract it from the y coordinate of the lower-right corner. For all the mapping modes, you subtract the line thickness from the x coordinate of the upper-left corner of the defining rectangle, and add it to the x coordinate of the lower-right corner.

To implement the element types as consistently as possible in Sketcher, you could store an enclosing rectangle for each shape in a member in the base class. The enclosing rectangle needs to be calculated when a shape is constructed. The job of the GetBoundRect() function in the base class will then be to calculate the bounding rectangle by offsetting the enclosing rectangle by the pen width. You can amend the CElement class definition by adding two data members, as follows:

```cpp
class CElement: public CObject
{
protected:
    COLORREF m_Color;                  // Color of an element
    CRect m_EnclosingRect;             // Rectangle enclosing an element
    int m_Pen;                         // Pen width

public:
    virtual ~CElement();               // Virtual destructor
    virtual void Draw(CDC* pDC) {}     // Virtual draw operation

    CRect GetBoundRect();              // Get the bounding rectangle for an element

protected:
    CElement();                        // Here to prevent it being called
};
```

You can add these by right-clicking on the class name and selecting Add Member Variable from the pop-up, or you can add the statements directly in the Editor window along with the comments.

You must also update the CLine constructor so that it has the correct pen width:

```cpp
// CLine class constructor
CLine::CLine(CPoint Start, CPoint End, COLORREF aColor)
{
    m_StartPoint = Start;              // Set line start point
    m_EndPoint = End;                  // Set line end point
    m_Color = aColor;                  // Set line color
    m_Pen = 1;                         // Set pen width
}
```

You can now implement the `GetBoundRect()` member of the base class, assuming the `MM_TEXT` mapping mode:

```cpp
// Get the bounding rectangle for an element
CRect CElement::GetBoundRect()
{
    CRect BoundingRect;              // Object to store bounding rectangle
    BoundingRect = m_EnclosingRect;  // Store the enclosing rectangle

    // Increase the rectangle by the pen width
    BoundingRect.InflateRect(m_Pen, m_Pen);
    return BoundingRect;             // Return the bounding rectangle
}
```

This returns the bounding rectangle for any derived class object. You define the bounding rectangle by modifying the coordinates of the enclosing rectangle stored in the base class data member so that it is enlarged all round by the pen width, using the `InflateRect()` method of the `CRect` class.

The `CRect` class provides an operator + for rectangles, which you could have used instead. For example, you could have written the statement before the return as:

```cpp
BoundingRect = m_EnclosingRect + CRect(m_Pen, m_Pen, m_Pen, m_Pen);
```

Equally, you could have simply added (or subtracted) the pen width for each of the x and y values that make up the rectangle. You could have replaced the assignment with the following statements:

```cpp
BoundingRect = m_EnclosingRect;
BoundingRect.top -= m_Pen;
BoundingRect.left -= m_Pen;
BoundingRect.bottom += m_Pen;
BoundingRect.right += m_Pen;
```

> As a reminder, the individual data members of a CRect object are left and top (storing the x and y coordinates of the upper-left corner) and right and bottom (storing the coordinates of the lower-right corner). These are all public members, so you can access them directly. A commonly made mistake, especially by me, is to write the coordinate pair as (top,left) instead of in the correct order (left,top).

The hazard with both this and the `InflateRect()` option is that there is a built-in assumption that the mapping mode is `MM_TEXT`, which means that the positive y axis is assumed to run from top to bottom. If you change the mapping mode, neither of these will work properly, although it’s not immediately obvious that they won’t.

### Normalized Rectangles

The `InflateRect()` function works by subtracting the values that you give it from the top and left members of the rectangle and adding the values to the bottom and right. This means that you may find your rectangle actually decreasing in size if you don’t make sure that the rectangle is normalized. A normalized rectangle has a left value that is less than or equal to the right value, and a top value that is less than or equal to the bottom value. You can make sure that a `CRect` object is normalized by calling the `NormalizeRect()` member of the object. Most of the CRect member functions require the object to be normalized for them to work as expected, so you need to make sure that when you store the enclosing rectangle in `m_EnclosingRect`, it is normalized.

### Calculating the Enclosing Rectangle for a Line

All you need now is code in the constructor for a line to calculate the enclosing rectangle:

```cpp
CLine::CLine(CPoint Start, CPoint End, COLORREF aColor)
{
    m_StartPoint = Start;                // Set line start point
    m_EndPoint = End;                    // Set line end point
    m_Color = aColor;                    // Set line color
    m_Pen = 1;                           // Set pen width

    // Define the enclosing rectangle
    m_EnclosingRect = CRect(Start, End);
    m_EnclosingRect.NormalizeRect();
}
```

The arguments to the CRect constructor you are using here are the start and end points of the line. To ensure that the bounding rectangle has the top value less than the bottom value, regardless of the relative positions of the start and end points of the line, you call the NormalizeRect() member of the m_EnclosingRect object.

### The CRectangle Class

Although you'll be defining a rectangle object by the same data that you use to define a line (a start point and an end point on a diagonal of the rectangle), you don't need to store the defining points. The enclosing rectangle in the data member inherited from the base class completely defines the shape, so you don't need any data members. You can therefore define the class like this:

```cpp
// Class defining a rectangle object
class CRectangle: public CElement
{
public:
    ~CRectangle(void);
    virtual void Draw(CDC* pDC);        // Function to display a rectangle

    // Constructor for a rectangle object
    CRectangle(CPoint Start, CPoint End, COLORREF aColor);

protected:
    CRectangle(void);                   // Default constructor - should not be used
};
```

The no-arg constructor is now protected to prevent it from being used. The definition of the rectangle becomes very simple — just a constructor, the virtual Draw() function, plus the no-arg constructor in the protected section of the class.

### The CRectangle Class Constructor

The code for the new CRectangle class constructor is somewhat similar to that for a CLine constructor:

```cpp
// CRectangle class constructor
CRectangle::CRectangle(CPoint Start, CPoint End, COLORREF aColor)
{
```

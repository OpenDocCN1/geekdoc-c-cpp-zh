# Chapter 15

The last option looks to be the best choice, so go with that. You can extend the document class definition to:

```
class CSketcherDoc: public CDocument
{

// Rest of the class as before...

// Operations
public:
    unsigned int GetElementType()        // Get the element type
    { return m_Element; }
    COLORREF GetElementColor()           // Get the element color
    { return m_Color; }
    void AddElement(CElement* pElement) // Add an element to the list
    { m_ElementList.AddTail(pElement); }
    POSITION GetListHeadPosition()       // return list head POSITION value
    { return m_ElementList.GetHeadPosition(); }
    CElement* GetNext(POSITION& aPos)    // Return current element pointer
    { return m_ElementList.GetNext(aPos); }

// Rest of the class as before...
};
```

By using the two functions you have added to the document class, the OnDraw() function for the view will be able to iterate through the list, calling the Draw() function for each element. The implementation of OnDraw() to do this is:

```
void CSketcherView::OnDraw(CDC* pDC)
{
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    if (!pDoc)
        return;

    POSITION aPos = pDoc->GetListHeadPosition();
    while(aPos)                         // Loop while aPos is not null
    {
        pDoc->GetNext(aPos)->Draw(pDC); // Draw the current element
    }
}
```

This implementation of the OnDraw() function always draws all the elements the document contains. The statement in the while loop first gets a pointer to an element from the document with the expression pDoc->GetNext(). The pointer that is returned is used to call the Draw() function for that element. The statement works this way without parentheses because of the left to right associativity of the -> operator. The while loop plows through the list from beginning to end. You can do it better though, and make the program more efficient.

Frequently, when a WM_PAINT message is sent to your program, only part of the window needs to be redrawn. When Windows sends the WM_PAINT message to a window, it also defines an area in the client area of the window, and only this area needs to be redrawn. The CDC class provides a member function,
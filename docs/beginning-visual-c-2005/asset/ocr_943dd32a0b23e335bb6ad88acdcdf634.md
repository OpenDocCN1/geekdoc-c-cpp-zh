```
public:
    void DeleteElement(CElement* pElement); // Delete an element
    unsigned int GetElementType()
        { return m_Element; }    // Get the element type

// Rest of the class as before...
};
```

It accepts a pointer to the element to be deleted as an argument and returns nothing. You can implement it in SketcherDoc.cpp as:

```
void CSketcherDoc::DeleteElement(CElement* pElement)
{
    if(pElement)
    {
        // If the element pointer is valid,
        // find the pointer in the list and delete it
        POSITION aPosition = m_ElementList.Find(pElement);
        m_ElementList.RemoveAt(aPosition);
        delete pElement;                // Delete the element from the heap
    }
}
```

You shouldn’t have any trouble understanding how this works. After making sure that you have a non-null pointer, you find the POSITION value for the pointer in the list using the Find() member of the list object. You use this with the RemoveAt() member to delete the pointer from the list, then delete the element pointed to by the parameter pElement from the heap.

That’s all you need to delete elements. You should now have a Sketcher program in which you can draw in multiple scrolled views, and delete any of the elements in your sketch from any of the views.

# Moving an Element

Moving the selected element is a bit more involved. As the element must move along with the mouse cursor, you must add code to the OnMouseMove() method to account for this behavior. As this function is also used to draw elements, you need a mechanism for indicating when you’re in “move” mode. The easiest way to do this is to have a flag in the view class, which you can call m_MoveMode. If you make it of type BOOL, you use the value TRUE for when move mode is on, and FALSE for when it’s off. Of course, you could also define it as the fundamental type, bool, and the values are true and false.

You’ll also have to keep track of the cursor during the move, so you can another data member in the view for this. You can call it m_CursorPos, and it will be of type CPoint. Another thing you should provide for is the possibility of aborting a move. To do this you must remember the first position of the cursor when the move operation started, so you can move the element back when necessary. This is another member of type CPoint, and it is called m_FirstPos. Add the three new members to the protected section of the view class:

```
class CSketcherView: public CScrollView
{
    // Rest of the class as before...

protected:
```
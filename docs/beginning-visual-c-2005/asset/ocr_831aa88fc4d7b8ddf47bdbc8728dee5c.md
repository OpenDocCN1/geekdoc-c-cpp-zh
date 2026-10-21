You only need to change one line. The Draw() function for an element has the second argument added to communicate the address of the element to be highlighted.

# Exercising the Highlights

This is all that’s required for the highlighting to work all the time. It wasn’t trivial but on the other hand it wasn’t terribly difficult either. You can build and execute Sketcher to try it out. Any time there is an element under the cursor, the element is drawn in magenta. This makes it obvious which element the context menu is going to act on before you right-click the mouse and means that you know in advance which context menu is displayed.

# Servicing the Menu Messages

The next step is to provide code in the bodies of the handlers for the Move and Delete menu items that you added earlier. You can add the code for Delete first, as that’s the simpler of the two.

# Deleting an Element

The code that you need in the OnElementDelete() handler in the CSketcherView class to delete the currently selected element is simple:

```
void CSketcherView::OnElementDelete()
{
    if(m_pSelected)
    {
        CSketcherDoc* pDoc = GetDocument();// Get the document pointer
        pDoc->DeleteElement(m_pSelected);    // Delete the element
        pDoc->UpdateAllViews(0);             // Redraw all the views
        m_pSelected = 0;                     // Reset selected element ptr
    }
}
```

The code to delete an element is only executed if m_pSelected contains a valid address, indicating that there is an element to be deleted. You get a pointer to the document and call the function DeleteElement() for the document object; you’ll add this member to the CSketcherDoc class in a moment. When the element has been removed from the document, you call UpdateAllViews() to get all the views redrawn without the deleted element. Finally, you set m_pSelected to zero to indicate that there isn’t an element selected.

You can add a declaration for DeleteElement() as a public member of the CSketcherDoc class:

```
class CSketcherDoc : public CDocument
{
protected: // create from serialization only
    CSketcherDoc();
    DECLARE_DYNCREATE(CSketcherDoc)

// Attributes
public:

// Operations
```
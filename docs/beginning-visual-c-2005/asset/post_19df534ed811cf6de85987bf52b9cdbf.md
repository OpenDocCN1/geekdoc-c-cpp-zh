
## Chapter 14

```
if(m_pTempElement)
{
    // Call a document class function to store the element
    // pointed to by m_pTempElement in the document object
    delete m_pTempElement;    // This code is temporary
    m_pTempElement = 0;       // Reset the element pointer
}
```

If the pointer returned by the GetCapture() function is equal to the pointer this, your view has captured the mouse, so you release it.

The final alteration you should make is to modify the WM_MOUSEMOVE handler so that it only deals with messages that have been captured by the view. You can do this with one small change:

```
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
    // Define a Device Context object for the view
    CClientDC aDC(this);                // DC is for this view
    aDC.SetROP2(R2_NOTXORPEN);          // Set the drawing mode
    if((nFlags & MK_LBUTTON) && (this == GetCapture()))
    {
        m_SecondPoint = point;          // Save the current cursor position
        if(m_pTempElement)
        {
            // Redraw the old element so it disappears from the view
            m_pTempElement->Draw(&aDC);
            delete m_pTempElement;      // Delete the old element
            m_pTempElement = 0;         // Reset the pointer to 0
        }
        // Create a temporary element of the type and color that
        // is recorded in the document object, and draw it
        m_pTempElement = CreateElement();// Create a new element
        m_pTempElement->Draw(&aDC);      // Draw the element
    }
}
```

The handler now processes only the message if the left button is down and the left button down handler for your view has been called, so that the mouse has been captured by your view window.

If you rebuild Sketcher with these additions, you’ll find that the problems that arose earlier when the cursor was dragged off the client area no longer occur.

### Summary

After completing this chapter, you should have a good grasp of how to write message handlers for the mouse, and how to organize drawing operations in your Windows programs. The important points covered in this chapter are:

enclosing rectangle? Modify the example to work this way. (Hint—look up the CPoint class members in Help.)

- 4. Add a new menu pop-up to the IDR(SketcherTYPE menu for Pen Style, to allow solid, dashed, dotted, dash-dotted, and dash-dot-dotted lines to be specified.
- 5. Which parts of the program need to be modified to support the operation of the menu, and the drawing of elements in these line types?
- 6. Implement support for the new menu pop-up and drawing elements in any of the line types.

## Creating the Document and Improving the View

In this chapter, you’ll look into the facilities offered by MFC for managing collections of data items. You’ll use these to complete the class definition and implementation for the curve element that was left open in the last chapter. You’ll also extend the Sketcher application to store data in a document, and make the document view more flexible, introducing several new techniques in the process.

In this chapter, you’ll learn about:

- - Collections and what you can do with them
- - How to use a collection to store point data for a curve
- - How to use a collection to store document data
- - How to implement drawing a document
- - How to implement scrolling in a view
- - How to create a context menu at the cursor
- - How to highlight the element nearest the cursor to provide feedback to the user for moving and deleting elements
- - How to program the mouse to move and delete elements

### What Are Collection Classes?

By the nature of Windows programming, you’ll frequently need to handle collections of data items where you have no advance knowledge of how many items you will need to manage, or even what particular type they are going to be. This is clearly illustrated by the Sketcher application. The user can draw an arbitrary number of elements which can be lines, rectangles, circles and curves, and in any sequence. MFC provides a group of collection classes designed to handle

exactly this sort of problem — a collection being an aggregation of an arbitrary number of data items organized in a particular way.

## Chapter 15

### Types of Collection

MFC provides you with a large number of collection classes for managing data. You’ll use just a couple of them in practice, but it would be helpful to understand the types of collections available. MFC supports three kinds of collections, differentiated by the way in which the data items are organized. The way a collection is organized is referred to as the shape of the collection. The three types of organization, or shape, are:

| Shape | How information is organized |
|-------|------------------------------|
| Array | An array in this context is just like the array you have seen in the C++ language. It’s an ordered arrangement of elements, where any element is retrieved by using an integer index value. An array collection can automatically grow to accommodate more data items; however, one of the other collection types is generally preferred, because array collections can be rather slow in operation. |
| List | A list collection is an ordered arrangement of data items, where each item has two pointers associated with it that point to the next and previous items in the list. You saw a linked list in Chapter 7, when I discussed structures. The list here is called a doubly linked list because it has backward as well as forward-pointing links. It can be searched in either direction and, like an array, a list collection grows automatically when required. A list collection is easy to use, and fast when it comes to adding items. Searching for an item can be slow, though, if there are a lot of data items in the list. |
| Map | A map is an unordered collection of data items, where each item is associated with a key that is used to retrieve the item from the map. A key is usually a string, but it can also be a numeric value or any type of object. Maps are fast in storing data items and in searching because a key takes you directly to the item you need. This sounds as though maps are always the ideal choice, and this is often the case, but for sequential access arrays are faster. You also have the problem of choosing a key for your object that’s unique for each item in the list. |

MFC collection classes provide two approaches to implementing each type of collection. One approach is based on the use of class templates and provides you with type-safe handling of data in a collection. Type-safe handling means that the data passed to a function member of the collection class are checked to ensure that it’s of a type that can be processed by the function.

The other approach makes use of a range of collection classes (rather than templates), but these perform no data checking. If you want your collection classes to be type-safe, you have to include code yourself to assure this. These latter classes were available in older versions of Visual C++ under Windows, but the template collection classes were not. I’ll concentrate on the template-based versions because these provide the best chance of avoiding errors in our application.

### The Type-Safe Collection Classes

The template-based type-safe collection classes support collections of objects of any type, and collections of pointers to objects of any type. Collections of objects are supported by the template classes CArray, CList and CMap, and collections of pointers to objects are supported by the template classes CTypedPtrArray, CTypedPtrList and CTypedPtrMap. I won’t go into the detail of all of these, just the two that you’ll use in the Sketcher program. You’ll use one to store objects and the other to store pointers to objects so you’ll get a feel for both sorts of collection.

### Collections of Objects

The template classes for defining collections of objects are all derived from the MFC class CObject. They are defined this way so that they inherit the properties of the CObject class, which are particularly useful for a number of things These include file input and output operations for objects generally referred to as serialization, and you’ll look at this in Chapter 17.

These template classes can store and manage any kind of object, including all the C++ basic data types, plus any classes or structures that you or anybody else might define. Because these classes store objects, whenever you add an element to a list, an array, or a map, the class template object needs to make a copy of your object. Consequently, any class type that you want to store in any of these collections must have a copy constructor. The copy constructor for your class is used to create a duplicate of the object that you want to store in the collection.

Take a look at the general properties of each of the template classes that provide type-safe management of objects. This is not an exhaustive treatment of all the member functions provided. Rather, it’s intended to give you a sufficient flavor of how they work to enable you to decide if you want to use them or not. You can get information on all of the member functions by using Help to get to the template class definition.

### The CArray Template Class

You can use this template to store any kind of object in an array and have the array automatically grow to accommodate more elements when necessary. An array collection is illustrated in Figure 15-1.

As with the arrays that you’ve seen in native C++, elements in array collections are indexed from 0. The declaration of an array collection takes two arguments. The first argument is the type of the object to be stored so, if your array collection is to store objects of type CPoint, for example, you specify CPoint as the first argument. The second argument is the type used in member function calls. To avoid the overhead in copying objects when passed by value, the second argument is usually a reference, so an example of an array collection declaration to hold CPoint objects is:

```
CArray<CPoint, CPoint&> PointArray;
```

This defines the array collection class object, PointArray, that stores CPoint objects. When you call function members of this object, the argument is a reference, so to add a CPoint object, you would write

```
PointArray.Add(aPoint);
```

and the argument aPoint is passed as a reference.

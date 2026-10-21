
## Creating the Document and Improving the View

The value of 503 for N is the smallest prime greater than the likely number of entries. The base chosen to evaluate a hash value for a string is usually a power of 2 that corresponds to the minimum value that is greater than or equal to the number of possible different characters in a string. For long strings, this can generate very large numbers, so special techniques are used to compute the value modulo N. Detailed discussion of these techniques is beyond the scope of this book, but you can find numerous Web references by searching on “hashing.”

## The Typed Pointer Collections

The typed pointer collection class templates store pointers to objects, rather than objects themselves. This is the primary difference between these class templates and the template classes just discussed. Take a look at how the CTypedPtrList class template is used, because you’ll use this as a basis for managing elements in your document class, CSketcherDoc.

## The CTypedPtrList Template Class

You can declare a typed pointer list class with a statement of the form:

```
CTypedPtrList<BaseClass, Type*> ListName;
```

The first argument specifies a base class that must be one of two pointer list classes defined in MFC, either CObList or CPtrList. Your choice depends on how your object class has been defined. Using the CObList class creates a list supporting pointers to objects derived from CObject, while CPtrList supports lists of void* pointers. Because the elements in the Sketcher example have CObject as a base class, I’ll concentrate on how CObList is used.

The second argument to the template is the type of the pointers to be stored in the list. In the example, this is going to be CElement* because all your shapes have CElement as a base class and CElement is derived from CObject. Thus, the declaration of a class for storing shapes is:

```
CTypedPtrList<CObList, CElement*> m_ElementList;
```

You could have used CObList* types to store the pointers to our elements, but then the list could contain an object of any class that has CObject as a base. The declaration of m_ElementList ensures that only pointers to objects of the class CElement can be stored. This provides a greatly increased level of security in the program.

## CTypedPtrList Operations

The functions provided in the CTypedPtrList based classes are similar to those supported by CList, except of course that all operations are with pointers to objects rather than with objects, so you need to tabulate them. They fall into two groups: those that are defined in CTypedPtrList, and those that are inherited from the base class — CObList in this case.

## Chapter 15

The functions defined in CTypedPtrList are:

| Function | Description |
|---|---|
| GetHead() | Returns the pointer at the head of the list. You should use IsEmpty() to verify that the list is not empty before calling this function. |
| GetTail() | Returns the pointer at the tail of the list. You should use IsEmpty() to verify that the list is not empty before calling this function. |
| RemoveHead() | Removes the first pointer in the list. You should use IsEmpty() to verify that the list is not empty before calling this function. |
| RemoveTail() | Removes the last pointer in the list. You should use IsEmpty() to verify that the list is not empty before calling this function. |
| GetNext() | Returns the pointer at the position indicated by the variable of type POSITION passed as a reference argument. The variable is updated to indicate the next element in the list. When the end of the list is reached, the position variable is set to NULL. This function can be used to iterate forwards through all the pointers in the list. |
| GetPrev() | Returns the pointer at the position indicated by the variable of type POSITION passed as a reference argument. The variable is updated to indicate the previous element in the list. When the beginning of the list is reached, the position variable is set to NULL. This function can be used to iterate backwards through all the pointers in the list. |
| GetAt() | Returns the pointer stored at the position indicated by the variable of type POSITION passed as an argument, which isn’t changed. Because the function returns a reference, as long as the list is not defined as const, this function can be used on the left of an assignment operator to modify a list entry. |

The functions in CTypedPtrList inherited from CObList are:

| Function | Description |
|---|---|
| AddHead() | Adds the pointer passed as an argument to the head of the list and returns a value of type POSITION that corresponds to the new element. There is another version of this function that can add another list to the head of the list. |
| AddTail() | Adds the pointer passed as an argument to the tail of the list and returns a value of type POSITION that corresponds to the new element. There is another version of this function that can add another list to the tail of the list. |
| RemoveAll() | Removes all the elements from the list. Note that this doesn’t delete the objects pointed to by elements in the list. You need to take care of this yourself. |

| Function | Description |
|---|---|
| GetHeadPosition() | Returns the position of the element at the head of the list. |
| GetTailPosition() | Returns the position of the element at the tail of the list. |
| SetAt() | Stores the pointer specified by the second argument at the position in the list defined by the first argument. An invalid position value causes an error. |
| RemoveAt() | Removes the pointer from the position in the list specified by the argument of type POSITION. An invalid position value causes an error. |
| InsertBefore() | Inserts a new pointer specified by the second argument before the position specified by the first argument. The position of the new element is returned. |
| InsertAfter() | Inserts a new pointer specified by the second argument after the position specified by the first argument. The position of the new element is returned. |
| Find() | Searches for a pointer in the list that is identical to the pointer specified as an argument. Its position is returned if it is found. NULL is returned otherwise. |
| FindIndex() | Returns the position of a pointer in the list specified by a zero-based integer index argument. |
| GetCount() | Returns the number of elements in the list. |
| IsEmpty() | Returns TRUE if there are no elements in the list, and FALSE otherwise. |

You’ll see some of these member functions in action a little later in this chapter in the context of implementing the document class for the Sketcher program.

## Using the CList Template Class

You can use of the CList collection template in the definition of the curve object in our Sketcher application. A curve is defined by two or more points, so storing these in a list would be a good method of handling them. You first need to define a CList collection class object as a member of the CCurve class. You’ll use this collection to store points. You’ve already looked at the CList template class in some detail, so this should be easy.

The CList template class has two parameters, so the general form of declaring a collection class of this type is:

```
CList<YourObjectType, FunctionArgType> ClassName;
```

The first argument, YourObjectType, specifies the type of object that you want to store in the list. The second argument specifies the argument type to be used in function members of the collection class when referring to an object. This is usually specified as a reference to the object type to minimize copying

of arguments in a function call. Declare a collection class object to suit your needs in the CCurve class as:

```
class CCurve: public CElement
{
    // Rest of the class definition...

protected:
    CCurve(void);                    // Default constructor - should not be used
    CList<CPoint, CPoint&> m_PointList;  // Type safe point list
};
```

You can either add this manually to the class definition or use the Add > Add Variable menu item that you’ve used before from Class View. I have omitted the rest of the class definition here because you’re not concerned with it for now. The collection declaration is shaded. It declares the collection m_PointList that stores CPoint objects in the list, and its functions use reference arguments to CPoint objects.

The CPoint class doesn’t allocate memory dynamically, so you won’t need to implement ConstructElements() or DestructElements(), and because you don’t need to use the Find() member function, you can forget about CompareElements() as well.

## Drawing a Curve

Drawing a curve is different from drawing a line or a circle. With a line or a circle, as you move the cursor with the left button down, you are creating a succession of different line or circle elements that share a common reference point — the point where the left mouse button was pressed. This is not the case when you draw a curve, as shown in Figure 15-5.

![](img/2359b0c604600c58fba3539c738a356e_815_0.png)

Figure 15-5

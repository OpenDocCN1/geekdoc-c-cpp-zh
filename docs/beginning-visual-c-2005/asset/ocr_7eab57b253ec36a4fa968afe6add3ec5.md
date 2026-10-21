# Creating the Document and Improving the View

![](bbox=[0.21, 0.11, 0.84, 0.56])

Figure 15-3

You can use a value of type POSITION to retrieve the object at a given position in the list by using the GetNext() function. Note that you can’t perform arithmetic on values of type POSITION — you can only modify a position value through member functions of the list object. Furthermore, you can’t set a position value to a specific numerical value. POSITION variables can only be set through member functions of the list object.

As well as returning the object, the GetNext() function increments the position variable passed to it so that it points to the next object in the list. You can, therefore, use repeated calls to GetNext() to step through a list element by element. The position variable is set to NULL if you use GetNext() to retrieve the last object from the list, so you can use this to control your loop operation. You should always make sure that you have a valid position value when you call member functions of a list object.

You can insert an element in a list at a specific position as long as you have a POSITION value. To insert the object ThePoint in the list PointList immediately before an element at the position aPosition, use the statement:

```
PointList.InsertBefore(aPosition, ThePoint);
```

The function InsertBefore() also returns the position of the new object. To insert an element after the object at a given position, the function InsertAfter() is provided. These functions are often used with a list containing geometric elements displayed. Elements are drawn on the screen in the sequence that you traverse the list. Elements that appear later in the list overlay elements positioned earlier, so the
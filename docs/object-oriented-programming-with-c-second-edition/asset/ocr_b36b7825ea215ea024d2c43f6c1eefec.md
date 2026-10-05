# Object-Oriented Programming with C++

Let us consider a function that copies and pastes a graphics object to a different place of the window. See Listing 6.26.

**Listing 6.26** An example to illustrate the use of the clone function

```
void MyWindow::copyPaste(const Shape * const p,
    unsigned int x, unsigned int y)
{
    Shape * q;
    q=p->clone();
    q->move(x,y);
    q->show();
    // to attach the new object to the list
    // of current objects on the screen
}
```

The pointer 'p' points at the object being copied. The variables 'x' and 'y' are the coordinates of the place where the copied object is to pasted. Although 'p' might point at an object of any of the classes that are derived from the Shape class, the entire operation of copying and pasting works in all cases. The only precondition is that the classes that are derived from the Shape class must define the clone() function, the move() function, and the show() function. This is easily ensured by declaring all these functions as virtual functions in the Shape class. An additional point to be noted in this specific example is that the clone object should not be destroyed. Instead, it should be added to the list of existing objects on the screen.

# Summary

Generic code contained in the functions of the base class remains inextensible without the use of virtual functions. Virtual functions make expected overrides in the derived class. Marking a base class function as a virtual function ensures its override in the derived class.
An abstract class is a class that has at least one pure virtual function. An abstract class cannot be instantiated. Virtual destructors ensure a proper cleanup operation if the 'delete' operator is applied on a base class pointer that points at a derived class object.

Although we cannot have virtual constructors, clone functions that construct virtually can be used instead. A class function returns an exact copy of the object at which the base class, with respect to it is called. If the pointer points at a base class object, the clone function creates an object of the base class and returns a pointer to it. If the pointer points at a derived class object, the clone function creates an object of the derived class and returns a pointer to it.

# Key Terms

+   - virtual functions
- extending class libraries by using virtual functions
- pure virtual functions

+   - abstract base class
- virtual destructors
- clone functions

composition. We have seen this in our link-based implementations of an ADT. For example, when an instance of LinkedBag, LinkedStack, or LinkedList is destroyed, the nodes used to store the container’s objects are no longer needed and are destroyed also. In the array-based implementations of our ADTs, the array containing the items is destroyed.

Another form of containment is aggregation. In an aggregate relationship the contained item can exist independently of the containing class. Our PlainBox class has an instance of ItemType named item. If our plain box is destroyed, the program can continue to use item. Another example of aggregation can be found in the implementations of our ADT bag, ADT stack, and ADT list: The items stored in a bag, stack, or list continue to exist even after we are finished using the container and it has been destroyed.

Programming Tip: Favor containment over inheritance. Use public inheritance when an is-a relationship exists, that is, when an instance of a derived class can substitute for an instance of the base class. Use private inheritance when you want to reuse a part of another class’s implementation.

Note: Containment and the execution order of constructors and destructors The constructors for a class’s member objects execute in the order listed in the class definition before the class’s constructor. For example, Ball’s constructor executes before Pen’s constructor. The destructors of a class’s member objects execute after the class’s destructor. For example, Ball’s destructor executes after Pen’s.

Note: Execution order of constructors and destructors
Considering both inheritance and containment, a class’s constructors execute in the following order:
- Its base class constructor executes.
- Constructors of its member objects execute in the declaration order.
- The body of its constructor executes.
A class’s destructors execute in the opposite order:
- The body of its destructor executes.
- Destructors of its member objects execute in the declaration order.
- Its base class destructor executes.

## C4.3 Abstract Base Classes Revisited

Imagine a CD player (CDP) and a DVD player (DVDP). Both devices share several characteristics. Each involves a compact disc. You can insert, remove, play, and stop such discs. You can also skip forward or skip backward from the current position on the disc. Some of these operations are essentially the same for both devices, while others—in particular, the play operation—are different but similar.
If you were specifying both devices, you might begin by describing the common operations.

```
// Inserts a disc into the player:
+insert()
// Removes a disc from the player:
+remove()
// Plays the disc.
+play()
// Stops playing the disc.
+stop()
// Skips ahead to another section of the disc.
+skipForward()
// Skips back to an earlier section of the disc.
+skipBackward()
```

These operations could constitute a generic disc player (GDP).
If GDP, CDP, and DVDP were classes, GDP could be the base class of CDP and DVDP, as Figure C4-9 illustrates. While GDP could implement operations such as `insert` and `remove` that would be suitable for both a CDP and a DVDP, it could only indicate that these devices have a `play` operation. So CDP, for example, inherits the operations provided by GDP but overrides the `play` operation to suit CDs, as Figure C4-10 illustrates. If necessary, CDP could override any of GDP's operations or define additional ones. We can make similar comments about DVDP. Thus,

- A CDP is a GDP that plays sound.
- A DVDP is a GDP that plays sound and video.

Because GDP cannot implement its `play` operation, we would not want instances of it. So GDP is simply a class without instances that forms the basis of other classes. If a class never has instances, its methods need not be implemented. Such methods, however, must be virtual so that derived classes can supply their own implementations. A virtual method with an undefined body is called a **pure virtual method** and is written as

A pure virtual method has an undefined body

```cpp
virtual prototype = 0;
```

within a class definition. The implementation of a pure virtual method is deferred to a derived class.

### FIGURE C4-9 CDP and DVDP have an abstract base class

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_370_0.png)

### FIGURE C4-10 CDP and DVDP are derived from GDP

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_371_0.png)

> A class that contains at least one pure virtual method is an abstract base class

Chapter 1 defined an abstract base class as a class that contains at least one virtual method that has no implementation. We can now restate that definition as a class that contains at least one pure virtual method. An abstract base class has no instances and is used only as the basis of other classes. Thus, the GDP class is an abstract base class, because it does not implement all of its methods. Any derived class that fails to implement all of the pure virtual methods is also an abstract base class and cannot have instances.

An abstract base class can provide a constructor, which cannot be pure because constructors cannot be virtual. A destructor in an abstract base class should not be pure, because derived classes will call it, and thus, it should be implemented even if it simply has an empty body. Generally, virtual destructors are recommended.

> An abstract base class has descendants but no instances

As you have seen, an abstract base class is a great place to specify an ADT. By defining the methods that make up the ADT’s public interface as pure virtual methods, we force any derived class to implement these methods, ensuring a common interface across implementations. For example, Listing C4-3 contains the abstract base class for boxes from C++ Interlude 1 with the addition of a virtual destructor.

### LISTING C4-3 An abstract class that is an interface for the ADT box

```cpp
template <class ItemType>
class BoxInterface
{
public:
   virtual ~BoxInterface() {} // Empty implementation
   virtual void setItem(const ItemType& theItem) = 0;
   virtual ItemType getItem() const = 0;
}; // end BoxInterface
```

We can indicate that our class PlainBox is derived from BoxInterface by changing its class header to `class PlainBox : public BoxInterface<ItemType>`

We can also define a new class, JewelryBox, that provides an alternate implementation of the methods in BoxInterface. Its class header would be `class JewelryBox : public BoxInterface<ItemType>`

Figure C4-11 shows the family of box classes.

### FIGURE C4-11 UML class diagram of the family of box classes

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_372_0.png)

If we define several pointer variables of type BoxInterface, we can have them point to instances of any of the derived classes:

```cpp
BoxInterface<string>* someBoxPtr = new PlainBox<string>("Ace");
BoxInterface<string>* anotherBoxPtr = new JewelryBox<string>("Emerald");
BoxInterface<string>* funBoxPtr = new MagicBox<string>("Stone");
```

For each of the objects created, we can call the setItem or getItem method, and the implementation specific to the instantiated class will execute, even though the pointers are of type BoxInterface:

```cpp
cout << someBoxPtr->getItem() << endl; // Uses PlainBox getItem
cout << anotherBoxPtr->getItem() << endl; // Uses JewelryBox getItem
cout << funBoxPtr->getItem() << endl; // Uses MagicBox getItem, which
// is PlainBox getItem
```

The key points about abstract base classes are summarized next.

> **Note: Abstract base classes**
>
> An abstract base class:
>
> - By definition is a class that contains at least one pure virtual method.
> - Is used only as the basis for derived classes and thus defines a minimum interface for its descendants.
> - Has no instances.
> - Should, in general, omit implementations except for the destructor and methods that provide access to private data members. That is, virtual methods in an abstract base class usually should be pure.
> - Must implement any virtual method that is not pure, thereby providing a default implementation if a derived class chooses not to supply its own.

composition. We have seen this in our link-based implementations of an ADT. For example, when an instance of LinkedBag, LinkedStack, or LinkedList is destroyed, the nodes used to store the container’s objects are no longer needed and are destroyed also. In the array-based implementations of our ADTs, the array containing the items is destroyed.

Another form of containment is **aggregation**. In an aggregate relationship the contained item can exist independently of the containing class. Our PlainBox class has an instance of ItemType named item. If our plain box is destroyed, the program can continue to use item. Another example of aggregation can be found in the implementations of our ADT bag, ADT stack, and ADT list: The items stored in a bag, stack, or list continue to exist even after we are finished using the container and it has been destroyed.

> **Programming Tip:** Favor containment over inheritance. Use public inheritance when an *is-a* relationship exists, that is, when an instance of a derived class can substitute for an instance of the base class. Use private inheritance when you want to reuse a part of another class’s implementation.

> **Note: Containment and the execution order of constructors and destructors**
> The constructors for a class’s member objects execute in the order listed in the class definition before the class’s constructor. For example, Ba11’s constructor executes before Pen’s constructor. The destructors of a class’s member objects execute after the class’s destructor. For example, Ba11’s destructor executes after Pen’s.

> **Note: Execution order of constructors and destructors**
> Considering both inheritance and containment, a class’s constructors execute in the following order:
> 1. Its base class constructor executes.
> 2. Constructors of its member objects execute in the declaration order.
> 3. The body of its constructor executes.
> A class’s destructors execute in the opposite order:
> 1. The body of its destructor executes.
> 2. Destructors of its member objects execute in the declaration order.
> 3. Its base class destructor executes.

# ## C4.3 Abstract Base Classes Revisited

Imagine a CD player (CDP) and a DVD player (DVDP). Both devices share several characteristics. Each involves a compact disc. You can insert, remove, play, and stop such discs. You can also skip forward or skip backward from the current position on the disc. Some of these operations are essentially the same for both devices, while others—in particular, the play operation—are different but similar.

If you were specifying both devices, you might begin by describing the common operations.

```
// Inserts a disc into the player:
+insert()
```
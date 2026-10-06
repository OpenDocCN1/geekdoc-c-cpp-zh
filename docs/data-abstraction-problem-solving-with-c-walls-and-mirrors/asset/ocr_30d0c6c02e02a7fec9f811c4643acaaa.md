# CHAPTER 4 Link-Based Implementations

```
while (headPtr != nullptr)
{
    Node<ItemType>* nodeDeletePtr = headDeletePtr;
    headPtr = headPtr->getNext();
    // Return the node to the system
    nodeToDeletePtr->setNext(nullptr);
    delete nodeToDeletePtr;
} // end while
headPtr = nullptr;
}

nodeToDeletePtr = nullptr;
itemCount = 0;
} // end clear
```

You must write a destructor if your class allocates memory dynamically

Each class has only one destructor. The destructor destroys an instance of the class, which is an object, when the object's lifetime ends. Typically, the destructor is invoked at the end of the block in which the object was created.
Classes that use statically allocated memory depend on the compiler-generated destructor, as was the case with ArrayBag in Chapter 3. However, when a class uses dynamically allocated memory, you need to write a destructor that deallocates this memory by using delete. The destructor for LinkedBag can simply call the method to delete each node in the link containing the bag's entries. The destructor's definition follows:

```
template ~Class<ItemType>
LinkedBag<ItemType>::~LinkedBag()
{
    clear();
} // end destructor
```

A destructor's name is a tilde~) followed by the class name. A destructor cannot have arguments, and has no return type—even void—and cannot return a value.

> Question 13 Revise the destructor in the LinkedBag so that it does not call clear, but instead directly deletes each node of the underlying linked chain.

![](bbox=[0.222, 0.611, 0.263, 0.653])

The copy constructor. The second constructor in LinkedBag is the copy constructor:

```
LinkedBag(const LinkedBag<ItemType>& a_bag);
```

The copy constructor makes a copy of an object. It is invoked implicitly when you either pass an object to a function by value, return an object from a valued function, or define and initialize an object, as in

```
LinkedBag bag(bag);
```

where bag exists already.
When copying an object involves copying the values of its data members, the copy is called a shallow copy. If a shallow copy is sufficient, you can omit the copy constructor, in which case the compiler generates a copy constructor that performs a shallow copy. Such was the case in Chapter 3 for the ArrayBag, although we did not mention it. Array-based implementation of the ADT bag used by a compiler-generated copy constructor to copy both the array of bag items and the number of items.

Situations that invoke the copy constructor

A compiler-generated copy constructor performs a shallow copy
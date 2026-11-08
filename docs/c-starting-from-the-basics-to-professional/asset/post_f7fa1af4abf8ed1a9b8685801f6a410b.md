
```cpp
export using SharedBox = std::shared_ptr<Box>;

export class Truckload
{
public:
    // Exact same public members as before,
    // only this time without getFirstBox() and getNextBox()...

    class Iterator;    // Declaration of a public nested class, Truckload::Iterator

    Iterator getIterator() const;

private:
    class Package;     // Declaration of a private nested class, Truckload::Package

    Package* m_head {};  // First in the list
    Package* m_tail {};  // Last in the list
};

// Out-of-class definition of the nested Iterator class (part of the module interface)
class Truckload::Iterator
{
public:
    SharedBox getFirstBox();  // Get the first Box
    SharedBox getNextBox();   // Get the next Box

private:
    Package* m_head;          // The head of the linked list (needed for getFirstBox())
    Package* m_current;       // The package whose Box was last retrieved

    friend class Truckload;   // Only a Truckload can create an Iterator
    explicit Iterator(Package* head) : m_head{head}, m_current{nullptr} {}
};

// Out-of-class definition of the nested Package class (implementation detail)
class Truckload::Package
{
public:
    SharedBox m_box;    // Pointer to the Box object contained in this Package
    Package* m_next;    // Pointer to the next Package in the list

    Package(SharedBox box) : m_box{box}, m_next{nullptr} {}  // Constructor
    ~Package() { delete m_next; }                            // Destructor
};
```

Defining nested classes (or member classes) out-of-class is analogous to defining other members out-of-class: all you need to remember is to prefix the member name (in this case Iterator or Package) with the name of the containing class (Truckload) followed by two colons. In fact, because Package is only required within the definition of other members, you could move its definition into an implementation file together with that of these other members. The definition of the Iterator class, however, should be part of the module interface; the consumers of the module need it to traverse a Truckload's contents.

Here is the definition of the getIterator() member:

```cpp
Truckload::Iterator Truckload::getIterator() const { return Iterator(m_head); }
```

There are two things worth noting here. First, the function's return type, Truckload::Iterator, must be prefixed with Truckload:: as well. Only within the function body or parameter list is this not required. And, second, because we defined Iterator out-of-class, the definition of the getIterator() member must be out-of-class as well, and put after that of Iterator. The reason is that the body of getIterator() needs the definition of the Iterator class to invoke its constructor. Of course, we start the iteration at the head of the linked list.

The m_current, getFirstBox(), and getNextBox() members have been moved from Truckload into its nested Iterator class. Both functions are implemented in the same manner as before, except that now they no longer update the m_current member variable of a Truckload object. Instead, they operate using the m_current member of an Iterator object specifically created to traverse this Truckload by getIterator(). As multiple Iterators can exist at the same time for a single Truckload, each with their own m_current pointer, both nested and concurrent traversals of the same Truckload become possible. Moreover, and more importantly, creating an iterator does not modify a Truckload, so getIterator() can be a const member function. This allows us to properly implement the findLargestBox() function from earlier with a reference-to-const-Truckload parameter:

```cpp
SharedBox findLargestBox(const Truckload& truckload)
{
    auto iterator{ truckload.getIterator() };    // Type of iterator is Truckload::Iterator
    SharedBox largestBox{ iterator.getFirstBox() };

    SharedBox nextBox{ iterator.getNextBox() };
    while (nextBox)
    {
        if (nextBox->compare(*largestBox) > 0)
            largestBox = nextBox;
        nextBox = iterator.getNextBox();
    }

    return largestBox;
}
```

We'll leave the completion of this example to you as an exercise (see Exercise 12-6). Before we conclude the chapter, though, let's first take a closer look at the access rights within the definition of Truckload and its nested classes. Iterator is a nested class of Truckload, so it has the same access privileges as Truckload member functions. This is fortunate because otherwise it couldn't have used the nested Package class, which is declared to be for private use only within the Truckload class. Naturally, Iterator itself must be a public nested class; otherwise, code outside of the class would not be able to use it. Notice that we did decide to make the primary constructor of the Iterator class private, however, because external code cannot (it never has access to any Package objects) and should not create Iterators that way. Only the getIterator() function will be creating Iterators with this constructor. For it to access this private constructor, however, we need a friend declaration. Even though you can access private members of the outer class from within a nested class, the same does not hold in the other direction. That is, an outer class has no special privileges when it comes to accessing the members of an inner class. It is treated like any other external code. Without the friend declaration, the getIterator() function would therefore not have been allowed to access the private constructor of the nested Iterator class.

> **Note**  Even though external code cannot create a new `Iterator` using our private constructor, it does remain possible to create a new `Iterator` object as a copy of an existing one. The default copy constructor generated by the compiler remains public.

## Summary

In this chapter, you learned the basic ideas involved with defining and using class types. However, although you covered a lot of ground, this is just the start. There's a great deal more to implementing the operations applicable to a class object, and there are subtleties in this too. In subsequent chapters, you'll be building on what you learned here, and you'll see more about how you can extend the capabilities of your classes. In addition, you'll explore more sophisticated ways to use classes in practice. The key points to keep in mind from this chapter are as follows:

- A class provides a way to define your own data types. Classes can represent whatever types of objects your particular problem requires.
- A class can contain *member variables* and *member functions*. The member functions of a class always have free access to the member variables of the same class.
- Objects of a class are created and initialized using member functions called *constructors*. A constructor is called automatically when an object declaration is encountered. Constructors can be overloaded to provide different ways of initializing an object.
- A copy constructor is a constructor for an object that is initialized with an existing object of the same class. The compiler generates a default copy constructor for a class if you don't define one.
- Members of a class can be specified as public, in which case they are freely accessible from any function in a program. Alternatively, they can be specified as private, in which case they may be accessed only by member functions, friends of the class, or members of nested classes.
- Member variables of a class can be static. Only one instance of each static member variable of a class exists, no matter how many objects of the class are created.
- Although static member variables of a class are accessible in a member function of an object, they aren't part of the object and don't contribute to its size.
- Every non-static member function contains the pointer `this`, which points to the current object for which the function is called.
- Static member functions can be called even if no objects of the class have been created. A static member function of a class doesn't contain the pointer `this`.
- `const` member functions can't modify the member variables of a class object unless the member variables have been declared as `mutable`.
- Using references to class objects as arguments to function calls can avoid substantial overheads in passing complex objects to a function.

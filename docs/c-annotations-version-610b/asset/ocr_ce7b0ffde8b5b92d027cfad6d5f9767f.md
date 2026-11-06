# 14.12  Virtual constructors

In section 14.2 we learned that C++ supports *virtual destructors*. Like many other object oriented languages (e.g., Java), however, the notion of a *virtual constructor* is not supported. Not having virtual constructors becomes a liability when only base class references or pointers are available, and a copy of a derived class object is required. Gamma *et al.* (1995) discuss the *Prototype design pattern* to deal with this situation.

According to the *Prototype Design Pattern* each derived class is given the responsibility of implementing a member function returning a pointer to a copy of the object for which the member is called. The usual name for this function is clone. Separating the user interface from the reimplementation interface clone is made part of the interface and newCopy is defined in the reimplementation interface. A base class supporting “cloning” defines a virtual destructor, clone, returning newCopy’s return value and the *virtual copy constructor*, a pure virtual function, having the prototype `virtual Base * newCopy() const = 0`. As newCopy is a pure virtual function all derived classes must now implement their own ‘virtual constructor’.

This setup suffices in most situations where we have a pointer or reference to a base class, but it fails when used with abstract containers. We can’t create a `vector<Base>`, with Base featuring the pure virtual copy member in its interface, as Base is called to initialize new elements of such a vector. This is impossible as newCopy is a pure virtual function, so a Base object can’t be constructed.

The intuitive solution, providing newCopy with a default implementation, defining it as an ordinary virtual function, fails too as the container calls Base (Base const & other), which would have to call newCopy to copy other. At this point it is unclear what to do with that copy, as the new Base object already exists, and contains no Base pointer or reference data member to assign newCopy’s return value to.

Alternatively (and preferred) the original Base class (defined as an abstract base class) is kept as-is and a wrapper class Clonable is used to manage the Base class pointers returned by newCopy. In chapter 17 ways to merge Base and Clonable into one class are discussed, but for now we’ll define Base and Clonable as separate classes.

The class Clonable is a very standard class. It contains a pointer member so it needs a copy constructor, destructor, and overloaded assignment operator. It’s given at least one non-standard member: `Base & base() const`, returning a reference to the derived object to which Clonable’s `Base * data` member refers. It is also provided with an additional constructor to initialize its `Base * data` member.

Any non-abstract class derived from Base must implement `Base *newCopy()`, returning a pointer to a newly created (allocated) copy of the object for which newCopy is called.

Once we have defined a derived class (e.g., Derived1), we can put our Clonable and Base facilities to good use. In the next example we see main defining a vector<Clonable>. An anonymous Derived1 object is then inserted into the vector using the following steps:

+   - A new anonymous `Derived1` object is created;
+   - It initializes a `Clonable` using `Clonable(Base *bp)`;
+   - The just created `Clonable` object is inserted into the vector, using `Clonable`’s move constructor. There are only temporary Derived and Clonable objects at this point, so no copy construction is required.

In this sequence, only the Clonable object containing the `Derived1 *` is used. No additional copies need to be made (or destroyed).

Next, the base member is used in combination with `typeof` to show the actual type of the Base & object: a Derived1 object.

Main then contains the interesting definition `vector<Clonable> v2(bv)`. Here a copy of bv is created. This copy construction observes the actual types of the Base references, making sure that the appropriate types appear in the vector’s copy.
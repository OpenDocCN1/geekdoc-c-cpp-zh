
# Member Functions and Data

> **Cross-Reference** For more discussion of routines in general, see Chapter 7, “High-Quality Routines.”

Here are a few guidelines for implementing member functions and member data effectively.

**Keep the number of routines in a class as small as possible** A study of C++ programs found that higher numbers of routines per class were associated with higher fault rates (Basili, Briand, and Melo 1996). However, other competing factors were found to be more significant, including deep inheritance trees, large number of routines called within a class, and strong coupling between classes. Evaluate the tradeoff between minimizing the number of routines and these other factors.

**Disallow implicitly generated member functions and operators you don’t want** Sometimes you’ll find that you want to disallow certain functions—perhaps you want to disallow assignment, or you don’t want to allow an object to be constructed. You might think that, since the compiler generates operators automatically, you’re stuck allowing access. But in such cases you can disallow those uses by declaring the constructor, assignment operator, or other function or operator *private*, which will prevent clients from accessing it. (Making the constructor private is a standard technique for defining a singleton class, which is discussed later in this chapter.)

**Minimize the number of different routines called by a class** One study found that the number of faults in a class was statistically correlated with the total number of routines that were called from within a class (Basili, Briand, and Melo 1996). The same study found that the more classes a class used, the higher its fault rate tended to be. These concepts are sometimes called “fan out.”

> **Further Reading** Good accounts of the Law of Demeter can be found in *Pragmatic Programmer* (Hunt and Thomas 2000), *Applying UML and Patterns* (Larman 2001), and *Fundamentals of Object-Oriented Design in UML* (Page-Jones 2000).

**Minimize indirect routine calls to other classes** Direct connections are hazardous enough. Indirect connections—such as *account.ContactPerson().DaytimeContactInfo().PhoneNumber()*—tend to be even more hazardous. Researchers have formulated a rule called the “Law of Demeter” (Lieberherr and Holland 1989), which essentially states that Object A can call any of its own routines. If Object A instantiates an Object B, it can call any of Object B’s routines. But it should avoid calling routines on objects provided by Object B. In the *account* example above, that means *account.ContactPerson()* is OK but *account.ContactPerson().DaytimeContactInfo()* is not.

This is a simplified explanation. See the additional resources at the end of this chapter for more details.

**In general, minimize the extent to which a class collaborates with other classes** Try to minimize all of the following:
- Number of kinds of objects instantiated
- Number of different direct routine calls on instantiated objects
- Number of routine calls on objects returned by other instantiated objects

# Constructors

Following are some guidelines that apply specifically to constructors. Guidelines for constructors are pretty similar across languages (C++, Java, and Visual Basic, anyway). Destructors vary more, so you should check out the materials listed in this chapter’s “Additional Resources” section for information on destructors.

**Initialize all member data in all constructors, if possible** Initializing all data members in all constructors is an inexpensive defensive programming practice.

**Enforce the singleton property by using a private constructor** If you want to define a class that allows only one object to be instantiated, you can enforce this by hiding all the constructors of the class and then providing a static `GetInstance()` routine to access the class’s single instance. Here’s an example of how that would work:

> **Further Reading** The code to do this in C++ would be similar. For details, see *More Effective C++*, Item 26 (Meyers 1998).

```
**Java Example of Enforcing a Singleton with a Private Constructor**

```java
public class MaxId {
    // constructors and destructors
    private MaxId() {
        ...
    }
    ...

    // public routines
    public static MaxId GetInstance() {
        return m_instance;
    }
    ...

    // private members
    private static final MaxId m_instance = new MaxId();
    ...
}
```
```

The private constructor is called only when the *static* object *m_instance* is initialized. In this approach, if you want to reference the *MaxId* singleton, you would simply refer to *MaxId.GetInstance()*.

**Prefer deep copies to shallow copies until proven otherwise** One of the major decisions you’ll make about complex objects is whether to implement deep copies or shallow copies of the object. A deep copy of an object is a member-wise copy of the object’s member data; a shallow copy typically just points to or refers to a single reference copy, although the specific meanings of “deep” and “shallow” vary.

The motivation for creating shallow copies is typically to improve performance. Although creating multiple copies of large objects might be aesthetically offensive, it rarely causes any measurable performance impact. A small number of objects might cause performance issues, but programmers are notoriously poor at guessing which code really causes problems. (For details, see Chapter 25, “Code-Tuning Strategies.”)

> Here is the private constructor.

> Here is the public routine that provides access to the single instance.

> Here is the single instance.

Because it’s a poor tradeoff to add complexity for dubious performance gains, a good approach to deep vs. shallow copies is to prefer deep copies until proven otherwise.

Deep copies are simpler to code and maintain than shallow copies. In addition to the code either kind of object would contain, shallow copies add code to count references, ensure safe object copies, safe comparisons, safe deletes, and so on. This code can be error-prone, and you should avoid it unless there’s a compelling reason to create it.

If you find that you do need to use a shallow-copy approach, Scott Meyers’s *More Effective C++*, Item 29 (1996) contains an excellent discussion of the issues in C++. Martin Fowler’s *Refactoring* (1999) describes the specific steps needed to convert from shallow copies to deep copies and from deep copies to shallow copies. (Fowler calls them reference objects and value objects.)

# 6.4 Reasons to Create a Class

If you believe everything you read, you might get the idea that the only reason to create a class is to model real-world objects. In practice, classes get created for many more reasons than that. Here’s a list of good reasons to create a class.

**Model real-world objects** Modeling real-world objects might not be the only reason to create a class, but it’s still a good reason! Create a class for each real-world object type that your program models. Put the data needed for the object into the class, and then build service routines that model the behavior of the object. See the discussion of ADTs in Section 6.1 for examples.

**Model abstract objects** Another good reason to create a class is to model an *abstract object*—an object that isn’t a concrete, real-world object but that provides an abstraction of other concrete objects. A good example is the classic *Shape* object. *Circle* and *Square* really exist, but *Shape* is an abstraction of other specific shapes.

On programming projects, the abstractions are not ready-made the way *Shape* is, so we have to work harder to come up with clean abstractions. The process of distilling abstract concepts from real-world entities is non-deterministic, and different designers will abstract out different generalities. If we didn’t know about geometric shapes like circles, squares and triangles, for example, we might come up with more unusual shapes like squash shape, rutabaga shape, and Pontiac Aztek shape. Coming up with appropriate abstract objects is one of the major challenges in object-oriented design.

**Reduce complexity** The single most important reason to create a class is to reduce a program’s complexity. Create a class to hide information so that you won’t need to think about it. Sure, you’ll need to think about it when you write the class. But after it’s written, you should be able to forget the details and use the class without any knowledge of its internal workings. Other reasons to create classes—minimizing code size,

![](img/649c8eee28c38ca1e062691e45dc9883_188_0.png)

Cross-Reference Reasons for creating classes and routines overlap. See Section 7.1.

Cross-Reference For more on identifying real-world objects, see “Find Real-World Objects” in Section 5.3.

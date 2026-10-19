# Constructors

Following are some guidelines that apply specifically to constructors. Guidelines for constructors are pretty similar across languages (C++, Java, and Visual Basic, anyway). Destructors vary more, so you should check out the materials listed in this chapter’s “Additional Resources” section for information on destructors.

**Initialize all member data in all constructors, if possible**  Initializing all data members in all constructors is an inexpensive defensive programming practice.

**Enforce the singleton property by using a private constructor**  If you want to define a class that allows only one object to be instantiated, you can enforce this by hiding all the constructors of the class and then providing a static `GetInstance()` routine to access the class’s single instance. Here’s an example of how that would work:

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

**Prefer deep copies to shallow copies until proven otherwise**  One of the major decisions you’ll make about complex objects is whether to implement deep copies or shallow copies of the object. A deep copy of an object is a member-wise copy of the object’s member data; a shallow copy typically just points to or refers to a single reference copy, although the specific meanings of “deep” and “shallow” vary.

The motivation for creating shallow copies is typically to improve performance. Although creating multiple copies of large objects might be aesthetically offensive, it rarely causes any measurable performance impact. A small number of objects might cause performance issues, but programmers are notoriously poor at guessing which code really causes problems. (For details, see Chapter 25, “Code-Tuning Strategies.”)

> Here is the private constructor.

> Here is the public routine that provides access to the single instance.

> Here is the single instance.
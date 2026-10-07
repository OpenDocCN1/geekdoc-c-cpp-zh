Chapter 14 Reusing Code in C++

# Containment or Private Inheritance?

Given that you model a has-a relationship with containment or with private inheritance, which should you use? Most C++ programmers prefer containment. First, it's easier to follow. When you look at the class declaration, you see explicitly named objects representing the contained classes, and your code can refer to these objects by name. Using inheritance makes the relationship more abstract. Second, inheritance can raise problems, particularly if a class inherits from more than one class. You may have to deal with issues as separate base classes having methods with the same name or of separate classes sharing a common ancestor. All in all, you're less likely to run into trouble using containment. If a class needs three string objects, you can declare separate string members by using the containment approach. But inheritance limits you to a single object. (It is difficult to tell objects apart when they are nameless.)

However, private inheritance offers features beyond those provided by containment. Suppose, for example, that a class has protected members, which could be either data members or functions. Such members are available to derived classes but not to the world at large. If you include such a class in another by composition, the new class is part of the world at large, not a derived class. Hence it can't access protected members. But using inheritance makes the new class a derived class, so it can access protected members.

Another situation that calls for using inheritance is if you need to redefine functions. Again, this is a privilege accorded to a derived class but not to a containing class. With private inheritance, the redefined functions would be just within the class, not publicly.

> Tip
 general, you should use containment to model a has-a relationship. You should use private inheritance if the new class needs to access protected members in the original class or if it needs to redefine virtual functions.

# Protected Inheritance

Protected inheritance is a variation of private inheritance. It uses the keyword protected when listing a base class:

```
class Student : protected std::string,
    protected std::vector<double>
{...};
```

With protected inheritance, public and protected members of a base class become protected of the derived class. As with private inheritance, the interface for the base class is available to the derived class but not to the outside world. The main difference between private inheritance and protected inheritance occurs when you derive another class from the derived class. With private inheritance, this third-generation class doesn't get the internal use of the base-class interface. That's the public base-class methods become
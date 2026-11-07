members of a class. When we use private data members, data are hidden to entities outside of the class and also to derived classes. On the other hand, using private data members means creating more code in the derived class. Therefore, the advantage of private data members is stronger encapsulation; its disadvantage is creating more code in the derived class. If we are the designer of the base class and want to protect our data members from direct access, we should use private data members.

# Using Protected Data Members

Using protected data members makes the coding of the derived classes simpler. However, it breaks the idea of encapsulation. We will see that sometimes we must use protected data members because the coding becomes very complicated if we use private data members.

# Blocking Inheritance

Sometimes we may want to block inheritance—for example, when we have defined a class (as a designer) and do not want users to inherit from this class and create derived classes. The C++ standard allows us to do so using the `final` modifier, as shown below.

```
```cpp
class First final
{
    ...
}
```
```

We can also use the final modifier to stop the inheritance anywhere in the hierarchy. For example, we may have a derived class from a base class, but we do not want the hierarchy to continue, as shown below.

```
```cpp
class First
{
    ...
}
class Second final : public First
{
    ...
}
```
```

The *Second* class is inherited from the *First* class, but inheritance is blocked here. We do not want someone to try to create another subclass from the *Second* class. The final modifier blocks further inheritance.

# Liskov Substitution Principle (LSP)

A design principle that is sometimes ignored is the **Liskov substitution principle** (LSP), developed by Barbara Liskov. This principle says that an object of a superclass must always be substitutable by an object of a subclass without altering any of the properties of the superclass. We may think of an object as a special kind of another object in real life, but in object-oriented programming, we must check LSP before writing the code.
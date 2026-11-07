that points to memory allocated by new. Then, when a Singer object expires, it’s vital that the `~Singer()` destructor be called to free that memory.

Now consider the following code:

```
Employee * pe = new Singer; // legal because Employee is base for Singer
...
delete pe;                  // ~Employee() or ~Singer()?
```

If the default static binding applies, the delete statement invokes the `~Employee()` destructor. This frees memory pointed to by the Employee components of the Singer object but not memory pointed to by the new class members. However, if the destructors are virtual, the same code invokes the `~Singer()` destructor, which frees memory pointed to by the Singer component, and then calls the `~Employee()` destructor to free memory pointed to by the Employee component.

Note that this implies that even if a base class doesn’t require the services of an explicit destructor, you shouldn’t rely on the default constructor. Instead, you should provide a virtual destructor, even if it has nothing to do:

```
virtual ~BaseClass() { }
```

By the way, it’s not an error for a class to have a virtual destructor even if it is not intended to be a base class; it’s just a matter of efficiency.

> **Tip**
> 
> Normally, you should provide a base class with a virtual destructor even if the class doesn’t need a destructor.

# Friends

Friends can’t be virtual functions because friends are not class members, and only members can be virtual functions. If this poses a problem for a design, you might be able to sidestep it by having the friend function use virtual member functions internally.

# No Redefinition

If a derived class fails to redefine a function (virtual or not), the class will use the base class version of the function. If a derived class is part of a long chain of derivations, it will use the most recently defined version of the function. The exception is if the base versions are hidden, as described next.

# Redefinition Hides Methods

Suppose you create something like the following:

```
class Dwelling
{
public:
    virtual void showperks(int a) const;
...
};
class Hovel : public Dwelling
```
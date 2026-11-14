base class method/operator with the same name and a different signature is a detail that even experienced programmers do not immediately think of when being confronted with unexpected behavior.

# 6.1.3.4 Abstract Classes

So far we have looked only at examples where a `virtual` function was defined in a base class and then expanded in derived classes. Sometimes we find ourselves in a situation where we have an ensemble of classes with some common functions and need a common super-class to select the classes dynamically. For instance, in Section 6.4, we will introduce solvers that provide the same interface: a `solve` function. To select them at run time, they need to share a super-class with a `solve` function. However, there is no universal `solve` algorithm that we can override later. For that purpose, we need a new feature to state: “I have a `virtual` function in this class without implementation; this will come later in sub-classes.”

# **Definition 6-3.** (Pure Virtual Function and Abstract Class). A `virtual` function is a *Pure Virtual Function* when it is declared with = 0. A class containing a pure virtual function is called an *Abstract Class*.

```
=> c++11/oop_abstract.cpp
```

To be more specific, we expand our `person` example with an abstract super-class `creature`:

Click here to view code image

```
class creature
{
    public:
    virtual void all_info() const= 0; // purely virtual
    virtual ~creature() = default;
};

class person
    : public creature
{ ... };

int main()
{
    creature some_beast; // Error: abstract class
}
```
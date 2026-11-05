# 13.4.7 Abstract Classes and Interfaces

Like a nonabstract class, an abstract class must provide implementations of all members of the interfaces that are listed in the base class list of the class. However, an abstract class is permitted to map interface methods onto abstract methods. For example:

```
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    public abstract void F();
    public abstract void G();
}
```

Here, the implementation of IMethods maps F and G onto abstract methods, which must be overridden in nonabstract classes that derive from C.

Note that explicit interface member implementations cannot be abstract, but explicit interface member implementations are, of course, permitted to call abstract methods. For example:

```
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    void IMethods.F() { FF(); }
    void IMethods.G() { GG(); }
    protected abstract void FF();
    protected abstract void GG();
}
```

Here, nonabstract classes that derive from C would be required to override FF and GG, thus providing the actual implementation of IMethods.
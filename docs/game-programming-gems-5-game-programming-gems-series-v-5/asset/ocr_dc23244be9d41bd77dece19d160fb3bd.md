we can add support for child factories, meaning we can connect factories in a hierarchical fashion to affect object creation in one simple way. If a factory does not know how to create the object we requested, we recursively descend its children until we find a child factory that does know how to create the object. For this support, we extend the factory class as follows:

```
struct Factory
{
    void RemoveChild(Factory* factory);
    void AddChild(Factory* factory);
};
```

Through these two new methods, our factory class can now maintain a list of pointers to child class objects (constructors). In this implementation, there is no support for cases where a child factory is destroyed elsewhere but is still referenced by another factory object. The system could be extended to cope with such circumstances by adding reference counting functionality (or some similar safety net) to the factory classes.

# DLL Factories.

For the Microsoft Windows operating system, we can enhance our factories even further to support the concept of dynamically loadable factories using Dynamic Link Libraries (DLLs). We achieve this by creating a class, DLLFactory, derived from Factory, that wraps the loading of the DLLs and binding to the factories exposed through them. The DLLs only have to export a function to return a pointer to the factory object to be exposed. Remember multiple factories can be exposed from a DLL by the use of child factories.

The implementation can be found in the supplied source code in the file, DLL-Factory.hpp, and an example of its use in the supplied example workspace. Note that care must be taken if the factory DLL is to be unloaded. Objects created using the DLL may still be around, which will result in access violations. Objects created through a DLL factory must also be released by that DLL, so the base class from which all factory creatable objects are derived should provide a method of self-deletion. An implementation of this typically follows the form:

```
struct Base
{
    void DeleteThis()
    {
        delete this;
    }
};
```

More complicated and robust functionality in such circumstances could be added by requiring the factory objects to track and play a more active part in the lifetime of the objects they create, but that is beyond the scope of this gem.
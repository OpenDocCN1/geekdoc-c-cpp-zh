# An interface named IGenericPersistable<> that uses generics

```
interface IGenericPersistable<T{
    T Read(string id);
    bool Save(T obj);
    bool HasChanges
    {
        get;
        set;
    }
}
```

# A class that implements the IGenericPersistable<> interface

```
class Customer : IGenericPersistable<Customer>
{
    # other members
    #region IGenericPersistable<Customer> Members
    public Customer Read(string id)
{
        throw new Exception("The method or operation is not implemented.");
    }
    public bool Save(Customer obj)
{
        throw new Exception("The method or operation is not implemented.");
    }
    public bool HasChanges
    {
        get{
            throw new Exception("The property is not implemented.");
        }
        set{
            throw new Exception("The property is not implemented.");
        }
    }
    #endregion
}
```

# Defining

+   - When defining an interface, you can use generics, just as you do when defining a class that uses generics.
- When implementing a generic interface that you defined, you can specify the type argument, just as you do when implementing generic interfaces from the .NET Framework.

Figure 15-12 How to code an interface that uses generics
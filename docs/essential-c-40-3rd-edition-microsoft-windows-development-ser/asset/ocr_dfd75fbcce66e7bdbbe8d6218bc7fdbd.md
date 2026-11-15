```
}
ICollection<Phone> IContainer<Phone>.Items
{
    get{...}
    set{...}
}
ICollection<Email> IContainer<Email>.Items
{
    get{...}
    set{...}
}
}
```

In this example, the Items property appears multiple times using an explicit interface implementation with a varying type parameter. Without generics, this is not possible, and instead, the compiler would allow only one explicit IContainer.Items property.

One possible improvement on Person would be to also implement IContainer<object> and to have items return the combination of all three containers (Address, Phone, and Email).

# Defining a Constructor and a Finalizer

Perhaps surprisingly, the constructor and destructor on a generic do not require type parameters in order to match the class declaration (in other words, not Pair<T>({...}). In the pair example in Listing 11.11, the constructor is declared using public Pair(T first, T second).

# LISTING 11.11: Declaring a Generic Type's Constructor

```
public struct Pair<T>: IPair<T>
{
    public Pair(T first, T second)
    {
        _Second = second;
        _Second = second;
    }

    public T First
    {
        get{ return _First; }
        set{ _First = value; }
    }
    private T _First;

    public T Second
```
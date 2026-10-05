Click here to view code image

```
class Mammal // base class
{
    public Mammal(string name) // constructor for base class
    {
        ...
    }
    ...
}
class Horse : Mammal // derived class
{
    public Horse(string name)
        : base(name) // calls Mammal(name)
    {
        ...
    }
    ...
}
```

If you don’t explicitly call a base-class constructor in a derived-class constructor, the compiler attempts to silently insert a call to the base class’s default constructor before executing the code in the derived-class constructor. Taking the earlier example, the compiler rewrites this as follows:

Click here to view code image

```
class Horse : Mammal
{
    public Horse(string name)
    {
        ...
    }
    }
```

as this:

Click here to view code image

```
class Horse : Mammal
{
    public Horse(string name)
        : base()
    {
        ...
    }
}
```
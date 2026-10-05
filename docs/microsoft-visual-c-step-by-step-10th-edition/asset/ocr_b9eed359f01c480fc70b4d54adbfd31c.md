The derived class inherits from the base class, and the methods in the base class become part of the derived class.

In C#, a class can derive from at most one base class; a class cannot derive from two or more classes. However, DerivedClass is declared as sealed, unless you can use the same syntax to derive other classes that inherit from DerivedClass. (You’ll learn about sealed classes in Chapter 13, "Creating interfaces and defining abstract classes.")

Click here to view code image

```
class DerivedSubClass : DerivedClass
{
}

```

Continuing the example described earlier, you could declare the Mammal class as follows. The methods Breathe and SuckleYoung are common to all mammals.

Click here to view code image

```
class Mammal
{
    public void Breathe()
    {
        ...
    }

    public void SuckleYoung()
    {
        ...
    }
}

```

You could define classes for each different type of mammal, adding more methods as necessary, as is in the following example:

Click here to view code image

```
class Horse : Mammal
{
    ...
    public void Trot()
    {
        ...
    }
}

```
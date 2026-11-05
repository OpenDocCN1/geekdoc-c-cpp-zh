View Demo

# Now what if we call the Dog's constructor with a parameter?

```
Dog dog = new Dog("Rex");
```

You know that members in the parent class which are not private are inherited by the child class, meaning that Dog will also have the name field.

In this case we passed an argument to our constructor. It in his turn passes the argument to the parent class' constructor with a parameter, which initializes the name field.

Output will be

```
Animal's constructor with 1 parameter
Rex
Dog's constructor with 1 parameter
Rex
```

# Summary:

Every object creation starts from the base class. In the inheritance, the classes which are in the hierarchy are chained. As all classes derive from Object, the first constructor to be called when any object is created is the Object class constructor; Then the next constructor in the chain is called and only after all of them are called the object is created

# base keyword

+   1. The base keyword is used to access members of the base class from within a derived class:
+   2. Call a method on the base class that has been overridden by another method. Specify which base-class constructor should be called when creating instances of the derived class.

# Section 58.2: Inheriting from a base class

To avoid duplicating code, define common methods and attributes in a general class as a base:

```
public class Animal
{
    public string Name { get; set; }
    // Methods and attributes common to all animals
    public void Eat(Object dinner)
    {
        // ...
    }
    public void Stare()
    {
        // ...
    }
    public void Roll()
    {
        // ...
    }
}
```

Now that you have a class that represents Animal in general, you can define a class that describes the peculiarities of specific animals:
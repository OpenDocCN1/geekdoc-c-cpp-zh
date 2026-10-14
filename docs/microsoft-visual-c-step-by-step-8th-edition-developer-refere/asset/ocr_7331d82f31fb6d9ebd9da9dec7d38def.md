and you need to perform additional logic when assigning values), existing applications will not be able to use the updated version of the class without being recompiled. This is awkward if you have deployed the application on a large number of devices throughout an organization. There are ways around this, but it is generally better to avoid getting into this situation in the first place.

# Compatibility with interfaces

If you are implementing an interface and the interface defines an item as a property, you must write a property that matches the specification in the interface, even if the property just reads and writes data in a private field. You cannot implement a property simply by exposing a public field with the same name.

The designers of the C# language recognized that programmers are busy people who should not have to waste their time writing more code than they need to. To this end, the C# compiler can generate the code for properties automatically, like this:

Click here to view code image

```
class Circle
{
    public int Radius{ get; set; }
    ...
}
```

In this example, the Circle class contains a property named Radius. Apart from the type of this property, you have not specified how this property works—the get and set accessors are empty. The C# compiler converts this definition to a private field and a default implementation that looks similar to this:

Click here to view code image

```
class Circle
{
    private int _radius;
    public int Radius{
        get
        {
            return this._radius;
        }
        set
        {
            this._radius = value;
        }
    }
    ...
}
```

So for very little effort you can implement a simple property by using automatically generated code, and if you need to include additional logic later, you can do so without breaking any existing applications.
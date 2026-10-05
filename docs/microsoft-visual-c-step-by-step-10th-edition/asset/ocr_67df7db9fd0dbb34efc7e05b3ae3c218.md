So, with very little effort, you can implement a simple property by using automatically generated code. If you need to include additional logic later, you can do so without breaking any existing applications.

> > Note
nThe syntax for defining an automatic property is almost identical to the syntax for defining a property in an interface. The exception is that an automatic property can specify an access modifier such as `private, public, or `protected`.

You can create a read-only automatic property by omitting the empty `set` accessor from your property declaration, like this:

Click here to view code image

```
class Circle
{
    public DateTime CircleCreated { get; }
...
}
```

This is useful in scenarios where you want to create an immutable property—that is, a property that is set when the object is constructed and cannot subsequently changed. For example, you might want to set the date on when an object was created or the name of the user who created it, or you might want to generate a unique identifier for the object. These are values that you typically want to set once and then prevent them from being modified. With this in mind, C# allows you to initialize read-only automatic properties in one of two ways. You can initialize the property from a constructor, like this:

Click here to view code image

```
class Circle
{
    public Circle()
    {
        CircleCreatedDate = DateTime.Now;
    }
    public DateTime CircleCreated { get; }
}
```
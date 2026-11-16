
## REVIEW

Write the statement that defines each month in the year, assigning January to 1, not the default of 0:

List three benefits of using enumerations as method parameters:

## INTERFACES

There are three primary relationships that can exist between types in your application: IS-A, Has-A and CanDo. We'll be looking at these relationships in detail in Chapter 12, but let's take a quick look now so that we can put interfaces in perspective.

A class might be a specialized type of another class, like Component and StockItem are specialized versions of their base class Ingredient in the diagram below. We call this an IS-A relationship, and it's implemented using inheritance. Alternatively, a class might contain another, as the StockItem class contains a Supplier. This is a HAS-A relationship, and is implemented using fields and properties.

You've already seen and implemented IS-A and HAS-A relationships, but there's a third kind, the CanDo relationship that's implemented using the last of the .NET Framework types we'll examine in this chapter, the INTERFACE. In the example below, the Ingredient and Supplier classes have no obvious relationship other than one of the children of Ingredient Has-A Supplier. But it's reasonable that both of them might be able to print themselves, and so they both implement the IPrintable interface, which is shown on the diagram using what's affectionately referred to as "lollipop notation".

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_298_0.png)

### INTERFACES & CLASSES

The syntax for defining an interface is almost identical to that for defining classes, but with two differences

- An interface can contain only member definitions, not implementation. Essentially, an interface defines something a class (or other interface) can do, but leaves the doing of it up to the class itself.
- Interfaces cannot define fields, constructors, destructors or other types.

```
interface <Name> <: base, interface, ...>
```

By convention, interface names begin with I and are usually adjectives that describe behavior (IPrintable).

```
interface IMyDoable
{
    Int32 MyProperty { get; set; }

    public void ShowHello();
}
```

This statement specifies that the property must have both get and set accessors. Don't confuse it with an auto-implemented property, even though the syntax is the same.

```
public class MyClass : IMyDoable
{
    Int32 m_myProperty;

    Int32 MyProperty
    {
        get {return m_myProperty;}
        set {m_myProperty = value;}
    }

    public void ShowHello ()
    {
        MessageBox.Show("Hello!");
    }
}
```

**ON YOUR OWN**

You may not realize it, but you already know how to create an interface in the Class Designer. Give it a try: Create the IPrintable interface and define its two methods.

### IMPLEMENTING INTERFACES

If you look at the Properties window of a class in the Class Designer, you’ll see that the Implements property is unavailable—you specify interface implementation using the Inheritance tool on the toolbar. But let’s add the interface inheritance in the editor, because once you do so, the editor has a neat trick for providing the implementation.

- 1. On the diagram where you created the IPrintable interface, add a class called Ingredient, and then double-click the new class to open it in the Code Editor. Add the IPrintable interface implementation to the class statement:

```
public class Ingredient : IPrintable
```

If you check the diagram at this point, you’ll see that Visual Studio has added the lollipop indicating that the class implements the interface.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_300_0.png)

- 2. Back in the editor, place the cursor anywhere in the word IPrintable, and the cursor will display a white rectangle under the “I”. If you move the mouse pointer over the rectangle, the “Smart Tag” will be displayed. Click on the Smart Tag and Visual Studio will give you two options.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_300_1.png)

You know that a class can implement more than one interface, and that different types can have members with the same name. (Both Supplier and Ingredient could have Name properties, for example.) Inevitably, your interfaces are going to overlap from time to time. When that happens, you need to use EXPLICIT IMPLEMENTATION so the compiler knows which member belongs to which interface. Explicit implementation simply uses the dot operator to identify the interface: IPrintable.PrintItem.

We're only implementing a single interface, so choose Implement Interface from the Smart Tag menu (it's never wrong to choose explicit implementation, but it's not often necessary), and Visual Studio will stub out all of the interface members for you.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_301_0.png)

## TAKE A BREAK

That's it for interfaces—there wasn't much you didn't already know how to do. You might be scratching your head a little about how and when to use them, and we'll talk about that in Chapter 12, but there really isn't anything tricky about implementing them.

Now why don't you take a break before we move on to working with the .NET types?

### WORKING WITH TYPES

Most of the time your code will instantiate types and manipulate their values and behavior.
But sometimes you'll need to step back and manipulate the types as types. We've already
seen one example of this, when we needed to use the GetType() operator to pass our enumeration to the
methods of the System.Enum class. Another time it can happen is when you need to pass an object of one
type to a method that declares a different type as a parameter. That's called CASTING, and you'll do a lot
of it. In this section we'll look at casting, and also how you can use REFLECTION to determine information
about your types at runtime.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_302_0.png)

### IMPLICIT CASTING

Implicit casting takes place when the compiler silently converts from one type to another without your doing anything in your code. There are two situations in which C# will help you out like this: Any type can be implicitly cast to its base class or one of the interfaces it implements, and numeric values will be implicitly cast if the destination type is larger (e.g., can contain more values) than the source type.

### SAFE CASTS

We'll look at the numeric data types that the .NET Framework exposes in the next chapter, but you've already seen the Int32 and Int16, both of which hold whole numbers. Since there's no possibility of losing data if you put the value of an Int16 into an Int32, the cast is considered “safe” and the compiler will implicitly cast it for you.

The reverse isn't true, however. Int32 can hold values that can't be contained in an Int16, so the compiler will complain if you try to treat an Int32 as an Int16 without stating your intentions. (We'll see how to do that in a minute.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_303_0.png)

### INHERITANCE CASTS

Remember that inheritance is usually an instance of an IsA relationship, while interface implementation is usually an instance of a CanDo relationship. In our sample class hierarchy, for example, both StockItem and Component inherit from Ingredient. That means that they expose all of the members that are defined for their parent. Similarly, both Ingredient and Supplier implement the IPrintable interface, so they expose all its members. In both cases, it's safe to treat the derived type as the base type or interface, but the reverse isn't true.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_303_1.png)

## EXPLICIT CASTS

Like implicit casts, explicit casts are also performed between numeric types and between base and derived classes, but an explicit cast is used when going the opposite direction; from a larger value to a smaller value (Int32 to Int16, for example), or from a base class or interface to a derived class.

You specify an explicit cast by putting the name of the desired type or interface in parentheses in front of the source type. Be aware, even with explicit casting, these remain unsafe conversions, and can result in data loss (in the case of numeric casts) or exceptions (in either case).

```
myInt16 = (Int16)myInt32;
```

You can use an explicit cast to perform casts that .NET considers unsafe, but you could potentially lose data.

| Type | Range |
| --- | --- |
| Int32 | -2,147,483,648 to 2,147,483,647 |
| Int16 | -32,768 to 32,767 |

```
myComponent = (MyComponent)myIngredient;
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_304_0.png)


classes (reference types) rather than structures.

| Keyword | Type equivalent | Class or structure |
|---|---|--|
| bool | System.Boolean | Structure |
| byte | System.Byte | Structure |
| decimal | System.Decimal | Structure |
| double | System.Double | Structure |
| float | System.Single | Structure |
| int | System.Int32 | Structure |
| long | System.Int64 | Structure |
| object | System.Object | Class |
| sbyte | System.SByte | Structure |
| short | System.Int16 | Structure |
| string | System.String | Class |
| uint | System.UInt32 | Structure |
| ulong | System.UInt64 | Structure |
| ushort | System.UInt16 | Structure |

# Declaring a structure

To declare your own structure type, you use the struct keyword followed by the name of the type and then enclose the body of the structure between opening and closing braces. Syntactically, the process is similar to declaring a class. For example, here is a structure named Time that contains three public int fields named hours, minutes, and seconds:

Click here to view code image

```
struct Time
{
    public int hours, minutes, seconds;
}
```

As with classes, making the fields of a structure public is not advisable in most cases; there's no way to control the values held in public fields. For example, anyone could set the value of minutes or seconds to a value greater than 60. A better idea is to make the fields private and provide your structure with constructors and methods to initialize and manipulate these fields, as shown in this example:

Click here to view code image

```
struct Time
{
    private int hours, minutes, seconds;
    ...
    public Time(int hh, int mm, int ss)
    {
        this.hours = hh % 24;
        this.minutes = mm % 60;
        this.seconds = ss % 60;
    }

    public int Hours()
    {
        return this.hours;
    }
}
```

> Note
> By default, you cannot use many of the common operators on your own structure types. For example, you cannot use the equality operator (==) or the inequality operator (!= to compare structure type variables. However, you can use the built-in Equals() method exposed by all structures to compare structure type variables. You can also explicitly declare and implement operators for your own structure types. The syntax for doing this is covered in Chapter 21, "Querying in-memory data by using query expressions."

When you copy a value type variable, you get two copies of the value. In contrast, when you copy a reference type variable, you get two references to the same object. In summary, use structures for small data values for which it is just as near or easily to copy the value as it would be to copy an address. Use classes for more complex data that is too big to copy efficiently.

> Tip
> Use structures to implement simple concepts whose main feature is their value rather than the functionality they provide.

# Understanding differences between structures and classes

A structure and a class are syntactically similar, but they have a few important differences. Let's look at some of these variations:

- You can't declare a default constructor (a constructor with no parameters) for a structure. The following example would compile if Time were a class, but because Time is a structure, it does not:

Click here to view code image

```
struct Time
{
    public Time() { ... } // compile-time error
    ...
}
```

You can't declare your own default constructor for a structure because the compiler always generates one. In a class, the compiler synthesizes the default constructor only if you don't write a constructor yourself. The compiler-generated default constructor for a structure always sets the fields to 0, false, or null—just as a class. Therefore, you should ensure that a structure value created by the default constructor behaves logically and makes sense with these default values. This has some ramifications that you'll explore in the next exercise.

You can initialize fields to different values by providing a nondefault constructor. However, when you do this, your nondefault constructor must explicitly initialize all fields in your structure; the default initialization no longer occurs. If you fail to do this, you'll get a compile-time error. For example, the following example would compile and silently initialize seconds to 0 if Time was a class, it fails to compile because Time is a structure:

Click here to view code image

```
struct Time
{
    private int hours, minutes, seconds;
    ...
    public Time(int hh, int mm)
    {
        this.hours = hh;
        this.minutes = mm;
    } // compile-time error: seconds not initialized
```

- In a class, you can initialize instance fields at their point of declaration; in a structure, you cannot. The following example would compile if Time was a class, but it causes a compile-time error because Time is a structure:

Click here to view code image

```
struct Time
{
    private int hours = 0; // compile-time error
    private int minutes; private int seconds;
    ...
}
```

The following table summarizes the main differences between a structure and a class:

| Question | Structure | Class |
| --- | --- | --- |
| Is this value type or a reference type? | A structure is a value type. | A class is a reference type. |
| Do instances live on the stack or heap? | Structure instances are called values and usually live on the stack (see following note). | Class instances are called objects and usually live on the heap. |
| Can you declare a default constructor? | No | Yes |
| If you declare your own constructor, will the compiler still generate the default constructor? | Yes | No |
| If you don't initialize a field in your constructor, will the compiler automatically initialize it for you? | No | Yes |
| Are you allowed to initialize instance fields at their point of declaration? | No | Yes |

> Note
> There are some occasions when struct will be created on the heap rather than the stack. This most commonly happens when a class declares a field that is struct type. When object of such a class is created, the memory for the struct is allocated as part of the object on the heap rather than separately on the stack.

There are other differences between classes and structures concerning inheritance. These differences are covered in Chapter 12, “Working with inheritance.”

# Declaring variables

After you’ve defined a structure type, you can use it the same way you do any other type. For example, if you have defined the Time structure, you can create variables, fields, and parameters of type Time, as shown in this example:

Click here to view code image

```
struct Time
{
    private int hours, minutes, seconds;
    ...
}
class Example
{
    private Time currentTime;
    public void Method(Time parameter)
    {
        Time localVariable;
        ...
    }
}
```

> Note
> As with enumerations, you can create a nullable version of a structure variable by using the ? modifier. You can then assign the null value to the variable, like so:

```
Time? currentTime = null;
```

# Understanding structure initialization

Earlier in this chapter, you saw how you could initialize the fields in a structure by using a constructor. If you call a constructor, the various rules described earlier guarantee that all the fields in the structure will be initialized:

```
var now = new Time();
```

The following illustration depicts the state of the fields in this structure:

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_377_0.png)

However, because structures are value types, you can also create structure variables without calling a constructor, as shown in the following example:

```
Time now;
```

This time, the variable is created, but its fields are left in their uninitialized state. The following illustration depicts the state of the fields in the now variable. Any attempt to read the structure or access the values in these fields will result in the compiler error “Use of unassigned local variable."

This property increments the static account number member before returning the result. This action probably isn’t a good idea, however, because the user of the property receives no clue that anything is happening other than the actual reading of the property. The incrementation is a side effect.

Like the accessor methods that they mimic, properties shouldn’t change the state of the class other than, say, setting a data member’s value. Both properties and methods generally should avoid side effects because they can lead to subtle bugs. Change a class as directly and explicitly as possible.

![](bbox=[0.13, 0.23, 0.22, 0.3])

# Letting the compiler write properties for you

Most properties described in the previous section are utterly routine, and writing them is tedious (though simple):

```
private string _name; // An underlying data member for the property
public string Name { get { return _name; } set { _name = value; } }
```

Because you write this same boilerplate code repeatedly, since C# 3.0, the compiler now does it for you. All you have to write for the previous property (including the private data member) is this line:

```
public string Name { get; set; }
```

This line is sort of equivalent to

```
private string <somename>; // What’s <somename>? Don’t know or care.
public string Name { get { return <somename>; } set { <somename> = value; } }
```

![](bbox=[0.13, 0.65, 0.22, 0.72])

The compiler creates a mysterious data member that shall be nameless along with the accessor boilerplate code. The AccessorPropertyShortcuts example on csharp102.info illustrates this usage. This style encourages using the property even inside other members of its containing class because the property name is all you know. For that reason, you must have both get and set when you write the shortcut property. You can initialize such properties using the property syntax:

```
public int AnInt { get; set; } // Compiler provides a private variable.
...
AnInt = 2; // Initialize compiler-written instance variable via property.
```

# Accessors with access levels

Accessor properties don’t necessarily have to be declared public. You can declare them at any appropriate level, even private, if the accessor is used only inside its class. (The upcoming example marks the Name property internal.)
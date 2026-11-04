
## Part I: C# Fundamentals

This is because the ToString() method from the Contact class inherits from the System.Object class, which simply returns the name of the class.

To ensure that the ToString() method returns something appropriate, you need to override it:

```
class Contact
{
    public int ID;
    public string FirstName;
    public string LastName;
    public string Email;

    public override string ToString()
    {
        return ID + "," + FirstName + "," +
            LastName + "," + Email;
    }
    //...
}
```

In this implementation of the ToString() method, you return the concatenation of the various data members, as evident in the output of the following code:

```
Contact c1 = new Contact()
{
    ID = 1234,
    FirstName = "Wei-Meng",
    LastName = "Lee",
    Email = "weimenglee@learn2develop.net"
};

//---returns "1234,Wei-Meng,Lee,weimenglee@learn2develop.net"---
Console.WriteLine(c1.ToString());
```

## Attributes

Attributes are descriptive tags that can be used to provide additional information about types (classes), members, and properties. Attributes can be used by .NET to decide how to handle objects while an application is running.

There are two types of attributes:

- Attributes that are defined in the CLR.
- Custom attributes that you can define in your code.

## CLR Attributes

Consider the following Contact class definition:

```
class Contact
{
    public string FirstName;
    public string LastName;

    public void PrintName()
    {
        Console.WriteLine("{0} {1}", this.FirstName, this.LastName);
    }

    [Obsolete("This method is obsolete. Please use PrintName()")]
    public void PrintName(string FirstName, string LastName)
    {
        Console.WriteLine("{0} {1}", FirstName, LastName);
    }
}
```

Here, the PrintName() method is overloaded — once with no parameter and again with two input parameters. Notice that the second PrintName() method is prefixed with the Obsolete attribute:

```
[Obsolete("This method is obsolete. Please use PrintName()")]
```

That basically marks the method as one that is not recommended for use. The class will still compile, but when you try to use this method, a warning will appear (see Figure 4-7).

![](img/a977a875c7c627b45d939729705a252e_186_0.png)

Figure 4-7

The Obsolete attribute is overloaded — if you pass in true for the second parameter, the message set in the first parameter will be displayed as an error (by default the message is displayed as a warning):

```
[Obsolete("This method is obsolete. Please use PrintName()", true)]
```

Figure 4-8 shows the error message displayed when you use the PrintName() method marked with the Obsolete attribute with the second parameter set to true.

![](img/a977a875c7c627b45d939729705a252e_187_0.png)

Figure 4-8

Attributes can also be applied to a class. In the following example, the obsolete attribute is applied to the Contact class:

```
[Obsolete("This class is obsolete. Please use NewContact")]
class Contact
{
    //...
}
```

## Custom Attributes

You can also define your own custom attributes. To do so, you just need to define a class that inherits directly from System.Attribute. The following Programmer class is one example of a custom attribute:

```
public class Programmer : System.Attribute
{
    private string _Name;
    public double Version;
    public string Dept { get; set; }
    public Programmer (string Name)
    {
        this._Name = Name;
    }
}
```

In this attribute, there are:

- [ ] One private member (_Name)
- [ ] One public member (Version)
- [ ] One constructor, which takes in one string argument

Here's how to apply the Programmer attribute to a class:

```
[Programmer("Wei-Meng Lee", Dept="IT", Version=1.5)]
class Contact
{
    //...
}
```

You can also apply the Programmer attribute to methods (as the following code shows), properties, structure, and so on:

```
[Programmer("Wei-Meng Lee", Dept="IT", Version=1.5)]
class Contact
{
    [Programmer("Jason", Dept = "CS", Version = 1.6)]
    public void PrintName()
    {
        Console.WriteLine("{0} {1}", this.FirstName, this.LastName);
    }
    //...
}
```

Use the AttributeUsage attribute to restrict the use of any attribute to certain types:

```
[System.AttributeUsage(System.AttributeTargets.Class |
                      System.AttributeTargets.Method |
                      System.AttributeTargets.Property)]
public class Programmer : System.Attribute
{
    private string _Name;
    public double Version;
    public string Dept { get; set; }
    public Programmer(string Name)
    {
        this._Name = Name;
    }
}
```

In this example, the Programmer attribute can only be used on class definitions, methods, and properties.

## Structures

An alternative to using classes is to use a struct (for structure). A struct is a lightweight user-defined type that is very similar to a class, but with some exceptions:

- Structs do not support inheritance or destructors.
- A struct is a value type (class is a reference type).
- A struct cannot declare a default constructor.

## Part I: C# Fundamentals

Structs implicitly derive from *object* and unlike classes, a struct is a value type. This means that when an object is created from a struct and assigned to another variable, the variable will contain a copy of the struct object.

Like classes, structs support constructor, properties, and methods. The following code shows the definition for the *Coordinate* struct:

```
```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    }
}
```
```

```
```csharp
public struct Coordinate
{
    public double latitude { get; set; }
    public double longitude { get; set; }
}
```
```

The *Coordinate* struct contains two properties (defined using the automatic properties feature). You can add a constructor to the struct if you want:

```
```csharp
public struct Coordinate
{
    public double latitude { get; set; }
    public double longitude { get; set; }
}

public Coordinate(double lat, double lng)
{
    latitude = lat;
    longitude = lng;
}
```
```

> **Remember, a struct cannot have a default constructor.**

Note that the compiler will complain with the message “Backing field for automatically implemented property ‘Coordinate.latitude’ must be fully assigned before control is returned to the caller” when you try to compile this application. This restriction applies only to structs (classes won’t have this problem). To resolve this, you need to call the default constructor of the struct, like this:

```
public struct Coordinate
{
    public double latitude { get; set; }
    public double longitude { get; set; }

    public Coordinate(double lat, double lng)
        : this()
    {
        latitude = lat;
        longitude = lng;
    }
}
```

You can also add methods to a struct. The following shows the ToString() method defined in the Coordinate struct:

```
public struct Coordinate
{
    public double latitude { get; set; }
    public double longitude { get; set; }

    public Coordinate(double lat, double lng)
        : this()
    {
        latitude = lat;
        longitude = lng;
    }

    public override string ToString()
    {
        return latitude + "," + longitude;
    }
}
```

To use the Coordinate struct, create a new instance using the new keyword and then initialize its individual properties:

```
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }

    private void Form1_Load(object sender, EventArgs e)
    {
        Coordinate pt1 = new Coordinate();
        pt1.latitude = 1.33463167;
        pt1.longitude = 103.74697;
    }
}
```

Or you can use the object initializer feature:

```
private void Form1_Load(object sender, EventArgs e)
{
    //...
    Coordinate pt2 = new Coordinate()
    {
        latitude = 1.33463167,
        longitude = 101.74697
    };
}
```

Because structs are value types, assigning one struct to another makes a copy of its value, as the following code sample shows:

```
private void Form1_Load(object sender, EventArgs e)
{
    //...
    Coordinate pt2 = new Coordinate()
    {
        latitude = 1.33463167,
        longitude = 101.74697
    };

    Coordinate pt3;
    pt3 = pt2;
    Console.WriteLine("After assigning pt2 to pt3");
    Console.WriteLine("pt2: {0}", pt2.ToString());
    Console.WriteLine("pt3: {0}", pt3.ToString());

    pt3.latitude = 1.45631234;
    pt3.longitude = 101.32355;

    Console.WriteLine("After changing pt3");
    Console.WriteLine("pt2: {0}", pt2.ToString());
    Console.WriteLine("pt3: {0}", pt3.ToString());
}
```

Here's the program's output:

```
After assigning pt2 to pt3
pt2: 1.33463167,103.74697
pt3: 1.33463167,103.74697
After changing pt3
pt2: 1.33463167,103.74697
pt3: 1.45631234,101.32355
```

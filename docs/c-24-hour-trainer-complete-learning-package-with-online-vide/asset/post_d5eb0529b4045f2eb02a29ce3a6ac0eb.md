
```csharp
// If our last name comes first, we come first.
if (LastName.CompareTo(other.LastName) < 0) return -1;

// If our last name comes second, we come second.
if (LastName.CompareTo(other.LastName) > 0) return 1;

// If our last names are the same, compare first names.
return FirstName.CompareTo(other.FirstName);
}
} ...
```

First, if the other Person object is null, the method returns 1 to indicate that the current Person should come after it. (By convention, null values come before non-null values.)

Next, the method compares the two objects' LastName values. If the values are not the same, the code returns -1 or 1 to indicate that the current Person comes before or after the other.

Finally, if the two LastName values are the same, the code uses the CompareTo method provided by the string class to compare the two FirstName values and returns the result.

You can write the code to implement an interface yourself, but it's easier to let Visual Studio build a default implementation for you. Write the class declaration including the interface. Then hover the mouse over the interface name in the class declaration and look for the change suggestion lightbulb to appear. You can see it under the word “class” in Figure 27-1.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_425_0.png)

**FIGURE 27-1**

Click the lightbulb and select the Implement Interface command from the dropdown list, as shown in Figure 27-2.

When you select that command, Visual Studio adds placeholder code to satisfy the interface. The following code shows the placeholder method for the IComparable<Person> interface:

```csharp
public int CompareTo(Person other)
{
    throw new NotImplementedException();
}
```

![](img/d5be6ade75773ca6cec5c78f96a98bb1_426_0.png)

**FIGURE 27-2**

Now you can fill in the code you want to use.

You can learn more about what an interface is for and what it does in several ways. You can always search the online help. You can also right-click the interface's name and select Go To Definition to see information, as shown in Figure 27-3. Click the plus signs on the left to view detailed comments describing the purposes of the pieces of code.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_426_1.png)

**FIGURE 27-3**

Finally, you can open the Object Browser (use the View menu's Object Browser command) and search for the interface's name (without the generic parameters). Select the interface in the browser's left panel. Click an item in the upper-right panel for more details, as shown in Figure 27-4.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_427_0.png)

**FIGURE 27-4**

## DEFINING INTERFACES

The preceding sections give examples that implement predefined interfaces. This section explains how you can define your own.

Defining an interface is a lot like defining a class, with two main differences:

- First, you use the keyword `interface` instead of `class` in the declaration. (You can use the Project menu's Add Class command and then change the keyword `class` to `interface`.)
- Second, you don't provide any code for the properties, methods, and events that you declare in the interface.

The following code shows a simple IDrawable interface. The code includes a `using System.Drawing;` directive at the top of the file to make working with Brush, Pen, and Graphics objects easier.

```csharp
interface IDrawable
{
    int X { get; set; }
    int Y { get; set; }
    Brush Background { get; set; }
    Pen Foreground { get; set; }
    void Draw(Graphics gr);
}
```

A class that implements IDrawable must provide X, Y, Background, and Foreground properties and a Draw method.

You cannot provide an accessibility modifier such as private to the items defined by an interface because they are always assumed to be public. That means a class that implements the interface must declare these items as public.

The declarations for the properties look like they are providing a default implementation, but they actually only indicate which accessors are required. For example, you could omit the set accessor to require a read-only property.

A class that implements IDrawable must still provide its own implementations, although you can use auto-implemented properties if you like. For example, the following code shows how the DrawableCircle class might implement its X property:

```csharp
public int X { get; set; }
```

> **NOTE** This example might work better with true inheritance instead of an interface. If you make a Drawable class that implements the X, Y, Background, and Foreground properties, other classes such as DrawableCircle could inherit them. In this example an interface makes sense only if the classes already inherit from some other class so they cannot also inherit from Drawable.

## TRY IT

In this Try It, you build the Vehicle class and the IDomicile interface described earlier in this lesson. You then make a MotorHome class that inherits from the first and implements the second. Finally, you create an instance of the derived class.

### Lesson Requirements

In this lesson, you:

- Start a new project. Create a Vehicle class with the properties NumberOfPassengers, MilesPerGallon, and NumberOfCupHolders. Give it an initializing constructor and override its ToString method so it returns the object's property values separated by the escape sequence `\r\n`.
- Make an IDomicile interface that defines the properties SquareFeet, NumberOfBedrooms, and NumberOfBathrooms. Also make it define a ToString method that returns a string as usual.
- Derive the MotorHome class from Vehicle, making it implement IDomicile. Give it an initializing constructor and override its ToString method so it returns all of the object's property values separated by the escape sequence `\r\n`.
- Create an instance of the MotorHome class. Then use its ToString method to display its properties in a textbox.

**NOTE** You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

### Hints

- Don't forget to make the MotorHome class's constructor invoke the base class's constructor. If you don't remember how, see the section "Invoking Other Constructors" in Lesson 24.
- You can save a little work by making the MotorHome class's ToString method call the Vehicle class's version.

### Step-by-Step

1. Start a new project. Create a Vehicle class with the properties NumberOfPassengers, MilesPerGallon, and NumberOfCupHolders. Give it a constructor to make it easy to initialize a new object's properties. Override its ToString method so it returns the object's property values separated by the escape sequence `\r\n`.

   Use code similar to the following:

```csharp
class Vehicle
{
    // Properties.
    public int NumberOfPassengers { get; set; }
    public double MilesPerGallon { get; set; }
    public int NumberOfCupHolders { get; set; }

    // Initializing constructor.
    public Vehicle(int numberOfPassengers, double milesPerGallon,
        int numberOfCupHolders)
    {
        NumberOfPassengers = numberOfPassengers;
        MilesPerGallon = milesPerGallon;
        NumberOfCupHolders = numberOfCupHolders;
    }

    // Return the object's properties.
    public override string ToString()
    {
        return
            "NumberOfPassengers: " + NumberOfPassengers +
            "\r\nMilesPerGallon: " + MilesPerGallon +
            "\r\nNumberOfCupHolders: " + NumberOfCupHolders;
    }
}
```

2. Make an IDomicile interface that defines the properties SquareFeet, NumberOfBedrooms, and NumberOfBathrooms. Also make it define a ToString method that returns a string as usual.

   Use code similar to the following:

```csharp
interface IDomicile
{
    int SquareFeet { get; set; }
    int NumberOfBedrooms { get; set; }
    double NumberOfBathrooms { get; set; }
    string ToString();
}
```

3. Derive the MotorHome class from Vehicle, making it implement IDomicile. Give it a constructor to make it easy to initialize a new object's properties. Override its ToString method so it returns the object's property values separated by the escape sequence `\r\n`.

   Use code similar to the following:

```csharp
class MotorHome : Vehicle, IDomicile
{
    // IDomicile methods.
    public int SquareFeet { get; set; }
    public int NumberOfBedrooms { get; set; }
    public double NumberOfBathrooms { get; set; }

    // Initializing constructor.
    public MotorHome(int numberOfPassengers, double milesPerGallon,
        int numberOfCupHolders, int squareFeet,
        int numberOfBedrooms, double numberOfBathrooms)
        : base(numberOfPassengers, milesPerGallon,
        numberOfCupHolders)
    {
        SquareFeet = squareFeet;
        NumberOfBedrooms = numberOfBedrooms;
        NumberOfBathrooms = numberOfBathrooms;
    }

    // Return the object's properties.
    public override string ToString()
    {
        return base.ToString() +
            "\r\nSquareFeet: " + SquareFeet +
            "\r\nNumberOfBedrooms: " + NumberOfBedrooms +
            "\r\nNumberOfBathrooms: " + NumberOfBathrooms;
    }
}
```

4. Create an instance of the MotorHome class. Then use its ToString method to display its properties in a textbox.

   The following code creates an instance of the MotorHome class and displays its properties in resultTextBox:

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    // Make a MotorHome.
    MotorHome motorHome = new MotorHome(6, 0.25, 32, 150, 3, 0.5);
}
```

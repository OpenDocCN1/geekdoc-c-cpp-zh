The following C# code shows a version of the Direction property stored in the backing field named direction:

```
```csharp
// The Turtle's direction in degrees.
private int direction = 0;      // Backing field.
public int Direction
{
    get { return direction; }
    set { direction = value; }
}
```
```

The code starts by defining the field direction to hold the property's value. The field is private so only the code inside the class can see it.

The property's get accessor simply returns the value of direction.

The property's set accessor saves a new value in the backing field direction. The new value that the calling code is trying to assign to the property is stored in a parameter named value. This parameter is a bit odd because it isn't declared anywhere. The set accessor implicitly defines value and can use it.

The preceding code simply copies values in and out of the backing field, so why didn't you just make the backing field public and not bother with a property? There are several reasons.

First, a property hides its details from the outside world, increasing the class's encapsulation. As far as the outside world is concerned, a description of the Direction property tells you what is stored (the direction in degrees) but not how it is stored (as an integer value in degrees).

This example stores the direction in degrees, but suppose you decided that the class would work better if you stored the direction in radians. If Direction is a field, then any code that uses it would now break because it is using degrees. If you use accessors, they can translate between degrees and radians as needed so the code outside the class doesn't need to know that anything has changed.

The following code shows a new version of the Direction property that stores the value in radians. As far as the code outside the class is concerned, nothing has changed and that code can still work in degrees.

```
```csharp
// The Turtle's direction in radians.
private double direction = 0;      // Backing field.
public int Direction
{
    get { return (int)(direction * 180 / Math.PI); }
    set { direction = value * Math.PI / 180; }
}
```
```

You can also add validation code to property accessors. For example, suppose the Direction property represents an angle in degrees and you only want to allow values between 0 and 359. The following code asserts that the new value is between 0 and 359 degrees. The program can continue correctly if the value is outside of this range so the code uses Debug.Assert instead of throwing an exception:

```
```csharp
// The Turtle's direction in degrees.
private int direction = 0;      // Backing field.
public int Direction
```
```
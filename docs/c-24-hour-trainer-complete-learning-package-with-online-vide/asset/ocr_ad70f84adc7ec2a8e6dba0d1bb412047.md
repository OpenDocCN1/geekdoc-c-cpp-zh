By convention, event handlers usually take two parameters named sender and e. The sender parameter is an object that contains a reference to whatever object is raising the event. The e parameter contains data specific to the event. Often you will define a class to provide that information and the parameter e will be of that class.

For example, suppose you want the Turtle class to raise an OutOfBounds event to tell the program that it is trying to move the Turtle off the drawing area. You want the parameter e to tell the program the X and Y coordinates where the Turtle is trying to move.

In that case, you could use the following TurtleOutOfBoundsEventArgs class to store the X and Y coordinates:

```
```csharp
// The TurtleOutOfBoundsEventArgs data type.
public class TurtleOutOfBoundsEventArgs
{
    // Where the Turtle would stop if
    // this were not out of bounds.
    public int X { get; set; }
    public int Y { get; set; }
}
```
```

The following code shows how the Turtle class could declare its OutOfBoundsEventHandler delegate:

```
```csharp
// Declare the OutOfBounds event's delegate.
public delegate void OutOfBoundsEventHandler(
    object sender, TurtleOutOfBoundsEventArgs e);
```
```

Next the class must declare the actual event to tell C# that the class will provide this event. The declaration should begin with an accessibility keyword (public, private, and so on) followed by the keyword event. Next it should give the event handler's delegate type. It finishes with the event's name.

The following code declares the OutOfBounds event, which is handled by event handlers of type OutOfBoundsEventHandler:

```
```csharp
// Declare the OutOfBounds event.
public event OutOfBoundsEventHandler OutOfBounds;
```
```

The final piece of code that you need to add to the class is the code that raises the event. This code simply invokes the event handler, passing it any parameters that it should receive.

Before it raises the event, however, the code should verify that some other piece of code has registered to receive the event. The code does that by checking whether the event is null. (This syntax seems a bit strange to me. The code looks like it is checking that an event is null when really it's asking whether another piece of code has asked to receive the event. This is just the syntax used by C#.)

The following code raises the Turtle class's OutOfBounds event:

```
```csharp
if (OutOfBounds != null)
{
    TurtleOutOfBoundsEventArgs args = new TurtleOutOfBoundsEventArgs();
    args.X = newX;
    args.Y = newY;
    OutOfBounds(this, args);
}
```
```
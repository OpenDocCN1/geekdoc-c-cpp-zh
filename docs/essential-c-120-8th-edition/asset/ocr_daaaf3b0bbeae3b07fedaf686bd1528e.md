# Chapter 9: Introducing Structs and Records

even toString() diagnostic capabilities. Listing 9.3 demonstrates working with the Angle type.

LISTING 9.3: Working with the Record Struct

```
using System.Diagnostics;

public class Program
{
    public static void Main(
    {
        (int degrees, int minutes, int seconds) = (90, 0, 0);

        // The constructor is generated using positional parameters
        Angle angle = new(degrees, minutes, seconds);

        // Records include a ToString() implementation
        // that returns:
        "Angle = 90, Minutes = 0, Seconds = 0, Name = ""
        Console.WriteLine(angle.ToString());

        // Records has a deconstructor using the
        // positional parameters.
        if (angle is (int, int, int, string) angleData)
        {
            Trace.Assert(angle.Degrees == angleData.Degrees);
            Trace.Assert(angle.Minutes == angleData.Minutes);
            Trace.Assert(angle.Seconds == angleData.Seconds);
        }

        Angle copy = new(degrees, minutes, seconds);
        // Records provides a custom equality operator.
        Trace.Assert(angle == copy);

        // The with operator is the equivalent of
        // Angle copy = new(degrees, minutes, seconds);
        copy = angle with { };
        Trace.Assert(angle == copy);

        // The with operator has object initializer type
        // syntax for instantiating a modified copy.
        Angle modifiedCopy = angle with { Degrees = 180 };
        Trace.Assert(angle != modifiedCopy);
    }
}
```
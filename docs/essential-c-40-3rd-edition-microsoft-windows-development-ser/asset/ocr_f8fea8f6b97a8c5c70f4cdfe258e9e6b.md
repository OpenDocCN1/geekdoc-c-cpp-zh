```
{
  // ...
  Angle angle = new Angle(25, 58, 23);
  object objectAngle = angle; // Box
  Console.WriteLine(((Angle)objectAngle).Hours);

  // Unbox and discard
  ((Angle)objectAngle).MoveTo(26, 58, 23);
  Console.WriteLine(((Angle)objectAngle).Hours);

  // Box, modify, and discard
  ((IAngle)angle).MoveTo(26, 58, 23);
  Console.WriteLine("" + ((Angle)angle).Hours);

  // Modify heap directly
  ((IAngle)objectAngle).MoveTo(26, 58, 23);
  Console.WriteLine("" + ((Angle)objectAngle).Hours);

  // ...
}
```

# Output 8.2:

25、25、25、26

Listing 8.7 uses the Angle struct and IAngle interface from Listing 8.1. Note also that the IAngle.MoveTo() interface changes Angle to be mutable. This brings out some of the idiosyncrasies and, in so doing, demonstrates the importance of the guideline to make structs immutable.

In the first two lines, you initialize angle and then box it into a variable called objectAngle. Next, you call move in order to change Hours to 26. However, as the output demonstrates, no change actually occurs the first time. The problem is that in order to call MoveTo(), the compiler unboxes objectAngle and (by definition) makes a copy of the value. Although the stack value is successfully modified at execution time, this value is discarded and no change occurs on the heap location referenced by objectAngle.

In the next example, a similar problem occurs in reverse. Instead of calling MoveTo() directly, the value is cast to IAngle. The cast invokes a box instruction and the runtime copies the angle data to the heap. Next, the data on the heap is modified directly on the heap before the call returns.
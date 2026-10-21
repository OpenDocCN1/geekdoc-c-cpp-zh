```
EventTest et = new EventTest();
ec.Status += new EDelegate(et.EventCatch);
ec.TriggerEvent();
}
public void EventCatch(string str)
{
Console.WriteLine(str);
}
}
```

Program 16.3 would produce the following output:
Event Triggered

Program 16.3 declares first a delegate which is used to declare the event Status in the class EventClass. This class has a method to trigger the event when it occurs. Note that we have to check the event Status against null because no event might have occurred earlier.

The class EventTest defines, in addition to the Main, a method EventCatch whose signature matches that of the event. The EventClass is instantiated, and the method is subscribed to the Status event: ec.Status += new EDelegate(et.EventCatch); From now on, this method is called when the event is triggered.

Program 16.4 shows another application of delegates which store values in an array, sorts and then, reverses the array.

# Program 16.4
AN APPLICATION OF DELEGATES

```
using System;
using System.Collections.Generic;
using System.Text;

namespace Delegates
{
public enum Comparison
{
    Student1 = 1,
    Student2 = 2
}
// a simple array to hold 2 items
public class Pair<array1>
{
    // private array to hold the two objects
    private array1[] pairObj = new array1[2];
    // the delegate declaration
    public delegate Comparison
        WhichIsFirst(array1 obj1, array1 obj2);
    // passed in constructor take two objects, added in the order as received in the array
    public Pair(
        array1 arr1,
        array1 arr2)
{
```
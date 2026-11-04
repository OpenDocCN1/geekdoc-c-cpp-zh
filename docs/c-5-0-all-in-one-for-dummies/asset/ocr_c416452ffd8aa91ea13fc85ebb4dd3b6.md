# Mixing inheritance and interface implementation

Unlike some languages, such as C++, C# doesn’t allow multiple inheritance — a class inheriting from two or more base classes. Think of class `HouseBoat` inheriting from `House` and `Boat`. Just don’t think of it in C#.

But although a class can inherit from only one base class, it can *in addition* implement as many interfaces as needed. After I treated `recordability` as an interface, a couple of the recording devices looked like this:

```
```csharp
public class Pen : IRecordable          // Base class is Object.
{
    public void TakeANote(string note)
    {
        // Record the note with a pen.
    }
}
public class PDA : ElectronicDevice, IRecordable
{
    public void TakeANote(string note)
    {
        // Record the note with your thumbs or a stylus.
    }
}
```
```

Class PDA inherits from a base class *and* implements an interface.

# And he-e-e-re’s the payoff

To begin to see the usefulness of an interface such as `IRecordable`, consider this example:

```
```csharp
public class Program
{
    static public void RecordShoppingList(IRecordable recorder)
    {
        // Jot it down, using whatever device was passed in.
        recorder.TakeANote(...);
    }
    public static void Main(string[] args)
    {
        PDA pda = new PDA();
        RecordShoppingList(pda);  // Oops, battery's low ...
        Pen pen = new Pen();
        RecordShoppingList(pen);
    }
}
```
```

The `IRecordable` parameter is an instance of any class that implements the `IRecordable` interface. `RecordShoppingList()` makes no assumptions about the exact type of recording object. Whether the device is a PDA or a type of ElectronicDevice isn’t important, as long as the device can record a note.
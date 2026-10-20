Like many things, making this easy is hard. But the hard code only gets written once, so it is worth the work. The work to be done is boilerplate:

+   1. See if the new value and the old value are different.
+   2. Raise the INotifyPropertyChanging event.
+   3. Change the value.
+   4. Raise the INotifyPropertyChanged event.

The hard part is determining what string to use for the name of the property. Remember that the point of this exercise is to make the code durable enough so that strings aren’t necessary to make the code work properly. I wanted to make an API that is as simple as possible for users but allows the code underlying that simple API to execute whatever magic was necessary to do all the work.

My original goal was to make the extension methods extend either INotifyPropertyChanged or INotifyPropertyChanging, but that made the API worse, primarily because it made raising the events harder. Instead, the method actually extends the PropertyChanged event that is a member of INotifyPropertyChanged. Here’s how you would use it in the MemoryMonitor:

```
```csharp
// MemoryMonitor, using the extension methods
private void timerCallback(object unused)
{
    long updatedValue = GC.GetTotalMemory(false);
    PropertyChanged.SetNotifyProperty(updatedValue,
        () => UsedMemory);
}

public long UsedMemory
{
    get;
    private set;
}
```
```

This serves the goal of making the implementation of the MemoryMonitor much easier. No magic strings. The UsedMemory is now an automatic property. There are no magic strings inside the code. The code to implement this is a complicated bit that uses reflection and expression trees, so let’s walk through it carefully. Here’s the full extension method:
RemoveItem are overridden to fire the CollectionChanged event. Clients of this class can register to this event by using the interface INotifyCollectionChanged.

The next example demonstrates using an ObservableCollection<string> where the method Data_CollectionChanged is registered to the CollectionChanged event. Two items are added to the end—one item is inserted, and one item is removed (code file ObservableCollectionSample/Program.cs):

```
var data = new ObservableCollection<string>();
data.CollectionChanged += Data_CollectionChanged;
data.Add("One");
data.Add("Two");
data.Insert(1,"Three");
data.Remove("One");
```

The ObservableCollectionSample makes use of the following dependencies and namespaces:

# Dependencies

+   NETStandard.Library
+   System.ObjectModel

# Namespaces

+   System.Collections.ObjectModel
+   System.Collections.Specialized
+   static System.Console

The method Data_CollectionChanged receives NotifyCollectionChangedEventArgs containing information about changes to the collection. The Action property provides information if an item was added or removed. With removed items, the OldItems property is set and lists the removed items. With added items, the NewItems property is set and lists the new items:

```
public static void Data_CollectionChanged(object sender,
NotifyCollectionChangedEventArgs e)
{
    WriteLine($"action: {e.Action.ToString()}");

    if (e.OldItems != null)
    {
        WriteLine($"starting index for old item(s): {e.OldStartingIndex}");
        WriteLine("old item(s):");
        foreach (var item in e.OldItems)
        {
            WriteLine(item);
        }
    }
    if (e.NewItems != null)
    {
        WriteLine($"starting index for new item(s): {e.NewStartingIndex}");
```
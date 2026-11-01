The next sample shows using an ObservableCollection<string> where the method Data_CollectionChanged is registered to the CollectionChanged event. Two items are added to the end — one item is inserted, and one item is removed:

```
var data = new ObservableCollection<string>();
data.CollectionChanged += Data_CollectionChanged;
data.Add("One");
data.Add("Two");
data.Insert(1, "Three");
data.Remove("One");
```

code snippet ObservableCollectionSample/Program.cs

The method Data_CollectionChanged receives NotifyCollectionChangedEventArgs containing information about the changes of the collection. The Action property gives information if an item was added or removed. With removed items, the OldItems property is set and lists the removed items. With added items, the NewItems property is set and lists the new items:

```
static void Data_CollectionChanged(object sender,
    NotifyCollectionChangedEventArgs e)
{
    Console.WriteLine("action: {0}", e.Action.ToString());
    if (e.OldItems != null)
    {
        Console.WriteLine("starting index for old item(s): {0}", e.OldStartingIndex);
        Console.WriteLine("old item(s):");
        foreach (var item in e.OldItems)
        {
            Console.WriteLine(item);
        }
    }
    if (e.NewItems != null)
    {
        Console.WriteLine("starting index for new item(s): {0}", e.NewStartingIndex);
        Console.WriteLine("new item(s): ");
        foreach (var item in e.NewItems)
        {
            Console.WriteLine(item);
        }
    }
    Console.WriteLine();
}
```

Running the application, you can see the output as follows. The first items One and Two are added to the collection and thus the Add action is shown with the index 0 and 1. The third item Three is inserted on position 1 so it shows the action Add with index 1. Finally, the item One is removed as shown with action Remove and index 0:

```
action: Add
starting index for new item(s): 0
new item(s):
One

action: Add
starting index for new item(s): 1
new item(s):
Two

action: Add
```
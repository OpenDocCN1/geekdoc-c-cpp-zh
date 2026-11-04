+   7. Click the **Change Data Context Value With Code-Behind** button.

Hmmm. Nothing is happening. What is up with that? If you click on the **Show Current Data Context Value** button, you will see the properties have in fact been changed. Because you're using a TwoWay binding, your settings should automatically update your UI, right? Wrong! This is where another feature of WPF, the concept of `INotifyPropertyChanged`, comes into play.

`INotifyPropertyChanged` is a simple interface that allows your objects to raise an event that notifies its subscribers (namely your application) that a property value on the object has changed. Client applications subscribe to these events and update the user interface with the new values only when changes occur.

A similar interface exists for collections as well — the `INotifyCollectionChanged` interface. WPF also provides a generic class called `ObservableCollection<T>` that already implements `INotifyCollectionChanged` for you. When creating an `ObservableCollection` or your own collection that implements `INotifyCollectionChanged`, you need to ensure that the objects that will be contained within the collection also implement `INotifyPropertyChanged` interface.

The `INotifyPropertyChanged` interface contains a single event that must be implemented. This event is called `PropertyChanged`, and its parameters are the object that owns the property that has changed (the sender), and the string name of the property that has changed.

+   8. Open your **Car** class, and have it implement the **INotifyPropertyChanged** interface.

The interface is located in the `System.ComponentModel` namespace (add `using System.ComponentModel` to the top of your class)

Implementing this interface adds the following event to the `Car` class:

```
    public event PropertyChangedEventHandler PropertyChanged;
```

In order for the application to be notified of the changes that occur in `Car` objects, the `PropertyChanged` event must be fired each time a property value has changed.

+   9. To implement this in the **Car** class, create a helper method called **NotifyPropertyChanged** that takes in a string property name and fires the **PropertyChanged** event for the object instance and the name of the property that has changed, like this:

```
    private void NotifyPropertyChanged(string propertyName)
    {
        if (PropertyChanged != null)
        {
            this.PropertyChanged(this,
                new PropertyChangedEventArgs(propertyName));
        }
    }
```

![](bbox=[0.015, 0.305, 0.13, 0.39])

![](bbox=[0.015, 0.475, 0.13, 0.56])
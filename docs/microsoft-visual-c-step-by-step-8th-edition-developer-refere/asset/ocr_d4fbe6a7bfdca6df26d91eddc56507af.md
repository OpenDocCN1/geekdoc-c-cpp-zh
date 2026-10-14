```
}
...
}
```

This code initiates the *DispatcherTimer* object and sets the interval for timer events to one second before it starts the timer running.

+   13. On the Build menu, click Build Solution and ensure that your app builds without errors.

You can now use the *Command* class to add commands to the *ViewModel* class. In the next exercise, you will define commands to enable a user to move between customers in the view.

# Add *NextCustomer* and *PreviousCustomer* commands to the *ViewModel* class

+   1. In Visual Studio, open the ViewModel.cs file in the Code and Text Editor window.

+   2. Add the following *using* directive to the top of the file and modify the definition of the *ViewModel* class to implement the *INotifyPropertyChanged* interface.

Click here to view code image

```
...
using System.ComponentModel;

namespace Customers
{
    public class ViewModel : INotifyPropertyChanged
    {
        ...
    }
}
```

+   3. Add the *PropertyChanged* event and *OnPropertyChanged* method to the end of the *ViewModel* class. This is the same code that you included in the *Customer* class.

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    ...
    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName)
    {
        if (PropertyChanged != null)
        {
            PropertyChanged(this,
                new PropertyChangedEventArgs(propertyName));
        }
    }
```

```xml
Text="Binding Current.EmailAddress, Mode=TwoWay" ... />
... 
<TextBox Grid.Row="5" Grid.Column="3" x:Name="phone" ...
Text="Binding Current.Phone, Mode=TwoWay " ... />
</Grid>
<Grid x:Name="customersColumnarView" Margin="20,10,20,110" ...>
```

```xml
<TextBox Grid.Row="0" Grid.Column="1" x:Name="cid"
Text="Binding Current.CustomerID, Mode=TwoWay" ... />
<TextBox Grid.Row="2" Grid.Column="1" x:Name="cFirstName"
Text="Binding Current.FirstName, Mode=TwoWay" ... />
<TextBox Grid.Row="3" Grid.Column="1" x:Name="cLastName"
Text="Binding Current.LastName, Mode=TwoWay" ... />
<ComboBox Grid.Row="1" Grid.Column="1" x:Name="cTitle"
SelectedValue="Binding Current.Title, Mode=TwoWay" />
</ComboBox>
```

```xml
<TextBox Grid.Row="4" Grid.Column="1" x:Name="cEmail"
Text="Binding Current.EmailAddress, Mode=TwoWay" ... />
<TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone"
Text="Binding Current.Phone, Mode=TwoWay" ... />
</Grid>
```

11. On the Debug menu, select Start Debugging to build and run the app.

12. Verify that the app displays the details of John Sharp (the first customer in the customers list). Change the details of the customer and switch between views to prove that the data binding is still functioning correctly.

13. Return to Visual Studio and stop debugging.

The ViewModel provides access to customer information through the Current property; currently, it does not supply a way to navigate between customers. You can implement methods that increase and decrement the currentCustomer variable so that the Current property retrieves different customers, but you should do so in a manner that does not tie the view to the ViewModel.

The commonly accepted technique is to use the Command pattern. In this pattern, the ViewModel exposes methods in the form of commands that the view can invoke. The trick is to avoid explicitly referencing these methods by name in the code for view. To do this, XAML makes it possible for you to declaratively bind commands to the actions triggered by controls in the UI, as you'll see in the exercises in the next section.

# Adding commands to a ViewModel

The XAML markup that binds the action of a control to a command requires that commands exposed by a ViewModel implement the ICommand interface. This interface defines the following items:

- CanExecute: This method returns a Boolean value indicating whether the command can run. Using this method, a ViewModel can enable or disable a command depending on the context. For example, a command that fetches the next customer from a list should be able to run only if there's a next customer to fetch; if there are no more customers, the command should be disabled.
- Execute: This method runs when the command is invoked.
- CanExecuteChanged: This event is triggered when the state of the ViewModel changes. Under these circumstances, commands that could previously run might now be disabled and vice versa. For example, if the UI invokes a command that fetches the next customer from a list, and if customer is the last customer, then subsequent calls to CanExecute return false. In these circumstances, the CanExecuteChanged event should fire to indicate that the command has been disabled.

In the next exercise, you'll create a generic class that implements the ICommand interface.

# To implement the Command class

1. In Visual Studio, right-click the Customers project, point to Add, and then select Class.
2. In the Add New Item – Customers dialog, select the Class template. In the Name box, type Command.cs, and select Add.
3. In the Code and Editor window displaying the Command.cs file, add the following using directive to the list at the top of the file:
4. Make the Command class public and specify that it implements the ICommand interface, as follows in bold:

Click here to view code image

```csharp
using System.Windows;
```

The ICommand interface is defined in this namespace.

Click here to view image

```csharp
public class Command : ICommand
{
}
```

5. Add the following private fields to the Command class:

Click here to view image

```csharp
public class Command : ICommand
{
  private Action methodExecute = null;
  private Func<bool> methodToDetectExecute = null;
}
```

The Action and Func types are briefly described in Chapter 20, “Decoupling application logic and handling events.” The Action is a delegate that you can use to reference a method that takes no parameters and doesn’t return a value. The Func<T> type is also a delegate that can reference a method that takes no parameters but returns a value of the type specified by the parameter T.

In this class, you'll use the methodExecute field to reference the code that the Command object will run when it's invoked by the view. The methodToDetectCanExecute field will be used to reference the method that detects whether the command can run. (It may be disabled for some reason, depending on the state of the app or the data.)

6. Add a constructor to the Command class. This constructor should take two parameters: an Action object and a Func<T> object. Assign these parameters to the methodExecute and methodToDetectCanExecute fields, as shown here in:

Click here to view image

```csharp
public class Command : ICommand
{
  public Command(Action methodExecute, Func<bool> methodToDetectExecute)
  {
    this.methodExecute = methodExecute;
    this.methodToDetectExecute = methodToDetectExecute;
  }
}
```

7. Implement the Execute and CanExecute methods of the Command class using the methodExecute and methodToDetectCanExecute fields, as follows:

Click here to view image

```csharp
public class Command : ICommand
{
  public void Execute(object parameter)
  {
    methodExecute?.Invoke();
  }

  public bool CanExecute(object parameter)
  {
    return methodToDetectExecute?.Invoke() ?? false;
  }
}
```

The ViewModel will create an instance of the Command for the command. The ViewModel will supply the method to run and the method to detect whether the command can be enabled.

8. Add the CanExecuteChanged event to the Command class:

Click here to view image

```csharp
public class Command : ICommand
{
  public bool CanExecute(object parameter)
  {
    ...
  }
  public event EventHandler CanExecuteChanged;
}
```

When you bind a command to a control, the control subscribes to this event. This event raises the theExecute event when the state of the object changes. The simplest strategy is to use a timer to raise the CanExecute event every second.

9. Add the following using directive to the list at the top of the file:

Click here to view image

```csharp
using System.UI.Xaml;
```

10. Add the following field to the Command class before the constructor:

Click here to view image

```csharp
public class Command : ICommand
{
    private Func<bool> methodToDetectExecute = null;
    private DispatcherTimer canExecuteEventTimer = null;
    public Command(Action methodExecute, Func<bool> methodToDetectExecute)
    {
        ...
    }
}
```

11. Add the canExecuteEventHandler_Tick method shown in bold in the following code to end of the Command class:

Click here to view image

```csharp
public class Command : ICommand
{
  ...
  public event EventHandler CanExecuteChanged;

  void canExecuteEventHandler_Tick(object sender, object e)
  {
    if (this.CanExecuteChanged != null)
      this.CanExecuteChanged(this, EventArgs.Empty);
  }
}
```

12. In the Command constructor, add the following statements shown in bold:

Click here to view image

```csharp
public class Command : ICommand
{
  ...
  public Command(Action methodExecute, Func<bool> methodToDetectExecute)
  {
    this.methodExecute = methodExecute;
    this.methodToDetectExecute = methodToDetectExecute;

    this.canExecuteEventTimer = new DispatcherTimer();
    this.canExecuteEventTimer.Tick += canExecuteEventHandler_Tick;
    this.canExecuteEventTimer.Interval = new TimeSpan(0, 0, 1);
    this.canExecuteEventTimer.Start();
  }
}
```

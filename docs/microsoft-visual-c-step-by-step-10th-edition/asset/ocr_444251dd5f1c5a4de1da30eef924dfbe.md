Despite the change in the data binding to two-way mode, the email address displayed in the narrow view hasn't been updated; it's still john@contoso.com.

+   4. Return to Visual Studio and stop debugging.

Clearly, nothing is working correctly! The problem now is that the data hasn't been updated but rather the view isn't displaying the latest version of the data. If you reinstate the breakpoint in the set accessor for the EmailAddress property of the Customer class and run the app in the debugger, you'll see the debugger reach the breakpoint whenever you change the value of the email address and move the focus away from the TextBox control.) Despite appearances, the data-binding process is not magic, and a data binding doesn't know when the value to which it has bound changed. The object needs to inform the data binding of any modifications by sending a PropertyChanged event to the UI. This event is part of an interface named INotifyPropertyChanged, and all objects that support two-way data binding should implement this. You'll implement this interface in the next exercise.

# To implement the INotifyPropertyChanged interface in the Customer class

+   1. In Visual Studio, display the Customer.cs file in the Code and Text Editor window.

+   2. Add the following using directive to the list at the top of the file:

Click here to view code image

```
using System.ComponentModel;
```

The INotifyPropertyChanged interface is defined in this namespace.

+   3. Modify the definition of the Customer class to specify that it implements the INotifyPropertyChanged interface, as shown in bold:

Click here to view code image

```
public class Customer : INotifyPropertyChanged
{
}
```

+   4. After the Phone property at the end of the Customer class, add the PropertyChanged event shown in bold in the following code:
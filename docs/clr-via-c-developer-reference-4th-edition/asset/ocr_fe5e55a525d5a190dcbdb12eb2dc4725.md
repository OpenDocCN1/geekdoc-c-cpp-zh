To turn on code contract features, select the Perform Runtime Checking check box and select From from the combo box next to it. This defines the CONTRACTS_FULL symbol when you build your project and invokes the appropriate tools (described shortly) after building your project. Now, at run time, when a contract is violated, Contract'sFailed event is raised. Usually, developers do not register any methods with this event, but if you do, then any methods you register receive a ContractFailedEventArgs object that looks like this.

```
public sealed class ContractFailedEventArgs : EventArgs {
    public ContractFailedEventArgs(ContractFailureKind kind,
                                    String message, String condition, Exception originalException) {

    public ContractFailureKind Kind { get; }
    public String Message { get; }
    public String Condition { get; }
    public Exception OriginalException { get; }

    public bool SetHandled { get; set; } // true if any handler called SetHandled
    public void SetHandled(); // Call to ignore the violation; sets Handled to true

    public bool Unwind { get; set; } // true if any handler called SetUnwind
    public void SetUnwind(); // Call to force Contractexception; sets Unwind to true
}
```

Multiple handlers can be registered with this event. Each method can process the contract violation any way it chooses. For example, a handler can ignore the violation (by calling SetHandled), or terminate the process. If any method calls SetHandled, then the violation will be considered handled, and after all the handlers return, the application code is allowed to continue running unless any handler calls SetUnwind. If a handler calls SetUnwind, then, after all the handlers have completed running, a System.Diagnostics.Contracts.ContractException is thrown. This type is internal to MSCorLib.dll and therefore you cannot write a catch block to catch it explicitly. Also note that if any handler throws an unhandled exception, then the remaining handler methods are invoked and then a ContractException is thrown.

If there are no event handlers or none of them call SetHandled, SetUnwind, or throw an unhandled exception, then default processing of the contract violation happens next. If the CLR is running an application on a non-interactive window station (which would be the case for a Windows service application), then Environment.FailFast is called to instantly terminate the process. If you compile with the Assert On Contract Failure check box selected, then an alert dialog will appear allowing you to connect a debugger to your application. If this option is not selected, then a ContractException is thrown.

Let's look at a sample class that uses code contracts.

```
public sealed class Item { /* ... */ }

```

```
public sealed class ShoppingCart {
    private List<Item> m_cart = new List<Item>();
    private Decimal m_totalCost = 0;
}
```
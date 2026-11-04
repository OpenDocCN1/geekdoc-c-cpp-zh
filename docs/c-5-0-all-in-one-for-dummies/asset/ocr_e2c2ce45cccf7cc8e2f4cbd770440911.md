# Dependency Injection (DI)

The ViewModel in this example *depends* on getting customer and sales region data. But hard-coding the fake repositories isn't a very good idea in the wild. More than once have I released a piece of software with a test value still in the code! "I'll change that back before I release" tends to be forgotten in the release two-step.

Dependency Injection is a technique that *injects* required dependencies into the class that needs them. This helps prevent just such a scenario. A common tool for DI with WPF is Unity, but several other high-quality open source tools exist, such as Ninject. And it's not that hard in most cases to roll your own DI with code (see the website at http://csharp102.info). Well beyond the scope of this book, DI is an extremely valuable pattern in software development.

# Listing 4-25: The View Code-Behind

```
public partial class CustomerMaintenance : Window
{
    public CustomerMaintenance()
    {
        InitializeComponent();
        DataContext = new CustomerMaintenanceViewModel();
    }
}
```

Wait! Didn't we say you want to remove all code from the code-behind? No, not *all* code. *Almost* all code. Event handlers stuffed with business logic, definitely. But you have to have two lines in the constructor: *InitializeComponent()*, which renders all the XAML, and the DataContext assignment. You might have cases for additional code living in the code-behind, and those cases might be perfectly valid. Just use critical thought before you start adding code in places where it can't be tested or reused.

The Command Binding expressions become very different using the ViewModel pattern. They actually become quite a bit easier as shown in Listing 4-26. Because the base class hooks the *Command* into the *CommandManager*, the need for the *Windows.CommandBindings* section is eliminated.

# Listing 4-26: The Add Customer Button XAML

```
<Button HorizontalAlignment="Right" Margin="3,0,3,0"
Command="{Binding Path=AddCustomerCmd}"
CommandParameter="{Binding Path=Customers}"
Content="{Binding RelativeSource={RelativeSource Mode=Self},Path=Command.Text}"
/>
```
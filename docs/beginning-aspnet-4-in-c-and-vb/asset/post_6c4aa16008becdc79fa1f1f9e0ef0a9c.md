
```csharp
using System.AddIn.Pipeline;
namespace Wrox.ProcSharp.MAF
{
    internal class OperationContractToViewHostAdapter: Operation
    {
        private ContractHandle handle;
        public IOperationContract Contract { get; private set; }
        public OperationContractToViewHostAdapter(IOperationContract contract)
        {
            this.Contract = contract;
            handle = new ContractHandle(contract);
        }
        public override string Name
        {
            get
            {
                return Contract.Name;
            }
        }
        public override int NumberOperands
        {
            get
            {
                return Contract.NumberOperands;
            }
        }
    }
    internal static class OperationHostAdapters
    {
        internal static IOperationContract ViewToContractAdapter(Operation view)
        {
            return ((OperationContractToViewHostAdapter)view).Contract;
        }
        internal static Operation ContractToViewAdapter(
            IOperationContract contract)
        {
            return new OperationContractToViewHostAdapter(contract);
        }
    }
}
```

code snippet HostAdapter/OperationContractToViewHostAdapter.cs.

The class CalculatorContractToViewHostAdapter implements the methods of the abstract host view Calculator class and forwards the call to the contract. Again, you can see the ContractHandle holding the reference to the contract, which is similar to the adapter from the add-in side type conversions. This time the type conversions are just in the other direction from the add-in adapters.

The attribute HostAdapter marks the class as an adapter that needs to be installed in the HostSideAdapters directory.

```csharp
using System.Collections.Generic;
using System.AddIn.Pipeline;
namespace Wrox.ProcSharp.MAF
{
    [HostAdapter]
    internal class CalculatorContractToViewHostAdapter: Calculator
    {
        private ICalculatorContract contract;
        private ContractHandle handle;
        public CalculatorContractToViewHostAdapter(ICalculatorContract contract)
        {
            this.contract = contract;
            handle = new ContractHandle(contract);
        }
        public override IList<Operation> GetOperations()
        {
            return CollectionAdapters.ToList<IOperationContract, Operation>(
                contract.GetOperations(),
                OperationHostAdapters.ContractToViewAdapter,
                OperationHostAdapters.ViewToContractAdapter);
        }
        public override double Operate(Operation operation, double[] operands)
        {
            return contract.Operate(OperationHostAdapters.ViewToContractAdapter(
                operation), operands);
        }
    }
}
```

*code snippet HostAdapter/CalculatorContractViewHostAdapter.cs*

## Calculator Host

The sample host application uses the WPF technology. You can see the user interface of this application in Figure 50-3. On top is the list of available add-ins. On the left, the operations of the active add-in are shown. As you select the operation that should be invoked, operands are shown. After entering the values for the operands, the operation of the add-in can be invoked.

The buttons on the bottom row are used to rebuild and update the add-in store, and to exit the application.

The XAML code that follows shows the tree of the user interface. With the ListBox elements, different styles with item templates are used to give a specific representation of the list of add-ins, the list of operations, and the list of operands.

![](img/d7d2ffa0a76feaab821930e95daace93_1628_0.png)

**FIGURE 50-3**

![](img/d7d2ffa0a76feaab821930e95daace93_1628_1.png)

```xml
<DockPanel>
    <GroupBox Header="AddIn Store" DockPanel.Dock="Bottom">
        <UniformGrid Columns="4">
            <Button x:Name="rebuildStore" Click="RebuildStore"
                    Margin="5">Rebuild</Button>
            <Button x:Name="updateStore" Click="UpdateStore"
                    Margin="5">Update</Button>
            <Button x:Name="refresh" Click="RefreshAddIns"
                    Margin="5">Refresh</Button>
            <Button x:Name="exit" Click="App_Exit" Margin="5">Exit</Button>
        </UniformGrid>
    </GroupBox>
    <GroupBox Header="AddIns" DockPanel.Dock="Top">
        <ListBox x:Name="listAddIns" ItemsSource="{Binding}"
                 Style="{StaticResource listAddInsStyle}" />
    </GroupBox>
    <GroupBox DockPanel.Dock="Left" Header="Operations">
        <ListBox x:Name="listOperations" ItemsSource="{Binding}"
                 Style="{StaticResource listOperationsStyle}" />
    </GroupBox>
```

To update the cache of the add-in store, the UpdateStore() and RebuildStore() methods are mapped to the Click events of the Update and Rebuild buttons. Within the implementation of these methods, the Rebuild() or Update() methods of the AddInStore class are used. These methods return a string array of warnings if assemblies are stored in the wrong directories. Because of the complexity of the pipeline structure, there's a good chance that the first time you may not get the project configuration completely right for copying the assemblies to the correct directories. Reading the returned information from these methods, you will get a clear explanation about what's wrong. For example, the message "No usable AddInAdapter parts could be found in assembly Pipeline\AddInSideAdapters\CalcView.dll" gives you a hint that the assembly CalcView is stored in the wrong directory.

```csharp
private void UpdateStore(object sender, RoutedEventArgs e)
{
    string[] messages = AddInStore.Update(Settings.Default.PipelinePath);
    if (messages.Length != 0)
    {
        MessageBox.Show(string.Join("\n", messages),
            "AddInStore Warnings", MessageBoxButton.OK,
            MessageBoxImage.Warning);
    }
}
private void RebuildStore(object sender, RoutedEventArgs e)
{
    string[] messages =
        AddInStore.Rebuild(Settings.Default.PipelinePath);
    if (messages.Length != 0)
    {
        MessageBox.Show(string.Join("\n", messages),
            "AddInStore Warnings", MessageBoxButton.OK,
            MessageBoxImage.Warning);
    }
}
```

In Figure 50-3, you can see an Activate button beside the available add-in. Clicking this button invokes the handler method ActivateAddIn(). With this implementation, the add-in is activated by using the Activate() method of the AddInToken class. Here, the add-in is loaded inside a new process that is created with the AddInProcess class. This class starts the process AddInProcess32.exe. Setting the KeepAlive property of the process to false, the process is stopped as soon as the last add-in reference is garbage collected. The parameter AddInSecurityLevel.Internet leads to an add-in running with restricted permissions. The last statement of ActivateAddIn invokes the ListOperations() method, which in turn invokes the GetOperations() method of the add-in. GetOperations() assigns the returned list to the data context of the ListBox listOperations for displaying all operations.

```csharp
private void ActivateAddIn(object sender, RoutedEventArgs e)
{
    FrameworkElement el = sender as FrameworkElement;
    Trace.Assert(el != null, "ActivateAddIn invoked from the wrong " +
        "control type");

    AddInToken addIn = el.Tag as AddInToken;
    Trace.Assert(el.Tag != null, String.Format(
        "An AddInToken must be assigned to the Tag property " +
        "of the control {0}", el.Name);

    AddInProcess process = new AddInProcess();
    process.KeepAlive = false;

    activeAddIn = addIn.Activate<Calculator>(process,
        AddInSecurityLevel.Internet);
    ListOperations();
}
```

## SUMMARY

In this chapter, you've learned the concepts of a new .NET 3.5 technology: the Managed Add-In Framework.

MAF uses a pipeline concept to create complete independence between the hosting and add-in assemblies. A clearly defined contract separates the host view from the add-in view. Adapters make it possible for both sides to change independently of each other.

The next chapter provides information on how to use .NET components with .NET Enterprise Services.

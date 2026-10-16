![](bbox=[0.105, 0.062, 0.895, 0.44])

# Figure 26.6

For every part type, a separate import, manager, and view model is created. For using the part implementing the ICalculator interface, the CalculatorImport is used to define the Import, the CalculatorManager is used to create the CompositionHost and load the parts, and the CalculatorViewModel is used to define the properties and commands that are bound to the user interface. For using the part implementing the ICalculatorExtension interface, the CalculatorExtensionImport, CalculatorExtensionManager, and CalculatorExtensionViewModel are defined accordingly.

Let’s start with the CalculatorImport class. With the first sample, just a property has been defined with the Program class to import a part. It’s a good practice to define a separate class for imports. With this class, you can also define a method that is annotated with the attribute OnImportsSatisfied. This attribute marks the method that is called when imports are matched. In the sample code, the event ImportsSatisfied is fired. The Calculator property has the Import attribute applied. Here, the type is Lazy<ICalculator> for late instantiation. The part is instantiated only when the value of the Lazy type is accessed (code file UICalculator/CalculatorViewModels/CalculatorImport.cs):

```
public class CalculatorImport
{
    public event EventHandler<ImportEventArgs> ImportsSatisfied;

    [Import]
    public Lazy<ICalculator> Calculator { get; set; }
}
```
```
{
    public string Title { get; set; }
    public string Description { get; set; }
    public string ImageUri { get; set; }
}
```

With a part, the CalculatorExtensionMetadata attribute is applied. The following is an example—the FuelCalculatorExtension (code file UICalculator/FuelEconomyShared/FuelCalculatorExtension.cs):

```
[Export(typeof(ICalculatorExtension))]
[CalculatorExtensionMetadata(
    Title ="Fuel Economy",
    Description ="Calculate fuel economy",
    ImageUri ="Images/Fuel.png")]
public class FuelCalculatorExtension: ICalculatorExtension
{
    private object _control;
    public object UI => _control ?? (_control = new FuelEconomyUC());
}
```

Parts can consume a large amount of memory. If the user does not instantiate the part, there’s no need to consume this memory. Instead, the title, description, and image can be accessed to give the user information about the part before instantiating it.

# Importing Parts

Now let’s take a look at using the user control parts with a hosting application. The design view of the WPF hosting application is shown in Figure 26.6.
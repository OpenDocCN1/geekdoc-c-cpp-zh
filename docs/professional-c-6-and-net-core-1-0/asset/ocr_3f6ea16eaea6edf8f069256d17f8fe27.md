```
private object _control;
public object UI =>
	_control ?? (_control = new TemperatureConversionUC());
}
```

For now, ignore the CalculatorExtension attribute used in the previous code snippet. It is explained in the section “Exporting Metadata” later in this chapter.

The second user control that implements the interface ICalculatorExtension is FuelEconomy. With this control, either miles per gallon or liters per 100 km can be calculated. The user interface is shown in Figure 26.5.

![](bbox=[0.05, 0.5, 0.95, 0.72])

The next code snippet shows the class FuelEconomyViewModel, which defines several properties that are bound from the user interface, such as a list of FuelEcoTypes that enables the user to select between miles and kilometers, and the Fuel and Distance properties, which are filled by the user (code file UI Calculator/FuelEconomyShared/FuelEconomyViewModel.cs):

```
public class FuelEconomyViewModel: BindableBase
{
	public FuelEconomyViewModel()
	{
		InitializeFuelEcoTypes();
		CalculateCommand = new DelegateCommand(OnCalculate);
	}
}
```
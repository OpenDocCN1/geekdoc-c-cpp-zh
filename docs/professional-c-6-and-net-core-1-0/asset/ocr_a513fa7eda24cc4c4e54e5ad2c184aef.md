```
get { return _fromValue; }
set { SetProperty(ref _fromValue, value); }
}

private string _toValue;
public string ToValue
{
    get { return _toValue; }
    set { SetProperty(ref _toValue, value); }
}

private TempConversionType _fromType;
public TempConversionType FromType
{
    get { return _fromType; }
    set { SetProperty(ref _fromType, value); }
}

private TempConversionType _toType;
public TempConversionType ToType
{
    get { return _toType; }
    set { SetProperty(ref _toType, value); }
}

public void OnCalculate()
{
    double result = FromCelsiusTo(
        ToCelsiusFrom(double.Parse(FromValue), FromType), ToType);
    ToValue = result.ToString();
}
```

So far, this control is just a simple user interface control with a view model. To create a part, the class TemperatureCalculatorExtension is exported by using the Export attribute. The class implements the interface ICalculatorExtension to return the user control TemperatureConversion from the UI property. For UWP and WPF, different binary code gets generated. Both the UWP and WPF projects define the TemperatureConversionUC control class, but with different namespaces. The namespace selection is done with preprocessor directives (code file

```
UICalculator/TemperatureConversion/TemperatureCalculatorExtension
```

```
#if WPF
using TemperatureConversionWPF;
#endif
#if WINDOWS_UWP
using TemperatureConversionUWP;
#endif
using System.Composition;

namespace Wrox.ProCSharp.Composition
{
    [Export(typeof(ICalculatorExtension))]
    [CalculatorExtensionMetadata(
        Title ="Temperature Conversion",
        Description ="Temperature conversion",
        ImageUri ="Images/Temperature.png")]
    public class TemperatureConversionExtension:
ICalculatorExtension
    {
```
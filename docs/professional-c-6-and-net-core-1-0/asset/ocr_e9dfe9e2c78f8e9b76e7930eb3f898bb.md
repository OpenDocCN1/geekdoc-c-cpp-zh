# Creating Parts

The WPF User Control library named `TemperatureConversionWPF` defines a user interface as shown in [Figure 26.4](#figure-264). This control provides conversion between Celsius, Fahrenheit, and Kelvin scales. You use the first and second combo box to select the conversion source and target. Clicking the Calculate button starts the calculation to do the conversion.

![](bbox=[0.136, 0.21, 0.865, 0.657])

**Figure 26.4**

For UWP, a library named `TemperatureConversionUWP` is defined as well. Both of these projects share the common code in a shared library, `TemperatureConversionShared`. All the C# code used by these UI add-ins is really in this shared project. The XAML code for the UI differs, and it is defined in the WPF and UWP projects.

The user control has a simple implementation for temperature conversion. The enumeration `TempConversionType` defines the different conversions that are possible with that control. The enumeration values shown in the two combo boxes are bound to the `TemperatureConversionTypes` property in the `TemperatureConversionViewModel`. The method `ToCelsiusFrom` converts the argument `t` from its original value to Celsius. The temperature source type is defined with the second argument, `TempConversionType`.
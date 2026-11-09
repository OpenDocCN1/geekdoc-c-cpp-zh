+   2. Navigate to the Connections tab in the Inspector.

+   3. Make sure each outlet is connected to the correct text field by hovering the mouse over the connections as shown in Figure 5-6.

**Figure 5-6** Checking the outlet connections

![](bbox=[0.215, 0.209, 0.797, 0.585])

# Connecting the Controller to the Model

Create an instance of the converter class inside the `ConverterController` class in Xcode.

+   1. In the Classes folder in the Groups and Files sidebar, double-click `ConverterController.h` to open it in an editor window.

+   2. Declare a pointer to a converter object by adding the following line to your code right after the outlets are declared, before the ending bracket:

```
Converter *converter;
```

When clicked, the Convert button sends the `convert:` message to the `ConverterController` object. Complete the definition of the `convert:` method in the `ConverterController` so that it sends the `convertCurrency` message to the `Converter` instance to execute the conversion:
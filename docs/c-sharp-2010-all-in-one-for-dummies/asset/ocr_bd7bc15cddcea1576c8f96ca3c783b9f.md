Figure 2-15:
TextBlock and Label controls.

![](bbox=[0.28, 0.18, 0.48, 0.26])

ProgressBar: The final display-only control is the Progress Bar. Although technically a descendant of the RangeBase class, it does not enable user input like the Slider (see the next section). Figure 2-16 shows a progress bar sample. To have the bar in perpetual motion, set the IsIndeterminate property to True (although in Visual Studio 2010 Beta 2, this is not functioning properly — I'm sure it will be fixed by the final release of Visual Studio 2010 and .NET 4).

Figure 2-16:
Progress Bar at 50 percent.

![](bbox=[0.28, 0.52, 0.48, 0.6])

# Basic input controls

The workhorses of line of business applications are the basic input controls. You will find some of these on every Window you create, and they are very straightforward. Figure 2-17 shows all these controls on a single Window. Here are the basic input controls:

TextBox and PasswordBox: The TextBox and PasswordBox both allow for the input of standard text into the Window. The PasswordBox obfuscates the characters typed (using either the default system password character or a developer-specified character) and is used for collection of sensitive information. The TextBox exposes its contents through the Text property, the PasswordBox through the Password property.

```
<TextBox Text="Some Text"/>
<PasswordBox PasswordChar="X" Password="Some Text"/>
```

CheckBox: Check boxes represent Boolean values through the IsChecked property. The IsChecked property is nullable, which provides for three-state display (True, False, Unknown).

```
<CheckBox IsChecked="True" Content="True"/>
<CheckBox IsChecked="False" Content="False"/>
<CheckBox IsChecked="{x:Null}" Content="Null"/>
```
# Triggers | 229

```
<Setter Property="Background" Value="Yellow" />
</Trigger>
</Style.Triggers>
</Style>
<Style TargetType="ComboBox">
<Style.Triggers>
<Trigger Property="Text" Value="*">
<Setter Property="Background" Value="Yellow" />
</Trigger>
</Style.Triggers>
</Style>
```

# TextTriggers

Each of these Styles defines a Style.Triggers section that contains a single Trigger that takes action when the control's Text property is blank. When that happens, the Styles' Setter makes the controls' Background yellow to indicate that the value is required.

The TextTriggers example program in Figure 13-7 uses this code to flag required fields that have values. If a required field is blank, its background is yellow. (In Figure 13-7, Mr. Obama hasn't finished filling in his information, so the City, State, ZIP, Phone and Email fields are yellow to flag them as missing.)

![](bbox=[0.566, 0.326, 0.852, 0.517])

Figure 13-7

# EXACT MATCHES ONLY

Unfortunately, triggers only detect matches for properties and cannot handle ranges, different capitalization, or more complicated situations. For example, you cannot use a simple trigger to give TextBoxes different colors based on the values they contain (e.g., red for negative values, yellow for values between 0 and 10, and green for larger values). XAML just doesn't have the expressive power to represent these sorts of tests.

# IsMouseOver Triggers

One common type of trigger takes action when the user moves the mouse over something. These triggers execute their Setters when the IsMouseOver property is True.

The following XAML code defines an unnamed Button Style. It sets some basic values and defines a Trigger that executes when the IsMouseOver property is True. When the mouse moves over the Button, the Trigger makes the Button and makes its font larger and bold.
![](bbox=[0.108, 0.078, 0.215, 0.235])

# # HOW'D YOU DO?

Did you figure out that you specify the group and state names using the x:Name markup extension, or did you have to peek?

```
<ControlTemplate TargetType="Button">
... Visual Tree ...
<VisualStateManager.VisualStateGroups>
<VisualStateGroup x:Name="CommonStates">
<VisualState x:Name="Normal" />
<VisualState x:Name="MouseOver" />
<VisualState x:Name="Pressed" />
<VisualState x:Name="Disabled" />
</VisualStateGroup>
<VisualStateGroup x:Name="FocusStates">
<VisualState x:Name="Focused" />
<VisualState x:Name="Unfocused" />
</VisualStateGroup>
<VisualStateGroup x:Name="ValidationStates">
<VisualState x:Name="Valid" />
<VisualState x:Name="InvalidUnfocused" />
<VisualState x:Name="InvalidFocused" />
</VisualStateGroup>
</VisualStateManager.VisualStateGroups>
</ControlTemplate>
```

The VisualStateGroups collection isn't exposed directly; it's an attached property.

Each group and each state is identified by name.

![](bbox=[0.108, 0.745, 0.215, 0.885])

# # MAKE A NOTE

Unlike the parts defined in the control template, the visual states supported by a control are only documented in the “Control Styles and Templates” section of MSDN, not in the class library. At least, that’s the case as I write this. It may be different tomorrow.
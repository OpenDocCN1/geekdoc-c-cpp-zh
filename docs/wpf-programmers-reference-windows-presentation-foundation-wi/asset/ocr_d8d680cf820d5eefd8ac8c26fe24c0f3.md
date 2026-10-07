Even that might work (you could put the properties in the Control class and let every other class inherit them), but there are lots of other properties that you might need to handle similarly. For example, the DockPanel control needs to know how to dock its children; the Canvas control needs to know Top, Left, and other position properties for its children; and the Toolbar needs to know what OverflowMode to use for the items contains.

Adding all of these properties to the Control class would not clutter the class, but it would also not give you a general solution. If you create a new control that needs to know something about other controls (e.g., you make a new container class that needs to know how to arrange its children), you would need to rebuild the Control base class to accommodate the new control. I doubt that Microsoft is likely to reconcile the WPF libraries and release a special build to add your property.

> OBJECT-ORIENTED OBJECTION
Adding all of these properties to the Control class would also mess up the classes' encapsulation. It would make the Control class know a lot about other classes when it really shouldn't. Object-oriented purists would say that disqualifies this approach from the start.

Instead, WPF takes a different approach, which allows a control to provide an attached property for use by other controls. For example, the Grid control actually implements the Grid.Row and Grid.Column attached properties, and other controls can use them.

The syntax for an attached property is the name of the property provider, followed by a dot, followed by the name of the property. For example, the Grid control's Row property is called Grid.Row.

> PROPERTIES WITHOUT RESTRICTIONS
The control providing the attached property does not check to make that the property makes sense in context. For example, you can give a TextBox control a Grid.Row even if it is not contained in a Grid. In that case, the property is simply ignored.

Unfortunately, the syntax for an attached property is very similar to the syntax for a property element. For instance, the AttachedProperties example shown in Figure 9-5 uses the following XAML code. This code contains several attached properties and property elements.

```
<Grid>
  <Grid.Background>
    <LinearGradientBrush EndPoint="0.5,0" StartPoint="0.5,0">
      <GradientStop Color="Yellow" Offset="0"/>
      <GradientStop Color="Red" Offset="1"/>
    </LinearGradientBrush>
  </Grid.Background>
  <Grid.RowDefinitions>
</Grid>
```

![](bbox=[0.1, 0.833, 0.155, 0.873])
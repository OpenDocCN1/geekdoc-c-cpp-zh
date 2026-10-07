```
</Grid>
</TabItem>
<TabItem Header="Products">
<Grid>
<!-- Controls omitted. --
</Grid>
</TabItem>
<TabItem Header="Employees">
<Grid>
<!-- Controls omitted. --
</Grid>
</TabItem>
</TabControl>
```

# EXAMPLE Using a Rotated TabControl

The following code is to the previous example simple except it places the tabs on the left side of the TabControl. The code uses the styTabHeader style to rotate the headers -90 degrees so they don't take up a huge amount of space.

```
<TabControl StripPlacement="Left">
<TabControl.Resources>
<Style x:Key="styTabHeader" TargetType="TextBlock">
<Setter Property="FontSize" Value="14"/>
<Setter Property="FontWeight" Value="Bold"/>
<Setter Property="Padding" Value="4,0,4,0"/>
<Setter Property="LayoutTransform">
<Value>
<RotateTransform Angle="-90"/>
</Value>
</Setter>
</Style>
</TabControl.Resources>
<TabItem>
<TabItem.Header>
<TextBlock Text="Customers" Style="StaticResource styTabHeader"/>
</TabItem.Header>
<Grid>
<!-- Controls omitted. --
</Grid>
</TabItem>
<TabItem>
<TabItem.Header>
<TextBlock Text="Products" Style="StaticResource styTabHeader"/>
</TabItem.Header>
<Grid>
<!-- Controls omitted. --
</Grid>
</TabItem>
<TabItem>
<TabItem.Header>
<TextBlock Text="Employees" Style="StaticResource styTabHeader"/>
</TabItem.Header>
</TabControl>
```
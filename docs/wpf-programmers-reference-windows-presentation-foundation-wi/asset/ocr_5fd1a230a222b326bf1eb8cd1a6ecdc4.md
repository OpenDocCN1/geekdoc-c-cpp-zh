# Spatial Controls | 89

```
<FontSize="12">superscripts</Run>
and <Run BaselineAlignment="Subscript">
<FontSize="12">superscripts</Run>
<LineBreak/>
<Run Foreground="Red" FontWeight="Bold">
<Run.Background>
<LinearGradientBrush>
<GradientStop Offset="0" Color="White"/>
<GradientStop Offset="1" Color="Orange"/>
</LinearGradientBrush>
</Run.Background>
You can give a Run to give different text properties such as
Foreground and Background colors.
</Run>
</TextBlock>
```

![](bbox=[0.838, 0.345, 0.941, 0.365])

# ToolTip

The ToolTip displays a tooltip for another object. Figure 5-13 shows a program displaying tooltip for the "First Name" textbox that is sitting under the mouse.

While you can give a control tooltip by building a ToolTip object, it is easier to simply set the control's ToolTip property as shown in the following:

```
<TextBox Margin="80,10,12,0" VerticalAlignment="Top"
Text="Prop" Tool="The customer's first name
Name="txtFirstName" Height="21.96" />
```

![](bbox=[0.088, 0.597, 0.148, 0.671])

![](bbox=[0.558, 0.389, 0.941, 0.553])

FIGURE 5-13

![](bbox=[0.848, 0.657, 0.941, 0.671])

# SPATIAL CONTROLS

The spatial controls have an important spatial component. Some, such as BulletDecorator and GroupBox, provide spatial arrangement and decoration for other controls. Others, as ListView and ListView, use spatial positioning to show relationships among objects.

![](bbox=[0.708, 0.709, 0.941, 0.833])

FIGURE 5-14

# Border

The Border controls a border or background. It's a spatial control in the sense that it creates a space to hold its child. While that may seem like a minor accomplishment, creating separate areas
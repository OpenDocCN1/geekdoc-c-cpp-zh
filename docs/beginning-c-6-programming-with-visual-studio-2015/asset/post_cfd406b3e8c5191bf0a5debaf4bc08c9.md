
When you create a command, you must also implement code that can respond to the question, “Should this code be available to the user at the moment?” This means that when a command is associated with a button, that button can ask the command if it can execute and set its state accordingly.

A command is much more complicated to implement than an event, so you are not going to see them in use until Chapter 15, where they will be used with menu items.

## TRY IT OUT Routed Events: Ch14Ex01\MainWindow.xaml

This example builds on the example from earlier in the chapter. If you added the rows and columns earlier, you should remove them to match the XAML in this example.

1. Select the button `rotatedButton` and add the event `KeyDown`. You can do this through the Properties panel or by typing the XAML directly. Name it `rotatedButton_KeyDown`.

2. Select the Grid by clicking on its tag in the XAML View, and add the same event to it. Name it `Grid_KeyDown`.

3. Select the Window tag in the XAML View and add the event again. Name it `Window_KeyDown`.

4. Repeat Steps 1 through 3, but replace the event with `PreviewKeyDown` and change the name of the event to reflect that it is the Preview handler. The XAML should look like this:

```
<Window x:Class="Ch14Ex01.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:local="clr-namespace:Ch14Ex01"
mc:Ignorable="d"
Title="MainWindow" Height="350" Width="525" KeyDown="Window_KeyDown"
PreviewKeyDown="Window_PreviewKeyDown">
<Grid KeyDown="Grid_KeyDown" PreviewKeyDown="Grid_PreviewKeyDown"> <Button
x:Name="button" Content="Button" HorizontalAlignment="Left"
Margin="27,4,0,0" VerticalAlignment="Top" Width="75" Grid.Column="0"
Grid.Row="0"/>
<Button x:Name="rotatedButton" Content="2nd Button" Width="75" Height="22"
FontWeight="Bold" RenderTransformOrigin="0.5,0.5"
KeyDown="rotatedButton_KeyDown"
PreviewKeyDown="rotatedButton_PreviewKeyDown" Grid.Column="1"
Grid.Row="1" >
<Button.RenderTransform>
<TransformGroup>
<ScaleTransform/>
<SkewTransform/>
<RotateTransform Angle="-23.896"/>
<TranslateTransform/>
</TransformGroup>
</Button.RenderTransform>
</Button>
</Grid>
</Window>
```

5. If you typed the XAML directly, right-click each of the events and add the event handler to the code-behind by selecting the Navigate to Event Handler menu item.

6. Add this code to the event handlers:

```csharp
private void Grid_KeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("Grid handler, bubbling up");
}
private void Grid_PreviewKeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("Grid handler, tunneling down");
}
private void rotatedButton_KeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("rotatedButton handler, bubbling up");
}
private void rotatedButton_PreviewKeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("rotatedButton handler, tunneling down");
}
private void Window_KeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("Window handler, bubbling up");
}
private void Window_PreviewKeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("Window handler, tunneling down");
}
```

7. Run the application by pressing F5.

8. Select the rotated button by clicking it and pressing any key except Return, Tab, Escape, the space-bar, or the arrow keys. Observe the events being executed in turn.

9. Stop the application.

10. Go to the `Grid_PreviewKeyDown` event handler and add this line below the MessageBox line:

```csharp
e.Handled = true;
```

11. Repeat Steps 7 and 8.

## How It Works

The `KeyDown` and `PreviewKeyDown` events demonstrate bubbling and tunneling events. When you press a key with `rotatedButton` selected, you see each of the event handlers executing, one after another.

First the Preview events execute, starting with the handler on Window, then the Grid, and finally the `rotatedButton`. Then the `KeyDown` events execute, but in the opposite order, starting with the event handler on the `rotatedButton` and finishing with the handler on Window.

If you use any of the keys explicitly stated not to use in Step 8, you will notice that the Preview event is fired only on Window. This is because these are not considered input keys and are ignored by the grid and buttons.

- `StackPanel` — This control positions its child controls in a sequential horizontal or vertical layout.
- `WrapPanel` — This control positions its child controls in a sequential horizontal or vertical layout as `StackPanel`, but rather than a single row or column of controls, this control wraps its children into multiple rows or columns according to the space available.

You'll look at how to use these controls in more detail shortly. First, however, there are a few basic concepts to understand:

- How controls appear in stack order
- How to use alignment, margins, and padding to position controls and their content
- How to use the `Border` control

## Stack Order

When a container control contains multiple child controls, they are drawn in a specific stack order. You might be familiar with this concept from drawing packages. The best way to think of stack order is to imagine that each control is contained in a plate of glass, and the container contains a stack of these plates of glass. The appearance of the container, therefore, is what you would see if you looked down from the top through these layers of glass. The controls contained by the container overlap, so what you see is determined by the order of the glass plates. If a control is higher up the stack, then it will be the control that you see in the overlap area. Controls lower down may be partially or completely hidden by controls above them.

This also affects hit testing when you click on a window with the mouse. The target control will always be the one that is uppermost in the stack when considering overlapping controls. The stack order of controls is determined by the order in which they appear in the list of children for a container. The first child in a container is placed on the lowest layer in the stack, and the last child on the topmost layer. The children between the first and last child are placed on increasingly higher layers. The stack order of controls has additional implications for some of the layout controls that you can use in WPF, as you will see shortly.

## Alignment, Margins, Padding, and Dimensions

Earlier examples used the `Margin`, `HorizontalAlignment`, and `VerticalAlignment` properties to position controls in a Grid container, but without going into much detail about their use. You have also seen how you can use `Height` and `Width` to specify dimensions. These properties, along with `Padding`, which you haven't looked at yet, are useful for all of the layout controls (or most of them, as you will see), but in different ways. Different layout controls can also set default values for these properties. You'll see a lot of this by example in subsequent sections, but before doing that, it is worth covering the basics.

The two alignment properties, `HorizontalAlignment` and `VerticalAlignment`, determine how the control is aligned. `HorizontalAlignment` can be set to Left, Right, Center, or Stretch. Left and Right tend to position controls to the left or right edges of the container, Center positions controls

## DockPanel

The `DockPanel` control, as its name suggests, enables you to dock controls to one of its edges. This sort of layout should be familiar to you, even if you've never stopped to notice it before. It is how, for example, the `Ribbon` control in Word remains at the top of the Word window, or how the various windows in Visual Studio are positioned. In Visual Studio you can also change the docking of windows by dragging them around.

`DockPanel` has a single attached property that child controls can use to specify the edge to which controls dock: `DockPanel.Dock`. You can set this property to `Left`, `Top`, `Right`, or `Bottom`.

The stack order of controls in a `DockPanel` is extremely important, as every time you dock a control to an edge you also reduce the available space of subsequent child controls. For example, you might dock a toolbar to the top of a `DockPanel` and then a second toolbar to the left of the `DockPanel`. The first control would stretch across the entire top of the `DockPanel` display area, but the second control would only stretch from the bottom of the first toolbar to the bottom of the `DockPanel` along the left edge.

The last child control you specify will (usually) fill the area that remains after all the previous children have been positioned. (You can control this behavior, which is why this statement is qualified.)

When you position a control in a `DockPanel`, the area occupied by the control might be smaller than the area of the `DockPanel` that is reserved for the control. For example, if you dock a `Button` with a `Width` of 100, a `Height` of 50, and a `HorizontalAlignment` of `Left` to the top of a `DockPanel`, then there will be space to the right of the `Button` that isn't used by other docked children. In addition, if the `Button` control has a `Margin` of 20, then a total of 90 pixels at the top of the `DockPanel` will be reserved (the height of the control plus the top and bottom margins). You need to take this behavior into account when you use `DockPanel` for layout; otherwise, you can end up with unexpected results.

Figure 14-4 shows a sample `DockPanel` layout.

![](img/cf72ea860016d2d680fc085fc06f265a_453_0.png)

FIGURE 14-4

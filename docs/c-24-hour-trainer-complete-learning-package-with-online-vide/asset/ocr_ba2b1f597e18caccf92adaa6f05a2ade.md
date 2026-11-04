```
```csharp
RoutedPropertyChangedEventArgs<double> e)
{
    rotateTransform.Angle = degreesScrollBar.Value;
    degreesLabel.Content = degreesScrollBar.Value.ToString("0");
}
```
```

+   13. [WPF] Build a WPF application with a Grid that contains an Image. Give the Grid a MouseMove event handler that moves the Image to the mouse's location. (Hint: By default, the window's main Grid has a transparent background so it won't receive mouse events correctly. To fix that, set its Background brush. You can use any brush as long as it's not transparent.)

+   14. Build a Windows Forms program that displays a TrackBar and an HScrollBar. Set their Maximum properties to 10, and set the scrollbar's LargeChange property to 1. When the controls' values change at run time, display the new values in Labels.

+   15. [WPF] Make a WPF application that displays two Sliders and a ScrollBar all with Maximum set to 10. Set IsSnapToTickEnabled to True for one of the sliders. When the controls' values change at run time, display the new values in Labels.

+   16. Make a bar chart similar to the one shown in Figure 4-8. When you click the button, it should assign random values to the bars.

![](bbox=[0.205, 0.452, 0.475, 0.633])

**FIGURE 4-8**

Hints:

+   - For the bars, use Labels inside a multi-column TableLayoutPanel.

+   - To make the Labels appear at the bottom of the TableLayoutPanel, set their Anchor properties to Bottom, Left, Right.

+   - To make the Labels touch, set their Margin properties to 0, 0, 0, 0.

+   - Use code similar to the following to give random heights to the Labels. Note that the **statements in bold** are outside of the event handler.

```
```csharp
// Make a random number generator.
private Random Rand = new Random();

// Pick random values for the Labels.
private void pickValuesButton_Click(object sender, EventArgs e)
```
```
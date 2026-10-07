# SCROLLBAR

The ScrollBar controls the user select a numeric value from a range of values. Often a program doesn't need to use ScrollBars, directly, relying on controls that display them as needed such as ScrollViewer, TextBox, and FlowDocumentReader.

Occasionally, however, a ScrollBar is handy for letting the user select a value that will be used in some other way than control.

For example, the UseScrollExample program shown in Figure 7-15 uses three ScrollBars to let the user select red, green, and blue color values between 0 and 255. When any of the values change, the program displays the new value to the right of its ScrollBar and displays a sample of the color with those components on the left.

![](bbox=[0.518, 0.246, 0.871, 0.332])

FIGURE 7-15

The ScrollBar control is relatively simple. The following table summarizes the control's most useful properties:

| PROPERTY | PURPOSE |
| LargeChange | The amount by which the control's value changes when the user clicks between the draggable thumb and one of the control's arrows |
| Orientation | Vertical or Horizontal |
| Maximum | The largest value the user can select |
| Minimum | The smallest value the user can select |
| SmallChange | The amount by which the control's value changes when the user clicks on one of the control's arrows |
| Value | The control's current value |

The ScrollBar's most useful event is ValueChanged, which — as you can probably guess — fires whenever the control's value changes.

The following C# code shows the UseScrollBar program handles ValueChanged events for all of its ScrollBars. The code uses the ScrollBars' values to make a blue brush and sets the l1Sample control Background property to the brush. It displays the color values in labels.

```
// Display a color sample.
private void sbar_ValueChanged(
    object sender, RoutedPropertyChanged<double> e) {
    byte r = (byte)sbar.Red;
    byte g = (byte)sbar.Green;
    byte b = (byte)sbar.Blue;
    Color cl = Color.Rgb(r, g, b);
    SolidColorBrush br = new SolidColorBrush(cl);
}
```

- Use two ScrollBar controls, one with `Orientation = Horizontal`.

- Use a Canvas instead of a Panel and an Image instead of a PictureBox.

- Instead of catching the form's Load and Resize events, catch the Canvas control's SizeChanged event and give it the following event handler:

```csharp
// Set the scrollbar maximums to fit the Canvas.
private void fieldCanvas_SizeChanged(object sender, SizeChangedEventArgs e)
{
    mouseHScrollBar.Maximum = e.NewSize.Width;
    mouseVScrollBar.Maximum = e.NewSize.Height;
}
```

- Use the following code for the Canvas's MouseMove event handler:

```csharp
// Move the scrollbars to track the mouse.
private void Canvas_MouseMove(object sender, MouseEventArgs e)
{
    Point location = Mouse.GetPosition(fieldCanvas);
    mouseHScrollBar.Value = location.X;
    mouseVScrollBar.Value = location.Y;
}
```

- Initially position the Image control in the Canvas control's upper-left corner. Then use the following MouseDown event handler:

```csharp
// Move the mouse Image to the point clicked.
private void fieldCanvas_MouseDown(object sender, MouseButtonEventArgs e)
{
    Point location = Mouse.GetPosition(fieldCanvas);
    mouseImage.Margin = new Thickness(location.X, location.Y, 0, 0);
}
```

3. Build the DynamicEvents example program shown in Figure 4-3. What happens if you click Attach twice? Three times? What happens if you then click Detach once? Five times?

4. [WPF] Repeat Exercise 3 with a WPF application.

5. Create a form with one Button labeled "Stop" and two Timers named leftTimer and rightTimer. Set the Timers' Interval properties to 1000. At design time, set leftTimer's Enabled property to True.

    - In each Timer's Tick event handler, disable that Timer and enable the other one.
    - Make one Timer's Tick event handler also move the Button to (10, 10) by setting its Left and Top properties.
    - Make the other Timer's Tick event handler move the Button to (200, 200).
    - In the Button's Click event handler, set Enabled = false for both Timers.

    Run the program. Experiment with different values for the Timers' Interval properties. What happens if Interval = 10?

6. Copy the FollowMouse program you built for Exercise 1. Modify the copy so the user can adjust the scrollbars to move the PictureBox.

7. [WPF] Copy the program you build for Exercise 2. Modify the copy so the user can adjust the scrollbars to move the image. (Hints: To save code, use the same event handler for both scrollbars. To prevent the mouse image from appearing on top of the scrollbars and in the small area on the window's lower-right corner, set the Canvas control's ClipToBounds property to True.)

8. Make a program similar to the one shown in Figure 4-5. When the user unchecks the Breakfast, Lunch, or Dinner checkbox, the program should disable the corresponding GroupBox.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_107_0.png)

**FIGURE 4-5**

**Hints:**

- Make the OK button be the form's accept button. Make the Cancel button be the form's cancel button.
- Blank the GroupBoxes' Text properties. Then place the CheckBoxes over the GroupBoxes where their text would go. (Be sure not to place the CheckBoxes inside the GroupBoxes. Try it to see why it won't work. You may need to position the CheckBoxes first and then move the GroupBoxes into position.)
- To enable or disable a GroupBox, set its Enabled property equal to the corresponding CheckBox's Checked property as in the following code:

```csharp
// Enable or disable the corresponding GroupBox.
private void breakfastCheckBox_CheckedChanged(object sender, EventArgs e)
{
    breakfastGroupBox.Enabled = breakfastCheckBox.Checked;
}
```

9. [WPF] Repeat Exercise 8 with a WPF application. Hints:

- A WPF CheckBox doesn't display a background so the checkboxes in this program won't cover the GroupBox borders below them. To work around that problem, place each CheckBox inside a Canvas and make the Canvas use a white background.
- A GroupBox can have only a single child. Give each GroupBox a StackPanel holding RadioButtons. Use the RadioButtons' Margin properties to add some spacing between the choices.
- The WPF `CheckBox` control doesn't have a `CheckedChanged` event. Use the `Click` event instead.
- To enable or disable a `GroupBox`, set its `IsEnabled` property equal to the corresponding `CheckBox`'s `IsChecked.Value` property as in the following code:

```csharp
// Enable or disable the appropriate GroupBox.
private void breakfastCheckBox_Click(object sender, RoutedEventArgs e)
{
    breakfastGroupBox.IsEnabled = breakfastCheckBox.IsChecked.Value;
}
```

- To set a WPF window's accept button, set the Button's `IsDefault` property to `True`.
- To set a WPF window's cancel button, set the Button's `IsCancel` property to `True`.

10. Make a program similar to the one shown in Figure 4-6.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_108_0.png)

**FIGURE 4-6**

- Create a `PictureBox` and load an image into it. Set its size to match the picture's size and set its `SizeMode` property to `StretchImage`. (Also see what happens if you set this to `Normal`.)
- Position the scrollbars next to the `PictureBox`. Set their `Maximum` properties so the user can select values between 0 and the picture's width/height.
- Initially set the scrollbars' `Value` properties equal to the image's width/height.
- Make the scrollbars' `Scroll` event handlers set the `PictureBox`'s width/height equal to the scrollbars' values.

11. [WPF] Repeat Exercise 10 with a WPF application. Hints:

- Set the Image control's Stretch property to Fill. (Also see what happens if you set this to None.)
- In a WPF program, the user can set a ScrollBar to its Maximum value.

12. [WPF, Games, Hard] One thing that's hard to do in a Windows Forms application that's easy in a WPF application (at least if you set it up properly) is transforming objects. For example, it's relatively easy to scale, rotate, and skew controls. For this exercise, make a program similar to the one shown in Figure 4-7. When the user adjusts the scrollbar at the bottom, the program should rotate the image and display the angle of rotation in the Label in the lower right.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_109_0.png)

**FIGURE 4-7**

**Hints:**

- Lay out the window and its controls. Put a picture in the Image control. Name the label control degreesLabel.

- Use the Properties window's Transform section to rotate the Image by 360 degrees.

- Edit the XAML code to give the rotateTransform a property called x:Name with value rotateTransform. The Image control's code should look something like this:

```xml
<Image x:Name="image" HorizontalAlignment="Left"
VerticalAlignment="Top" Source="ScienceGirl.png"
Stretch="None" Grid.ColumnSpan="2"
Margin="10,10,0,0" RenderTransformOrigin="0.5,0.5">
<Image.RenderTransform>
<TransformGroup>
<ScaleTransform/>
<SkewTransform/>
<RotateTransform x:Name="rotateTransform" Angle="360"/>
<TranslateTransform/>
</TransformGroup>
</Image.RenderTransform>
</Image>
```

- Make the ScrollBar's ValueChanged event handler look like this:

```csharp
// Rotate the Image.
private void degreesScrollBar_ValueChanged(object sender,
    RoutedPropertyChangedEventArgs<double> e)
{
    rotateTransform.Angle = degreesScrollBar.Value;
    degreesLabel.Content = degreesScrollBar.Value.ToString("0");
}
```

13. [WPF] Build a WPF application with a Grid that contains an Image. Give the Grid a MouseMove event handler that moves the Image to the mouse's location. (Hint: By default, the window's main Grid has a transparent background so it won't receive mouse events correctly. To fix that, set its Background brush. You can use any brush as long as it's not transparent.)

14. Build a Windows Forms program that displays a TrackBar and an HScrollBar. Set their Maximum properties to 10, and set the scrollbar's LargeChange property to 1. When the controls' values change at run time, display the new values in Labels.

15. [WPF] Make a WPF application that displays two Sliders and a ScrollBar all with Maximum set to 10. Set IsSnapToTickEnabled to True for one of the sliders. When the controls' values change at run time, display the new values in Labels.

16. Make a bar chart similar to the one shown in Figure 4-8. When you click the button, it should assign random values to the bars.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_110_0.png)

**FIGURE 4-8**

**Hints:**

- For the bars, use Labels inside a multi-column TableLayoutPanel.

- To make the Labels appear at the bottom of the TableLayoutPanel, set their Anchor properties to Bottom, Left, Right.

- To make the Labels touch, set their Margin properties to 0, 0, 0, 0.

- Use code similar to the following to give random heights to the Labels. Note that the **statements in bold** are outside of the event handler.

```csharp
// Make a random number generator.
private Random Rand = new Random();

// Pick random values for the Labels.
private void pickValuesButton_Click(object sender, EventArgs e)
```

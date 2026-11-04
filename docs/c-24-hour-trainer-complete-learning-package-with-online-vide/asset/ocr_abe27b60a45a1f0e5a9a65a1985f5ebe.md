+   - The WPF `CheckBox` control doesn't have a `CheckChanged` event. Use the `Click` event instead.
+   - To enable or disable a `GroupBox`, set its `IsEnabled` property equal to the corresponding `CheckBox`'s `IsChecked.Value` property as in the following code:
+   - To set a WPF window's accept button, set the Button's `IsDefault` property to `True`.
+   - To set a WPF window's cancel button, set the Button's `IsCancel` property to `True`.

```
// Enable or disable the appropriate GroupBox.
private void breakfastCheckBox_Click(object sender, RoutedEventArgs e)
{
    breakfastGroupBox.IsEnabled = breakfastCheckBox.IsChecked.Value;
}
```

10. Make a program similar to the one shown in Figure 4-6.

![](bbox=[0.22, 0.57, 0.48, 0.82])

FIGURE 4-6

+   - Create a `PictureBox` and load an image into it. Set its size to match the picture's size and set its `ScaleMode` property to `StretchImage`. (Also see what happens if you set this to `Normal`.)
+   - Position the scrollbars next to the `PictureBox`. Set their `Maximum` properties so the user can select values between 0 and the picture's width/height.
+   - Initially set the scrollbars' `Value` properties equal to the image's width/height.
+   - Make the scrollbars' `Scroll` event handlers set the `PictureBox`'s width/height equal to the scrollbars' values.
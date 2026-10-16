![](bbox=[0.105, 0.062, 0.894, 0.418])

# Figure 32.17

# Adaptive Triggers

The RelativePanel is a great control for alignment. However, to support multiple screen sizes and rearrange the controls depending on the screen size, you can use adaptive triggers with the RelativePanel control. For example, on a small screen the TextBox controls should be arranged below the TextBlock controls, but on a larger screen the TextBox controls should be right of the TextBlock controls.

In the following code, the RelativePanel from before is changed to remove all RelativePanel attached properties that should not apply to all screen sizes, and an optional image is added (code file LayoutSamples/Views/AdaptiveRelativePanelSample.xaml):

```
<RelativePanel ScrollViewer.VerticalScrollBarVisibility="Auto" Margin="16">
    <TextBlock x:Name="FirstNameLabel" Text="First Name" Margin="8" />
    <TextBox x:Name="FirstNameText"  Margin="8" Width="150" />
    <TextBlock x:Name="LastNameLabel" Text="Last Name" Margin="8" />
    <TextBox x:Name="LastNameText"  Margin="8" Width="150" />
    <Button Content="Save" RelativePanel.AlignBottomWithPanel="True" Margin="8" />
    <Rectangle x:Name="Image" Fill="Violet" Width="150" Height="250" Margin="8" />
    <Rectangle x:Name="OptionalImage" RelativePanel.AlignRightWithPanel="True" Fill="Red" Width="350" Height="350" Margin="8" />
</RelativePanel>
```

## RelativePanel

RelativePanel is a new panel for the UWP that allows one element to be positioned in relation to another element. If you’ve used the Grid control with definitions for rows and columns and you had to insert a row, you had to change all elements that were below the row that was inserted. The reason is that all rows and columns are indexed by numbers. This is not an issue with the RelativePanel, which enables you to place elements in relation to each other.

> NOTE Compared to the RelativePanel, the Grid control still has its advantages with auto, star, and fixed sizing. Read Chapter 34, “Windows Desktop Applications with WPF,” in which the Grid control is explained in detail. This control is covered with WPF, but you can use it in a similar way with the UWP.

The following code snippet aligns several TextBlock and TextBox controls, a Button, and a Rectangle within a RelativePanel. The TextBox elements are positioned to the right of the corresponding TextBlock elements; the Button is positioned relative to the bottom of the panel; and the Rectangle is aligned with the top with the first TextBlock and to the right of the first TextBox (code file LayoutSamples/Views/RelativePanelSample.xaml):

```xml
<RelativePanel>
    <TextBlock x:Name="FirstNameLabel" Text="First Name" Margin="8" />
    <TextBox x:Name="FirstNameText" RelativePanel.RightOf="FirstNameLabel" Margin="8" Width="150" />
    <TextBlock x:Name="LastNameLabel" Text="Last Name" RelativePanel.Below="FirstNameLabel" Margin="8" />
    <TextBox x:Name="LastNameText" RelativePanel.RightOf="LastNameLabel" Margin="8" RelativePanel.Below="FirstNameText" Width="150" />
    <Button Content="Save" RelativePanel.AlignHorizontalCenterWith="LastNameText" RelativePanel.AlignBottomWithPanel="True" Margin="8" />
    <Rectangle x:Name="Image" Fill="Violet" Width="150" Height="250" RelativePanel.AlignTopWith="FirstNameLabel" RelativePanel.RightOf="FirstNameText" Margin="8" />
</RelativePanel>
```

Figure 32.17 shows the alignment of the controls when you run the application.

![](img/3d365b72b289213a91ade7eb366b8f35_1217_0.png)

### Figure 32.17

## Adaptive Triggers

The RelativePanel is a great control for alignment. However, to support multiple screen sizes and rearrange the controls depending on the screen size, you can use adaptive triggers with the RelativePanel control. For example, on a small screen the TextBox controls should be arranged below the TextBlock controls, but on a larger screen the TextBox controls should be right of the TextBlock controls.

In the following code, the RelativePanel from before is changed to remove all RelativePanel attached properties that should not apply to all screen sizes, and an optional image is added (code file LayoutSamples/Views/AdaptiveRelativePanelSample.xaml):

```xml
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

Using an adaptive trigger—with which the `MinWindowWidth` can be set to define when the trigger is fired—values for different properties are set to arrange the elements depending on the space available for the app. As the screen size gets smaller, the width needed by the app gets smaller as well. Moving elements below instead of beside reduces the width needed. Instead, the user can scroll down. With the smallest window width, the optional image is set collapsed (code file `LayoutSamples/Views/AdaptiveRelativePanelSample.xaml`):

```xml
<VisualStateManager.VisualStateGroups>
    <VisualStateGroup>
        <VisualState x:Name="WideState">
            <VisualState.StateTriggers>
                <AdaptiveTrigger MinWindowWidth="1024" />
            </VisualState.StateTriggers>
            <VisualState.Setters>
                <Setter Target="FirstNameText.(RelativePanel.RightOf)"
                        Value="FirstNameLabel" />
                <Setter Target="LastNameLabel.(RelativePanel.Below)"
                        Value="FirstNameLabel" />
                <Setter Target="LastNameText.(RelativePanel.Below)"
                        Value="FirstNameText" />
                <Setter Target="LastNameText.(RelativePanel.RightOf)"
                        Value="LastNameLabel" />
                <Setter Target="Image.(RelativePanel.AlignTopWith)"
                        Value="FirstNameLabel" />
                <Setter Target="Image.(RelativePanel.RightOf)"
                        Value="FirstNameText" />
            </VisualState.Setters>
        </VisualState>

        <VisualState x:Name="MediumState">
            <VisualState.StateTriggers>
                <AdaptiveTrigger MinWindowWidth="720" />
            </VisualState.StateTriggers>
            <VisualState.Setters>
                <Setter Target="FirstNameText.(RelativePanel.RightOf)"
                        Value="FirstNameLabel" />
                <Setter Target="LastNameLabel.(RelativePanel.Below)"
                        Value="FirstNameLabel" />
                <Setter Target="LastNameText.(RelativePanel.Below)"
                        Value="FirstNameText" />
                <Setter Target="LastNameText.(RelativePanel.RightOf)"
                        Value="LastNameLabel" />
                <Setter Target="Image.(RelativePanel.Below)"
                        Value="LastNameText" />
                <Setter Target="Image.(RelativePanel.AlignHorizontalCenterWith)"
                        Value="LastNameText" />
            </VisualState.Setters>
        </VisualState>

        <VisualState x:Name="NarrowState">
            <VisualState.StateTriggers>
                <AdaptiveTrigger MinWindowWidth="320" />
            </VisualState.StateTriggers>
            <VisualState.Setters>
                <Setter Target="FirstNameText.(RelativePanel.Below)"
                        Value="FirstNameLabel" />
                <Setter Target="LastNameLabel.(RelativePanel.Below)"
                        Value="FirstNameText" />
                <Setter Target="LastNameText.(RelativePanel.Below)"
                        Value="LastNameLabel" />
                <Setter Target="Image.(RelativePanel.Below)"
                        Value="LastNameText" />
                <Setter Target="OptionalImage.Visibility"
                        Value="Collapsed" />
            </VisualState.Setters>
        </VisualState>
    </VisualStateGroup>
</VisualStateManager.VisualStateGroups>
```

You can establish the minimum window width needed by the application by setting the SetPreferredMinSize with the ApplicationView class (code file LayoutSamples/App.xaml.cs):

```csharp
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    ApplicationView.GetForCurrentView().SetPreferredMinSize(
        new Size { Width = 320, Height = 300 });
    // etc.
}
```

When you run the application, you can see different layout arrangements with the smallest width (see Figure 32.18), a medium width (see Figure 32.19), and the maximum width (see Figure 32.20).

![](img/3d365b72b289213a91ade7eb366b8f35_1219_0.png)

### Figure 32.18

### Figure 32.19

### Figure 32.20

The adaptive trigger is also good to use to change the look of the SplitView to CompactInline or Overlay mode (code file AppShellSample/AppShell.xaml):

```xml
<VisualStateManager.VisualStateGroups>
    <VisualStateGroup>
        <VisualState>
            <VisualState.StateTriggers>
                <AdaptiveTrigger MinWindowWidth="720" />
            </VisualState.StateTriggers>
            <VisualState.Setters>
                <Setter Target="RootSplitView.DisplayMode" Value="CompactInline"/>
                <Setter Target="RootSplitView.IsPaneOpen" Value="True"/>
            </VisualState.Setters>
        </VisualState>
        <VisualState>
            <VisualState.StateTriggers>
```


After the project has been created, click the Project > Open in Expression Blend menu item. If it takes a few seconds to load up Blend, don’t worry. The first time you launch Blend might be slow, even on a powerful computer with a fast hard drive.

Next we need to add a button. Expand the Assets pane by clicking the right-facing chevron (it looks like two greater-than signs: >>) in the far left toolbar. Go to the Categories section on the left and click Panels. Click and hold on the StackPanel icon and then drag the mouse pointer to the Grid control named ContentPanel. When you let go, a StackPanel will have been added to the Grid. Next, create a button inside this StackPanel. To do this, make sure the StackPanel is highlighted and double-click the Button shortcut on the left toolbar. Make sure you give this Button a name by setting the name in the Properties pane on the right side of the editor.

Now right-click the Button (either in the Objects and Timeline pane or the visual button itself on the design surface) and choose Edit Template; then left-click Edit a Copy. Click OK when prompted to create a style resource. This will allow you to visually edit the control’s template.

Now switch to the States tab in the top pane (the one that normally has the Projects tab selected). Inside the Objects and Timeline pane for the current control template, select ButtonBackground. You will then see all the prebuilt visual states for this control, as shown in Figure 7.6.

![](img/04a00d46bb1059867d95707babd62ee7_89_0.png)

Figure 7.6 Changing visual states of stock controls.

Click the Pressed state and you’ll see a message that Blend is now recording properties for the Pressed state. This means that while you are recording for this state, any property change made to the control or any of its nested properties will be saved as part of that visual state. We can now change the Background and BorderBrush properties of the button in this state without affecting those properties in the Normal or Disabled states.

At this point you can save your work and run the application by clicking Project, Run, or pressing the F5 key. Running the application will launch the Windows Phone 7 simulator. This simulator provides you with a very close representation of what your application might look like and how it might behave on an actual device.

The first time you launch an application after your computer starts up, it will take some time for the WP7 simulator to start. After it has done its initial startup, you can leave it running between debug sessions. This will cut down on the time it takes to start debugging your application.

After a few seconds of the simulator doing its initialization, your application will appear. Because the default Button control knows to put itself into the Pressed state when someone taps on the control, you don’t need to do any of that plumbing yourself. Because we’ve just styled the visual state, our new button will now turn green with an orange border when someone taps it.

When you’re done playing with this new button, take a look at the XAML inside MainPage.xaml (you can see this XAML by going back into Visual Studio and double-clicking the file) at the top in the newly created resource dictionary:

```
<Style x:Key="FancyButtonStyle" TargetType="Button">
<Setter Property="Background" Value="Transparent"/>
<Setter Property="BorderBrush"
Value="{StaticResource PhoneForegroundBrush}"/>
<Setter Property="Foreground"
Value="{StaticResource PhoneForegroundBrush}"/>
<Setter Property="BorderThickness"
Value="{StaticResource PhoneBorderThickness}"/>
<Setter Property="FontFamily"
Value="{StaticResource PhoneFontFamilySemiBold}"/>
<Setter Property="FontSize"
Value="{StaticResource PhoneFontSizeMediumLarge}"/>
<Setter Property="Padding" Value="10,3,10,5"/>
<Setter Property="Template">
<Setter.Value>
<ControlTemplate TargetType="Button">
<Grid Background="Transparent">
<VisualStateManager.VisualStateGroups>
<VisualStateGroup x:Name="CommonStates">
<VisualState x:Name="Normal"/>
<VisualState x:Name="MouseOver"/>
<VisualState x:Name="Pressed">
<Storyboard>
<ObjectAnimationUsingKeyFrames
Storyboard.TargetProperty="Foreground"
Storyboard.TargetName="ContentContainer">
<DiscreteObjectKeyframe KeyTime="0"
Value="{StaticResource PhoneBackgroundBrush}"/>
</ObjectAnimationUsingKeyFrames>
<ColorAnimation Duration="0" To="#FF001BFF"
    Storyboard.TargetProperty=
    "(Border.BorderBrush).(SolidColorBrush.Color)"
    Storyboard.TargetName="ButtonBackground" d:IsOptimized="True"/>
<ColorAnimation Duration="0" To="#FFFFC700"
    Storyboard.TargetProperty=
    "(Border.Background).(SolidColorBrush.Color)"
    Storyboard.TargetName="ButtonBackground" d:IsOptimized="True"/>
</Storyboard>
</VisualState>
<VisualState x:Name="Disabled">
    <Storyboard>
        <ObjectAnimationUsingKeyFrames
            Storyboard.TargetProperty="Foreground"
            Storyboard.TargetName="ContentContainer">
            <DiscreteObjectKeyFrame KeyTime="0"
                Value="{StaticResource PhoneDisabledBrush}"/>
        </ObjectAnimationUsingKeyFrames>
    </Storyboard>
</VisualState>
</VisualStateGroup>
</VisualStateManager.VisualStateGroups>
<Border x:Name="ButtonBackground"
    BorderThickness="{TemplateBinding BorderThickness}" CornerRadius="0"
    Margin="{StaticResource PhoneTouchTargetOverhang}" Background="Black">
<Border.BorderBrush>
    <SolidColorBrush Color="{StaticResource PhoneForegroundColor}"/>
</Border.BorderBrush>
<ContentControl x:Name="ContentContainer"
    ContentTemplate="{TemplateBinding ContentTemplate}"
    Content="{TemplateBinding Content}"
    Foreground="{TemplateBinding Foreground}"
    HorizontalContentAlignment=
    "{TemplateBinding HorizontalContentAlignment}"
    Padding="{TemplateBinding Padding}"
    VerticalContentAlignment="{TemplateBinding VerticalContentAlignment}"/>
</Border>
</Grid>
</ControlTemplate>
</Setter.Value>
</Setter>
```

If you scan through this XAML you can see all the visual states for the new button style, and you’ll also see that we’ve modified the Pressed state. One thing especially worth noticing is that all the changes that occur to all the properties of the button occur within animation storyboards.

## Chapter 7 Introducing Expression Blend

After developers spend a few seconds thinking about the fact that transitioning between different visual states is all done smoothly with animations, they start to see the power of this framework.

This means that when a Silverlight object transitions from one visual state to another, it does so with an animated storyboard. You can control how long it takes to switch to this new state and any special effects that occur as a result of this switch.

As a curmudgeonly as I am about using visual design tools, I must admit that hand-typing in all the visual state management stuff, even for simple property changes, is going to get really old really fast. I am a firm believer in using the best tool for the job, and I know that working with visual states is absolutely best done in Blend.

Here's a little food for thought and an assignment to do some exploring on your own with Blend: Stock controls come with their own visual states, and different user interaction will switch a control between visual states. A page is just a different type of control. This means that a page can have visual states and you can create your own custom visual states.

One of the biggest pains when building UIs for the iPad and iPhone is dealing with rotation. Making sure that the user interface looks good when rotated between landscape and portrait is a difficult and time-consuming process, especially when you consider that you often need to hand-code property changes to your views when the user rotates the phone or the iPad. What if you were to assign names to your visual states such as “portrait” and “landscape” or “portraitup,” and so on? Now all you need to do in Blend is rotate the design surface to the right orientation and, in that particular visual state, record mode, move and resize all your controls accordingly. Next, you need to programmatically transition your page’s visual state every time the device changes orientation.

Here is some code you can override in your MainPage.xaml.cs that will programmatically transition the page from its current visual state to the new one, invoking any custom animations, layout changes, color changes, and whatever else you want done. Again, remember that all these changes can be done in a timed, animated storyboard.

```
protected override void OnOrientationChanged(OrientationChangedEventArgs e)
{
    // if you have 4 states instead of 2
    // PortraitUp, PortraitDown, LandscapeLeft, LandscapeDown
    // VisualStateManager.GoToState(this, e.Orientation.ToString(), true);
    // if you just have Portrait or Landscape
    string orientation = (e.Orientation & PageOrientation.Portrait) != 0
        ? "Portrait" : "Landscape";
    VisualStateManager.GoToState(this, orientation, true);
    base.OnOrientationChanged(e);
}
```

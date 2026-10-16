
```xml
Value="{StaticResource CountryDataTemplate}" />
<Setter Property="ItemContainerStyle"
    Value="{StaticResource ListViewItemStyle1}" />
<Setter Property="ItemsPanel">
    <Setter.Value>
        <ItemsPanelTemplate>
            <ItemsStackPanel Orientation="Horizontal" Background="Yellow"/>
        </ItemsPanelTemplate>
    </Setter.Value>
</Setter>
<Setter Property="Template">
    <Setter.Value>
        <ControlTemplate TargetType="ListView">
            <Border BorderBrush="{TemplateBinding BorderBrush}"
                BorderThickness="{TemplateBinding BorderThickness}"
                Background="{TemplateBinding Background}">
                <ScrollViewer x:Name="ScrollViewer">
                    <!--ScrollViewer definitions removed for clarity-->
                    <ItemsPresenter FooterTransitions="{TemplateBinding FooterTransitions}"
                        FooterTemplate="{TemplateBinding FooterTemplate}"
                        Footer="{TemplateBinding Footer}"
                        HeaderTemplate="{TemplateBinding HeaderTemplate}"
                        Header="{TemplateBinding Header}"
                        HeaderTransitions="{TemplateBinding HeaderTransitions}"
                        Padding="{TemplateBinding Padding}"/>
                </ScrollViewer>
            </Border>
        </ControlTemplate>
    </Setter.Value>
</Setter>
</Style>
```

**NOTE** With WPF, the template for the ListView control looks similar to the UWP template. The ItemsPresenter doesn't offer many properties of the UWP ItemsPresenter, such as the properties related to the transitions.

With this resource available, the definition of the ListView becomes simple as just the ListViewStyle2 needs to be referenced in addition to the ItemsSource to retrieve the data (code file Templates [WPF|UWP]/StyledList.xaml):

```xml
<ListView ItemsSource="{Binding Countries}" Margin="10"
    Style="{StaticResource ListViewStyle2}" />
```

The new view is shown in Figure 30.22. Now a scrollbar is available.

![](img/3d365b72b289213a91ade7eb366b8f35_1136_0.png)

Figure 30.22

## Animations

Using animations, you can make a smooth transition between images by using moving elements, color changes, transforms, and so on. XAML makes it easy to create animations. You can animate the value of any dependency property. Different animation classes exist to animate the values of different properties, depending on their type.

The most important element of an animation is the timeline. This element defines how a value changes over time. Different kinds of timelines are available for changing different types of values. The base class for all timelines is `Timeline`. To animate a property of type double, you can use the class `DoubleAnimation`. The `Int32Animation` is the animation class for `int` values. You use `PointAnimation` to animate points and `ColorAnimation` to animate colors.

You can combine multiple timelines by using the `Storyboard` class. The `Storyboard` class itself is derived from the base class `TimelineGroup`, which derives from `Timeline`.

> **NOTE** The namespace for animation classes is `System.Windows.Media.Animation` with WPF and `Windows.UI.Xaml.Media.Animation` with UWP apps.

### Timeline

A `Timeline` defines how a value changes over time. The following example animates the size of an ellipse. In the code that follows, `DoubleAnimation` timelines change scaling and translation of an ellipse; `ColorAnimation` changes the color of the fill brush. The `Triggers` property of the `Ellipse` class is set to an `EventTrigger`. The event trigger is fired when the ellipse is loaded. `BeginStoryboard` is a trigger action that begins the storyboard. With the storyboard, a `DoubleAnimation` element is used to animate the `ScaleX`, `ScaleY`, `TranslateX`, and `TranslateY` properties of the `CompositeTransform` class. The animation changes the horizontal scale to 5 and the vertical scale to 3 within ten seconds (code file `AnimationUWP/SimpleAnimation.xaml`):

```xml
<Ellipse x:Name="ellipse1" Width="100" Height="40"
    HorizontalAlignment="Left" VerticalAlignment="Top">
    <Ellipse.Fill>
        <SolidColorBrush Color="Green" />
    </Ellipse.Fill>
    <Ellipse.RenderTransform>
        <CompositeTransform ScaleX="1" ScaleY="1" TranslateX="0" TranslateY="0" />
    </Ellipse.RenderTransform>
    <Ellipse.Triggers>
        <EventTrigger>
            <BeginStoryboard>
                <Storyboard x:Name="MoveResizeStoryboard">
                    <DoubleAnimation Duration="0:0:10" To="5" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.ScaleX)" />
                    <DoubleAnimation Duration="0:0:10" To="3" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.ScaleY)" />
                    <DoubleAnimation Duration="0:0:10" To="400" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.TranslateX)" />
                    <DoubleAnimation Duration="0:0:10" To="200" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.TranslateY)" />
                    <ColorAnimation Duration="0:0:10" To="Red" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(Ellipse.Fill).(SolidColorBrush.Color)" />
                </Storyboard>
            </BeginStoryboard>
        </EventTrigger>
    </Ellipse.Triggers>
</Ellipse>
```

With WPF, the XAML code is slightly different. Because there isn’t a CompositeTransform element, the TransformGroup element is used (code file `AnimationWPF/SimpleAnimation.xaml`):

```xml
<Ellipse.RenderTransform>
    <TransformGroup>
        <ScaleTransform x:Name="scale1" ScaleX="1" ScaleY="1" />
        <TranslateTransform X="0" Y="0" />
    </TransformGroup>
</Ellipse.RenderTransform>
```

Using ScaleTransform and TranslateTransform results in animations accessing the collection of the TransformGroup and accessing the ScaleX, ScaleY, X, and Y properties by using an indexer:

```xml
<DoubleAnimation Duration="0:0:10" To="5" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).Children[0].(ScaleTransform.ScaleX)" />
<DoubleAnimation Duration="0:0:10" To="3" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).Children[0].(ScaleTransform.ScaleY)" />
<DoubleAnimation Duration="0:0:10" To="400" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).Children[1].(TranslateTransform.X)" />
<DoubleAnimation Duration="0:0:10" To="200" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).Children[1].(TranslateTransform.Y)" />
```

Instead of using the indexer within the transformation group it would also be possible to access the ScaleTransform element by its name. The following code simplifies the name of the property:

```xml
<DoubleAnimation Duration="0:0:10" To="5"
    Storyboard.TargetName="scale1"
    Storyboard.TargetProperty="(ScaleX)" />
```

With WPF it is also necessary to specify the RoutedEvent property with the EventTrigger. With Windows Universal apps, the event is automatically fired on loading of the element. This can be explicitly specified with WPF:

```xml
<EventTrigger RoutedEvent="Loaded">
    <BeginStoryboard>
```

Figures 30.23 and 30.24 show two states from the animated ellipse.

![](img/3d365b72b289213a91ade7eb366b8f35_1138_0.png)

Figure 30.23

![](img/3d365b72b289213a91ade7eb366b8f35_1138_1.png)

Figure 30.24

Animations are far more than typical window-dressing animation that appears onscreen constantly and immediately. You can add animation to business applications that make the user interface feel more responsive. The look when a cursor moves over a button, or a button is clicked, is defined by animations.

The following table describes what you can do with a timeline.

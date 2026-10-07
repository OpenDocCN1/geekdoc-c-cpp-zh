
# TRANSFORMATION TIP

A Storyboard can change a transformation's properties, but it cannot create a new transformation from scratch. In the rotating button example, the Storyboard can change the RenderTransform's angle of rotation, but it cannot make the RenderTransform out of nothing, so the Button Style makes an initial RenderTransform that rotates the button by 0 degrees.

In general, if you want to rotate, stretch, or otherwise change a control's transformation, you must give it an initial transformation for the Storyboard to modify.

The sbSpin Storyboard is also defined as a resource to further simplify the Button's code. You could even define the EventTrigger in the Button Style to make the Button's code really simple. In some cases, it may make sense to define triggers more or less the same thing: For example, consider the CentralizedTriggers example program shown in Figure 14-2. This program displays a series of thumbnail images on the left. When you click on one, the image expands and moves to fill the area on the right.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_275_0.png)

FIGURE 14-2

In this example, all of the thumbnail images do more or less the same thing: They expand their images. In programs like one that displays a series of controls that serve similar purposes, it may make the program's logic easier to understand if their triggers are all placed together. This might make sense for a series of thumbnails, buttons, menu items, radio buttons, or any other set of controls that perform roughly the same actions.

When a routed event is triggered, it moves through the hierarchy of controls that contains the one that started it. The CentralizedTriggers example displays its controls on a Canvas, when the user clicks on one of the thumbnails (an Image control), a MouseLeftDown event starts at the thumbnail, moves up to the Canvas, and then moves up again to the Window. The program's code can catch the event at any of those levels.

The following code fragment shows the structure of the CentralizedTriggers program's Canvas control:

```
<Canvas Margin="5">
  <Canvas.Resources>
    <!-- Define an unnamed Image Style. -->
    <Style TargetType="Image">
      <Setter Property="Opacity" Value="0.5"/>
      <Setter Property="Width" Value="100"/>
      <Setter Property="Height" Value="100"/>
      <Setter Property="Stretch" Value="Uniform"/>
      <Setter Property="BitmapEffect">
        <DropShadowBitmapEffect/>
      </Setter>
    </Style>
  </Canvas.Resources>
```

```
<!-- Define a Storyboard for each Image. -->
<Storyboard x:Key="sbImg1">
  Code omitted ...
</Storyboard>
Define the other Storyboards
</Canvas.Resources>
```

```
<!-- Handle MouseLeftDown events. -->
<Canvas.Triggers>
  <EventTrigger SourceName="RoutedEvent" Tag="Image.MouseLeftDown">
    <EventTrigger.Actions>
      <RemoveStoryboard StoryName="sbImg1"/>
      <RemoveStoryboard StoryName="sbImg2"/>
      <RemoveStoryboard StoryName="sbImg3"/>
      <RemoveStoryboard StoryName="sbImg4"/>
    </EventTrigger.Actions>
  </EventTrigger>
```

```
<BeginStoryboard Name="sbImg1">
  <StaticResource sbImg1/>
</BeginStoryboard>
</EventTrigger.Actions>
</EventTrigger>
Define EventTriggers for the other Images
</Canvas.Triggers>
```

```
<!-- Build the controls. -->
```

```
<Image Canvas.Left="0" Canvas.Top="0" Name="img1" Source="Canon01.jpg"/>
<Image Canvas.Left="0" Canvas.Top="100" Name="img2" Source="Canon02.jpg"/>
<Image Canvas.Left="0" Canvas.Top="200" Name="img3" Source="Canon03.jpg"/>
<Image Canvas.Left="0" Canvas.Top="300" Name="img4" Source="Canon04.jpg"/>
</Canvas>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_276_0.png)

The Canvas.Resources section defines an unnamed Style (Width, Height, Stretch, etc.) and the storyboards that enlace and move the thumbnails to fill the viewing area.

The Canvas.Triggers section defines the Images' EventTriggers. The previous code shows only the first trigger in detail. Its SourceName and RoutedEvent attributes indicate that the trigger catches the MouseLeftDown event raised by an Image control named img1.

The Trigger.Actions section uses Remove objects to cancel any previously running Storyboards, restoring the thumbnails to their original positions. (The section "Controlling Storyboards" later in this chapter says more about objects like RemoveStoryboard.) It then uses a BeginStoryboard to run the sbImg Storyboard, which moves the Image control img1 to the viewing area.

Having defined the resources and triggers, the program's code that defines the Image controls is quite simple and easy to understand.

It often makes sense to keep triggers with controls that raise the events, but sometimes it makes the code easier to read if you group pieces of code together. That makes the individual sections of code (styles, storyboards, triggers, controls) easier to understand.

# Storyboards in Property Elements

Rather than referring to a storyboard defined in a resource, the code can include a storyboard directly inside the BeginStoryboard element. The following code shows a Button that includes a storyboard:

```
<Button Width="100" Height="50" Content="Click Me">
  <Button.Triggers>
    <EventTrigger RoutedEvent="Button.MouseEnter">
      <EventTrigger.Actions>
        <BeginStoryboard>
          <Storyboard>
            Place animations here
          </Storyboard>
        </BeginStoryboard>
      </EventTrigger.Actions>
    </EventTrigger>
  </Button.Triggers>
</Button>
```

# Storyboards in Styles

Building a storyboard right into a control makes its definition quite long and requires some deeply nested elements, so you may want to define them in resources. For example, the following code defines a Button Style that includes event triggers:

```
<Style x:Key="btnEventSize" TargetType="Button">
  <Setter Property="Width" Value="100"/>
  <Setter Property="Height" Value="50"/>
  <Triggers>
    <EventTrigger RoutedEvent="Button.MouseEnter">
      <EventTrigger.Actions>
        <Storyboard Storyboard="StaticResource BigSize"/>
      </EventTrigger.Actions>
    </EventTrigger>
    <EventTrigger RoutedEvent="Button.MouseLeave">
      <EventTrigger.Actions>
        <Storyboard Storyboard="StaticResource SmallSize"/>
      </EventTrigger.Actions>
    </EventTrigger>
  </Triggers>
</Style>
```

A program could use the following code to define a button that uses this style:

<Button Style="StaticResource btnEventSize" Content="New Size"/>

# PROPERTY TRIGGER ANIMATIONS

Normally a property trigger uses setters to change property values immediately, but you can use property triggers to run storyboards. How a property trigger applies a storyboard differs from how it applies a setter because the two have different purposes.

A setter changes a property value as long as another property has a certain value. For example, suggest a Button has a property that takes action when the IsMouseOver property is True. As long as that property is True, a Setter changes the Width to 150. If MouseOver is no longer True, the Setter returns to its normal size, say 100. Here the Setter changes the Width property 150 as long as IsMouseOver is True.

In contrast, an animation makes a change smoothly from one value to another over time. For an animation might make a Button's Width vary from its original value of 100 to 150 over a period of 1 second. In that case, it doesn't make sense to have the animation as long as the IsMouseOver property is True. The animation will finish in 1 second even if IsMouseOver is True for 10 minutes. Now the animation replay again and again, but that would be a bit strange in this example.

In order to sensibly apply animations, a property trigger provides two extra sections that can execute animations in addition to ordinary setters: EnterActions and ExitActions.

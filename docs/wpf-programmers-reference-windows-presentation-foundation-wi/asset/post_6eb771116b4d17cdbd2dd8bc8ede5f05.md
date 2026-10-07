
As before, setters take immediate action.

The animations include the EnterActions section when the property's value changes to the target value. In the previous example, they would execute when the Button'sMouseOver property value becomes True.

The animations include the ExitActions section when the property's value changes from the target value to another value. In the previous example, they would execute when the Button'sMouseOver property changes from True to False.

The following code shows a Button Style that uses a property trigger to invoke both Setters and Storyboards:

```xml
<Style x:Key="btnStyle" TargetType="Button">
  <Setter Property="Width" Value="100"/>
  <Setter Property="Height" Value="50"/>
  <Style.Triggers>
    <Trigger Property="IsMouseOver" Value="True">
      <Setter Property="FontStyle" Value="Italic"/>
      <Trigger.EnterActions>
        <BeginStoryboard Storyboard="StaticResource sbBigSize"/>
      </Trigger.EnterActions>
      <Trigger.ExitActions>
        <BeginStoryboard Storyboard="StaticResource sbSmallSize"/>
      </Trigger.ExitActions>
    </Trigger>
  </Style.Triggers>
</Style>
```

Available for download on Wrox.com

## PropertyTriggerButton Example

When the Button'sMouseOver property becomes True, the Setter immediately changes the Button's FontStyle to Italic.

When the Image'sMouseOver property changes to True, the EnterActions execute, launching the Storyboard named sbBigSize. Storyboard animates the Button's Width and Height, changing to 150 and 75, over a period of 0.2 seconds.

When the Image'sMouseOver property changes to False, the ExitActions execute, launching the Storyboard named sbSmallSize. Storyboard animates the Button's Width and Height, changing to 100 and 50, respectively, over a period of 0.2 seconds.

The PropertyTriggerButton example shown in Figure 14-3 uses this code to make its buttons grow and shrink as you move the mouse over them. In Figure 14-3, the mouse is over the middle button, so that the button has italic text. The sbBigSize Storyboard has finished running, so the button is at its larger size.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_279_0.png)

FIGURE 14-3

The GrowingButtons example program shown in Figure 14-4 demonstrates the three combinations of trigger types and trigger actions: property triggers with setters, property triggers with storyboards, and event triggers with storyboards.

The buttons in the top row change their size, so they grow larger but their text stays the same. The buttons on the bottom row change the scale transformations, so their text grows with them.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_280_0.png)

Figure 14-4

# STORYBOARDS

Now that you understand how to start a storyboard, it's time to learn how to build one. A storyboard is an object that defines a timeline for one or more animations.

An animation manages the transition of a property from one value to another time. An animation can include a start time indicating when the transition should begin and a duration however long the animation should last.

Animation make animation easy by handling a lot of very tricky details. For example, suppose you want to control a control's Width from 50 to 200 over a 1-second interval. To do this you would need to know how many values you can effectively display in 1 second. The number of frames you display depends on the speed of your computer, the complexity of the window (enlarging the control might force other controls to, e.g., if they are in a StackPanel), and other factors that are outside your control. With enough time and effort, you could probably work this out and come with something reasonable; but, unless your application does nothing but display animations, you would probably be better off concentrating on other parts of the program.

The animation classes let you specify what you want done and ignore how it is. You say you property changed to a certain value over the next 3 seconds, and the animation classes figure out how to do it.

The classes still do not provide absolutely perfect timing. After all, they are subject to the same issues that you would be if you were to perform the animation yourself. But they do a reasonable job with less effort on your part.

# ANIMATION PERFORMANCE

To get the best performance out of your animations, try to minimize their size effects. For example, suppose you use an animation to change the size of a Button. If that Button is inside a StackPanel, then changes to its size affect the locations of the other controls in the StackPanel. If the Button contains controls simple text, changing its size may force WPF to rearrange all of those controls. Depending on the complexity of the program, these kinds of side effects may slow the animation considerably.

When you design an animation, particularly one that changes control positions and sizes, try to minimize the effects of those changes on other controls. You can fix this by moving the Button into a Grid so that changes to its size don't affect other controls.

Specific kinds of animation handles properties of different data types such as Double, Color, String, Thickness, and many others.

The following code shows a simple Storyboard containing five DoubleAnimation objects.

```xml
<Storyboard>
  <DoubleAnimation TargetProperty="Left" To="120" Duration="0:0:0.5"/>
  <DoubleAnimation TargetProperty="Top" To="0" Duration="0:0:0.5"/>
  <DoubleAnimation TargetProperty="Width" To="485" Duration="0:0:0.5"/>
  <DoubleAnimation TargetProperty="Height" To="400" Duration="0:0:0.5"/>
  <DoubleAnimation TargetProperty="Opacity" To="1" Duration="0:0:0.5"/>
</Storyboard>
```

The first animation makes the Canvas.Left property of the control 120 over 0.5 seconds. The second animation similarly changes the Canvas.Top property to 0 over 0.5 seconds. The third and fourth animations change Width and Height properties to 485 and 400, respectively. The final animation changes Opacity to 1 so it is completely opaque.

# Storyboard and Animation Properties

The animation classes have several properties that determine the animation's behavior. For example, Duration determines how long the animation should take to finish.

The Storyboard class provides many of the same properties, the animations it contains can inherit. For example, Storyboard has a Duration attribute to 0:0:2 and you do not give the animations their own Duration attributes, then the animations run in 2 seconds.

The following list describes the most useful animation and storyboard properties:

- AccelerationRatio — Determines the fraction of the total time that is spent accelerating value before reaching its peak rate of change
- AutoReverse — If this is True, then the animation automatically reverses itself when it is done
- BeginTime — The time at which the animation should start after the storyboard has started. This has the form hours:minutes:seconds.

> GLACIAL ANIMATION
If your animation seems to be moving incredibly slowly or not at all, check your BeginTime and Duration properties and make sure they have the right format. For example, if you accidentally set Duration to 0:1 instead of 0:0:1, then the animation will take 1 minute rather than the 1 second you intended.

- DecelerationRatio — Determines the fraction of the total time that is spent decelerating value from its peak rate of change before stopping at its final value.
- Duration — The time the animation should take to move the property from its start value to its final value. This has the form hours:minutes:seconds.
- FillBehavior — Determines what the animation finishes with. This can be HoldEnd (the property keeps its final value) or Stop (the property immediately snaps back to its "default" value).
- RepeatBehavior — Determines how often the animation is repeated. This property can be one of three forms: a repeat count (2x means repeat twice, 5x means repeat five times), or the keyword Forever (0:0:10 means repeat until 10 seconds have elapsed).
- SpeedRatio — Determines the speed with which time pass relative to the animation's parent. For example, if SpeedRatio is 2, then time passes twice as quickly as the animation as it does for its parent.


## Ellipse Button Triggers

When events occur, the template's triggers make appropriate changes to the control's appearance. Mostly these involve changing Opacity values to make some controls more visible while hiding others.

The IsMouseOver property shown in the following code is the most interesting of the plate's triggers:

```
<Trigger Property="IsMouseOver" Value="True">
  <Setter TargetName="ellipseLeftHighlight" Property="Opacity" Value="1"/>
  <Setter TargetName="ellipse" Property="Opacity" Value="0"/>
  <Setter TargetName="content" Property="Opacity" Value="1"/>
  <Setter TargetName="content" Property="BitmapEffect" Value="StaticResource bmeMouseOver"/>
  <Setter TargetName="sparkle" Property="Opacity" Value="0.75"/>

<!-- Start the sparkle animation. -->
<Trigger.EnterActions>
  <BeginStoryboard StoryName="begSparkle">
    <Storyboard BeginTime="0:0:1" RepeatBehavior="Forever">
      <DoubleAnimationUsingKeyFrames
        Duration="0:0:2"
        Storyboard.TargetName="transSparkle
        Storyboard.Target="Angle">
        <LinearDoubleKeyFrame
          Value="0" KeyTime="0:0:0"/>
        <LinearDoubleKeyFrame
          Value="360" KeyTime="0:0:1"/>
        <LinearDoubleKeyFrame
          Value="360" KeyTime="0:0:2"/>
      </DoubleAnimationUsingKeyFrames>
    </Storyboard>
  </BeginStoryboard>
</Trigger.EnterActions>

<!-- Stop the sparkle animation. -->
<Trigger.ExitActions>
  <StopStoryboard BeginName="begSparkle"/>
</Trigger.ExitActions>
</Trigger>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_315_0.png)

This code uses simple setters to do the following immediately when it starts:

- Make the upper-left highlight fully opaque instead of translucent.
- Make the light gray color that tones down the other controls transparent so that all of the other controls have their full brightness.
- Make the ContentProperty fully opaque instead of translucent.

Give the ContentPresenter an OuterGlowmapEffect (defined in the template's Resources section). Make the white sparkle highlight visible with Opacity = 0.75. This makes the left edge high brighter than the right highlight and prepares the sparkle for the animation described next.

The Trigger's EnterActions occur when the MouseOver property becomes True. This code begins a Storyboard that uses a DoubleAnimationUsingKeyFrames object to animate the sparkle highlight brush. The brush uses a RotateTransform named sparkle that initially has Angle = 0, so the brush is not rotated. The animation makes Angle sweep from 0 to 360 degrees over a 1-second period and repeats indefinitely.

The Trigger's ExitActions occur when the MouseOver property becomes no longer True (in other words becomes False). When that happens, the code stops the Storyboard that animates the sparkle.

The Template's other triggers are much simpler. the following code shows the IsPressed property that executes when the user presses the button:

```
<Trigger IsPressed="True">
  <Setter TargetName="ellipseLeftHighlight" Property="Opacity" Value="0"/>
  <Setter TargetName="ellipseRightHighlight" Property="Opacity" Value="0.75"/>
  <Setter TargetName="content" Property="BitmapEffect" Value="StaticResource bmePressed"/>
</Trigger>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_316_0.png)

### EllipseButton

This code uses some setters to do the following:

- Hide the upper-left highlight by setting Opacity = 0.
- Display the lower-right highlight by setting Opacity = 0.75.
- Give the ContentPresenter the OuterGlowmapEffect named bmePressed, which is defined in the template's Resources section, uses a larger Glow than MouseOver effect, so the glow of ContentPresenter is larger. You can see the difference if you compare Figures 15-10 and 15-11.

The template's other triggers in the following code work similarly:

```
<Trigger Property="IsDefault" Value="True">
  <Setter TargetName="content" Property="Opacity" Value="0.15"/>
  <Setter TargetName="edgeHighlight" Property="Stroke" Value="StaticResource brDefaultEdgeHighlight"/>
</Trigger>
<!-- Default -->
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_316_1.png)

```
<Trigger Property="IsDefault" Value="False">
  <Setter TargetName="edgeHighlight" Property="Stroke" Value="StaticResource brEdgeHighlight"/>
</Trigger>
<!-- Not defaulted. -->
```

```
<Trigger Property="IsEnabled" Value="False">
  <Setter TargetName="content" Property="Opacity" Value="0.6"/>
</Trigger>
<!-- Disabled. This comes last so it gets precedence. -->
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_317_0.png)

These triggers are fairly straightforward, giving controls new Stroke values and shuffling around Opacity values.

## TEMPLATE TRICKS 3-

- Using BlurEffect to make an object appear three-dimensional (the outer edge with blurred highlight on it)
- Using Opacity 0 to make translucent highlights
- Using brushes that blend from a color to transparent to make highlights fade away
- Using brushes that blend a color to transparent and back to a color to make objects are visible in multiple places
- Using different brushes for different control states (the normal vs. defaulted highlights)
- Using different BitmapEffects for different control states (the smaller glow for MouseOver and the larger glow for IsPressed)
- Animating changes to the brush's transformation

## RESEARCHING CONTROL TEMPLATES

To effectively build templates, you need to learn how the control provides for you and what behaviors you need to provide for it. You also need to determine what events the control provides so that you know you have a chance to make the control take action.

For example, WPF provides an assortment of events including MouseEnter, MouseOver, MouseLeftDown, Pressed, and Click. If your trying to write a Button template, mouse events can you use to change the Button's appearance? Which properties and behaviors does the Button provide for you, and which ones do you need to implement?

The Button templates described in the previous sections use the Button’s MouseOver, IsPressed, IsEnabled, IsFocused, and IsDefault properties. The Button class defines no matter what controls you add to the template to provide basic Button behavior.

As described in the "Template Binding" section earlier in this chapter, templates can also read some of the property values provided by the underlying control. For example, the Button class provides Background, BorderBrush, and BorderThickness properties that a template can read using template bindings. Button also inherits properties such as Width and Height that you can also read with template bindings.

So, how do you learn what properties and templates are available?

One good source of information is Microsoft’s "Control Styles and Templates" web page at mdn.microsoft.com/cc2875(vs.9).aspx. That page provides links to other pages that describe the features available for different controls.

For example, the "Button Styles and Templates" page lists the Button’s states and properties and tells where to get them. For instance, the Pressed state (which you can read with the IsPressed property) tells when the button is pressed.

These web pages also show the default templates used by controls. The Button control’s default template is 84 lines long and fairly complicated. Some are longer and much more complex.

In addition to Microsoft’s web pages, you can make a control tell you about its template. The ShowTemplate example shown in Figure 15-13 displays the default template for a control. When you click on the "Show Template" button, the program displays the default template for the control named Target. In Figure 15-13, that control is the Slider in the upper-left corner. To see the template used by a different kind of control, replace the Slider with a different control, name it Target, and run the program.

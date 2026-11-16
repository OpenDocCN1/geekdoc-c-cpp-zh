![](bbox=[0.08, 0.05, 0.18, 0.22])

# HOW'D YOU DO?

I didn't give you much to go on this time, so don't worry if you got some of these wrong or not-quite-right.

A Storyboard that targets the Background property of the element that is being styled:

```
`<Storyboard TargetProperty = "Background">`
```

You don't need to specify the TargetName or Target if the Storyboard applies to the object being styled.

A Storyboard that targets the Opacity property of a Label with the x:Name set to MyLabel1:

```
`<Storyboard TargetName = "MyLabel1" TargetProperty = "Opacity" >`
```

This is just standard XAML.

A Storyboard that targets the Background property of the element being styled, and repeats three times:

```
`<Storyboard TargetProperty="Background" RepeatBehavior="3x">`
```

Did you remember the 'x'?

A Storyboard that targets the Width property of the element being styled, lasts 0.5 seconds, and then returns to the original value:

```
`<Storyboard TargetProperty="Width" Duration="0:0:0.5" AutoReverse="True">`
```

Duration can be set to any of the values of the Duration structure, but is most often set to a TimeSpan in the format Days.Hours:Minutes:Seconds.Fractions.

For example, a duration of 1 second (the default) would be specified as:

```
`Duration = "0:1.0"`
```

Be careful not to omit the value before the colon. A DURATION of .0 would be 1 day, not 1 second .

Did you find AutoReverse? You might have thought you'd use FillBehavior to control this, but FillBehavior controls whether or not you can change the property after the animation ends. FillBehavior.HoldEnd (the default), keeps applying the end value. If you want to be able to change the value, set FillBehavior to Stop.
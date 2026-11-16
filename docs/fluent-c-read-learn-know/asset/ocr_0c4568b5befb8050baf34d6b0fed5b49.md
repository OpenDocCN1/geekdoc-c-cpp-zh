# PUT ON YOUR THINKING HAT

Back to our explorer. Can you duplicate (or improve on) my version?

![](bbox=[0.095, 0.055, 0.225, 0.205])

This is a TextBlock. The LinearGradientBrush is declared in the XAML and
displayed as an underline, because that's the default behavior for a TextDecoration. The
equivalent C# to reference the pen would be:

```
TextBlock.TextDecorations[0].TextDecoration.Pen.Brush
```

The XAML syntax is in the solution on the next page, but see if you can
work out how to do it without help.

![](bbox=[0.445, 0.37, 0.9, 0.64])

In the code, remember that all of the
controls except Location represent properties
of the TextDecoration.Pen, not the
decoration itself.

Once you get the sample working, can you identify the location of each of these lines?

![](bbox=[0.345, 0.71, 0.55, 0.865])
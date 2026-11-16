WPF controls can be transformed, which in the context of graphics means they can be moved, sized or skewed. We'll look at the basics of the Transform object here, and in the next chapter we'll take a quick look at how to use transformations to animate things.

The TextBox has been skewed. Not something I'd recommend as a rule, but it can be useful in some situations.

WPF supports a kind of graphic manipulation called a pixel shader. The bad news is that pixel shaders are written in a language called HLSL, which makes C# look like baby talk. The good news is that two common effects, blurring and shadowing, are defined for you in the Framework.

The TextBox has a drop shadow, one of the effects defined in the Framework Library.

You apply color to an object with a Pen (for lines) or a Brush (for areas).
# # BASIC TEXT CHARACTERISTICS

Three of the four basic characteristics of text are represented in the typeface class. The fourth, the FontSize, isn't, because any typeface can be displayed at any size.

![](bbox=[0.08, 0.22, 0.9, 0.5])

You specify any of the characteristics using the properties of static classes defined by the Framework Library.

You could, in theory, create your own definition of one of these style types, but it wouldn't map to the layout of a font file, so there's really no point.

Most people don't make a distinction between oblique and italic, but they are quite different: The italic version of a font uses a different glyph.

![](bbox=[0.63, 0.61, 0.8, 0.67])

> ### PUT ON YOUR THINKING HAT
> 
> Not all fonts have every version of every characteristic. Very few define all the possible weights, for example, and a font that defines an italic version usually doesn't include an oblique. What do you think WPF does if you specify a characteristic that isn't defined?
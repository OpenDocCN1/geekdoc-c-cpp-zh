![](bbox=[0.069, 0.093, 0.649, 0.197])

*Figure 2.16: Minute hand subjected to the display-transform sequence (1 of 3).*

![](bbox=[0.083, 0.243, 0.649, 0.376])

*Figure 2.17: Minute hand subjected to the display-transform sequence (2 of 3).*

![](bbox=[0.087, 0.421, 0.644, 0.587])

*Figure 2.18: Minute hand subjected to the display-transform sequence (3 of 3).*

Thus far, it may seem that our use of a template did nothing but make the XAML more complicated. After all, we could have simply specified a `Polygon` after specifying the `Ellipse`. But now, as we build the hour hand—and later, when you perform the suggested exercises—you will appreciate this template strategy.

We will now construct the hour hand via the same approach—instantiating the template—but we are going to make two adjustments.

First, we want to adjust its shape to distinguish it from the minute hand. To do so, we attach a scale transformation to the instance. Although we used scale transforms earlier in this chapter, here we pursue a different goal. Whereas our previous use of a transform sequence was to control our scene's size and placement on the output device—a display transformation—here we are using scaling to construct a component of the scene—what we call a **modeling transformation**. This distinction between two uses of transformations has meaning to us as developers, but is unknown to the underlying platform since the same mechanism—`RenderTransform`—is used for both. (It's a “what-for” distinction, not a “how-to” distinction.)

Second, to make it easy to distinguish between the two clock hands when the full scene is composed, we want to adjust the scene so that they don't both lie on
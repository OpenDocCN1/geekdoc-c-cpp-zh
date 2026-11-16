# # EXPLORING BRUSHES

There are a LOT of UI widgets in the Framework, and they have a LOT of properties that control how they work. While you can change most of the properties in the WPF Designer and all of them in code, when I'm exploring a new widget, I often build a little window that lets me play with the control's properties interactively. Let's do that with the graphic objects we're exploring in this chapter, so you can get a feel for how these "explorers" work. You might find the idea useful when you're working on your own.

Here's the basic structure of our Explorer. We'll start with the SolidColorBrush tab.

We'll add a tab for each object or set of properties we want to explore.

These TextBlock elements display the Value of the Slider.

You could use any control that has a Background property to display the color. This happens to be a Canvas.

![](bbox=[0.12, 0.41, 0.85, 0.76])

Simple Slider controls let us set the ARGB values of a color.

When you click the Set Color button, the Background property of the Canvas should be set in code. You'll need to create a new Color first, and then pass it to the constructor of the SolidColorBrush you'll use to set the Background.